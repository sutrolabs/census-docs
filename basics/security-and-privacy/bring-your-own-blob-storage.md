# Using Your Own Blob Storage

## 💽 How Census Uses Blob Storage

All sources configured using the [Advanced Sync Engine](/sources/overview#sync-engines) use Amazon S3 as temporary storage for the data that is unloaded from your warehouse before it is sent to the destination service or application.

By default, Census manage this storage on your behalf. This includes managing credentials with narrow permissions and short lifetimes, encrypting data in the bucket at rest and in transit, and automatically removing old data from the bucket once it is no longer in use. This approach is secure and is used by the vast majority of Census customers.

If you perfer manage your own S3 bucket for legal or regulatory reasons, this article will describe how to set that up.

{% hint style="info" %}
This feature available to Census Enterprise Plans. Please contact your Census account representative for details before proceeding with these steps.
{% endhint %}


## 🪛 Initial Setup

This guide will take you through the steps to prepare a bucket for use with Census. These instructions only apply to Amazon S3 buckets. If you require support for Google Cloud Storage or Azure Blob Storage, please contact your Census representative.

We will use the `aws` CLI to create and configure your bucket - you should [install this tool and configure it to use your credentials](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) before starting. Similar configuration is also possible using the AWS Console UI but those instructions are not provided here.

In order to proceed, you will also need the Census AWS Account ID (`341876425553`) and your customer-owned bucket External ID - these will be provided to you by your Census representative.

### 1. Choose a bucket name

Choose a name for your bucket that is memorable and clear. For example, if your company name is "FooCorp", you might call your bucket "foocorp-census-sync-temporary-files".

### 2. Set up shell variables

In a shell, set up a few variables we'll use throughout the rest of this guide:

The `CENSUS_AWS_ACCOUNT_ID` and `CENSUS_CUSTOMER_BUCKET_EXTERNAL_ID` will be provided to you by your Census representative. This may be your account contact or you can reach out to support@getcensus.com

```
export BUCKET_NAME=<your bucket name>
export CENSUS_AWS_ACCOUNT_ID=<provided by Census>
export CENSUS_CUSTOMER_BUCKET_EXTERNAL_ID=<provided by Census>
```

### 3. Create and configure the bucket

Create the S3 bucket. Currently, `us-east-1` and `eu-central-1` are the only supported regions, as this is where the Census processing infrastructure is located. Note that it's okay if your data warehouse is located in a different region.

```
aws s3api create-bucket --acl private --bucket $BUCKET_NAME --region=us-east-1
```

Remove all public access from the bucket:

```
aws s3api put-public-access-block --bucket $BUCKET_NAME \
  --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"
```

Encrypt all data in the bucket:

```
aws s3api put-bucket-encryption --bucket $BUCKET_NAME \
  --server-side-encryption-configuration '{"Rules": [{"ApplyServerSideEncryptionByDefault": {"SSEAlgorithm": "AES256"}}]}'
```

(Optional) Choose an automatic retention period to remove stale data from the bucket that is more than X days old. This is a safety measure in case Census fails to remove data from the bucket after processing it. In this example, we set the retention period to 14 days, the same value Census uses by default:

```
aws s3api put-bucket-lifecycle-configuration --bucket $BUCKET_NAME --lifecycle-configuration \
  '{"Rules":[{"Expiration":{"Days":14},"ID":"expire-census-temp-files","Prefix":"","Status":"Enabled","AbortIncompleteMultipartUpload":{"DaysAfterInitiation":14}}]}'
```

### 4. Create an IAM role granting Census access

Census needs to be able to list, read, write, and delete items from the S3 bucket. In order to do so, you'll create an IAM role defining the allowed permissions and give the Census AWS account the ability to assume that role.

Feel free to adjust the names of the role and the inline policy to match your organization's naming scheme if you have one.

First, create an empty role with a policy that allows Census to assume it via AWS Account ID and External ID:

```
aws iam create-role --role-name census-data-warehouse-client --assume-role-policy-document \
  '{"Version":"2012-10-17","Statement":{"Effect":"Allow","Action":"sts:AssumeRole","Principal":{"AWS":"'341876425553'"},"Condition":{"StringEquals":{"sts:ExternalId":"'$CENSUS_CUSTOMER_BUCKET_EXTERNAL_ID'"}}}}'
```

This command should print out a role document that looks something like this:

```
{
  "Role": {
    "Path": "/",
    "RoleName": "census-data-warehouse-client",
    "RoleId": "...",
    "Arn": "arn:aws:iam::12345678:role/census-data-warehouse-client",
    "CreateDate": "2020-09-22T20:48:21+00:00",
    "AssumeRolePolicyDocument": {
      "Version": "2012-10-17",
      "Statement": {
        "Effect": "Allow",
        "Action": "sts:AssumeRole",
        "Principal": {
          "AWS": "77665544"
        },
        "Condition": {
          "StringEquals": {
            "sts:ExternalId": "CustomerOwnedS3Bucket/333444555"
          }
        }
      }
    }
  }
}
```

_Important_: Take note of the `Arn` from the role document - you'll need to give this value to your Census representative to finish the configuration.

Then add a policy to the role granting limited access to the S3 bucket:

```
aws iam put-role-policy --role-name census-data-warehouse-client \
  --policy-name census-data-warehouse-client --policy-document \
  '{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Action":["s3:GetBucketLocation","s3:GetObject","s3:HeadBucket","s3:DeleteObject","s3:ListBucket","s3:PutObject"],"Resource":["arn:aws:s3:::'$BUCKET_NAME'/*","arn:aws:s3:::'$BUCKET_NAME'"]}]}'
```

### 5. Finishing up

Provide the bucket name you chose and your Role ARN (it should look like `arn:aws:iam::12345678:role/census-data-warehouse-client` to your Census representative and they will complete the configuration on your behalf. Once Census is configured to use your S3 bucket, you can verify that it is working correctly in Census by going to Connections, then click "Test" next to your warehouse to run a test sync using your configured S3 bucket.

## Ongoing Maintenance

You shouldn't need to take any further action once you've set up your bucket. Census will automatically create and remove files as needed, and the S3 retention policies you defined in the previous step will automatically remove any stale data in the unlikely event that Census fails to do so.

We strongly recommend that once set up, you do not modify the bucket or any of the keys it contains in any way. Adding, removing, modifying, or renaming data in your Census bucket is not supported and will likely cause Census syncs to fail. In addition, the Census bucket should not be simultaneously employed for any other purposes.

If you need to rename your bucket or the IAM roles you have granted to the bucket, please contact Census Support.

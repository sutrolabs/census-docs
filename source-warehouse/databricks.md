---
description: >-
  This page describes how to configure Databricks credentials for use by Census
  and why those permissions are needed.
---

# Databricks

## Configuring a new Databricks connection

1. Visit the **Connections** section on Census, and press **Add Data Warehouse Connection**, selecting **Databricks** from the list.

2. Enter the **hostname, port, and HTTP Path** for your cluster. These can be found in the Databricks UI under **Advanced Options** _→_ **JDBC/ODBC**:  
  


![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/603ee80124d2d21e45edbebd/file-dgqKduDlbF.png)

3. Enter your Databricks **Access Token.** A token can be generated in the **User Settings** page in the Databricks UI.

4. Add the following configuration parameters to your cluster. This can be done under **Advanced Options** _→_ **Spark.**

```text
spark.hadoop.fs.s3n.impl.disable.cache true
spark.hadoop.fs.s3.impl.disable.cache true
spark.hadoop.fs.s3a.impl.disable.cache true
```

5. After the connection is saved, go ahead and press the **Test** button. This will validate that you've completed the above steps correctly. Once you've got a checkmark for all four steps, you're good to go!

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5ea7766b2c7d3a7e9aebba26/file-bagpimlYKc.png)




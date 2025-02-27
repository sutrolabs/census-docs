---
description: >-
  Census offers a number of login methods to make it easy for your team to get
  in while keeping your data secure.
---

# Login & SSO Settings

## Google Login

Users can of course sign up with a simple email & password, but we offer some more advanced options for organizations using GSuite.

**Automatically add GSuite domain members to this organization.** If this option is enabled, any user that signs up for Census with your Google domain will automatically be added to your organization.&#x20;

**Force all users to use Google Account sign in.** When enabled, users will not be able to use email & password to log into this organization. This is an easy way to level up the security of your Census instance by requiring two-factor authentication on your GSuite organization.

<figure><img src="../../.gitbook/assets/screenshot 2023-07-18 at 16.22@2x.png" alt="" width="375"><figcaption><p>You can configure your organization's Google Login settings on the organization settings page.</p></figcaption></figure>

## Single Sign On

Census also supports login via SSO with SAML 2.0, including Okta on our Enterprise Plan. Setting this up is easy but requires a manual step from our support team. Please contact [support@getcensus.com](mailto:support@getcensus.com) if you'd like to set up SSO in your organization. Below is a useful set of Frequently Asked Questions regarding Census' SSO capabilities.

### FAQs for Single Sign On

#### **What does SAML do for an organization?**

Once SSO is set up, any client employees that have access to Census inside their IdP will be able to login to Census using their IdP for authentication.

#### Which Identity Providers (IdPs) does Census support?

We work with all SAML 2.0 Identity Providers (IdPs).

#### If SSO is enabled, is there any way to bypass it and login?

If SSO is enabled, it is the only path into the Census account.

#### How does MFA impact logging in when using SAML?

MFA is integrated directly with the client’s SSO provider. Census will not be aware of MFA. Census sees the user after they have completed authentication, which includes MFA.

#### How can I provision users with SAML enabled?

We treat your IdP as the source of truth for who has access to your Census account. To give someone access to your Census account, you'll need to provide access via your IdP.

After being provisioned to Census within your IDP new users can login to Census to create their user within your Census Organization. After logging in for the first time they will need to be added by an existing user to a Workspace. &#x20;

#### What is the user’s default workspace and role if their account is created from a SAML-initiated login?

On initial login, the user will be added as an organization member and will not have access to any workspaces. An organization administrator will need to assign the user to specific workspaces inside Census.

**How do I delete users from my organization?**

If SSO is enabled, you cannot remove users from Census. We let the IdP be the source of truth - if the user is no longer in your IdP, they will not be able to access Census, even if you see their name still listed in your Census memberships page.

####

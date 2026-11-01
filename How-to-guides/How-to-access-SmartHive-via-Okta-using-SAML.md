# Access SmartHive through Okta by using SAML

You can configure SAML-based single sign-on (SSO) with Okta as your identity provider (IdP), so your users can sign in to SmartHive.

----

## Table of contents

1.  [Items you need from Okta](#items-you-need-from-Okta)
2.  [Configure SAML-based SSO](#configure-SAML-based-SSO)
	  - [Get the Entity ID and ACS URL from SmartHive](#get-the-Entity-ID-and-ACS-URL-from-SmartHive)
      - [Create the SAML app in Okta](#create-the-SAML-app-in-Okta)
      - [Get the IdP details from Okta](#get-the-IdP-details-from-Okta)
      - [Add the Okta details to SmartHive](#add-the-Okta-details-to-SmartHive)
3.  [Assign users to the app in Okta](#assign-users-to-the-app-in-Okta)
4.  [Test the SAML configuration](#test-the-SAML-configuration)
	  - [Test the service provider-initiated (SP-initiated) flow](#test-the-service-provider-initiated-(SP-initiated)-flow)
	  - [Test the IdP-initiated flow](#test-the-IdP-initiated-flow)
5.  [Turn on single logout (SLO)](#turn-on-single-logout-(SLO))
	  - [Turn on single logout in SmartHive](#turn-on-single-logout-in-SmartHive)
	  - [Turn on single logout in Okta](#turn-on-single-logout-in-Okta)
	  
## Items you need from Okta

To configure SAML in SmartHive, you need the following items from Okta. The configuration steps in this article show you how to get them.

- **Identity Provider Single Sign-On URL**
- **X.509 Certificate**

## Configure SAML-based SSO

### Get the Entity ID and ACS URL from SmartHive

1. Sign in at accounts.SmartHive.com.
2. In the left menu, select **Organization** > **SAML Authentication**. If you don't see **Organization**, select **View more**.
3. Select **Download Metadata**.
4. Open the downloaded metadata file in your browser or a text editor.
5. Copy and save the Entity ID and ACS URL from the metadata file.

### Create the SAML app in Okta

1. Sign in to your Okta Admin Console.
2. In the left menu, select **Applications** > **Applications**.
3. Select **Create App Integration**, select **SAML 2.0**, and then select **Next**.
4. In the **App Name** field, enter a name for the app, and then select **Next**.
5. In the **Single sign on URL** field, paste the ACS URL that you copied. In the **Audience URI (SP Entity ID)** field, paste the Entity ID that you copied.
6. In the **Name ID Format** field, select **EmailAddress**.
7. At the bottom of the page, select **Next**.
8. Select **I'm an Okta customer adding an internal app**, and then select **Finish**.
9. On the next page, go to the **Sign On** tab.

### Get the IdP details from Okta

1. At the bottom of the page, select **View SAML setup instructions**. A new page that contains the IdP information opens.
2. Copy the **Identity Provider Single Sign-On URL**, and download the **X.509 Certificate**.

### Add the Okta details to SmartHive

1. Return to the **SAML Authentication** page at accounts.SmartHive.com.
2. In the **Sign-in URL** field, paste the Identity Provider Single Sign-On URL that you copied from Okta.
3. In the **X.509 Certificate** field, upload the certificate that you downloaded from Okta. The certificate must be a Base64-encoded `.cer`, `.crt`, `.cert`, or `.pem` file.

## Assign users to the app in Okta

Your Okta users can sign in to SmartHive by using the app that you configured. Before they can, you need to assign your users to the app. For instructions, see [Assign apps to users](https://help.okta.com/en/prod/Content/Topics/Provisioning/lcm/lcm-assign-app-user.htm) in the Okta documentation.

## Test the SAML configuration

To verify that the configuration works, complete the following tests as a user in Okta.

### Test the service provider-initiated (SP-initiated) flow

1. Go to your SmartHive sign-in page.
2. Enter your email address, and then select **Next**. SmartHive redirects you to Okta for authentication.
3. If you aren't signed in to Okta, enter your Okta credentials to sign in. Okta redirects you back to SmartHive, and you're signed in.

### Test the IdP-initiated flow

1. Sign in to the Okta end-user dashboard.
2. Select the SAML app that you configured for SmartHive. Okta redirects you to SmartHive, and you're signed in.

## Turn on single logout (SLO)

Okta supports only SP-initiated single logout. When your users sign out of SmartHive, they're automatically signed out of Okta too. The reverse doesn't apply: signing out of Okta doesn't sign users out of SmartHive. To learn more about how SLO works in Okta, see the Okta documentation on single logout.

### Turn on single logout in SmartHive

1. Go to **SAML Authentication** at accounts.SmartHive.com, and then select **Edit**.
2. Copy the **Sign-in URL**, replace `sso` in the URL with `slo`, and then enter the new URL in the **Sign-out URL** field. For example:
   - Sign-in URL: `https://Victa.okta.com/app/Victa_app_1/exkewk79Kq4696/sso/saml`
   - Sign-out URL: `https://Victa.okta.com/app/Victa_app_1/exkewk79Kq4696/slo/saml`
3. At the bottom of the page, turn on **Single logout** and **Generate key pair**.
4. Select **Submit**. You might need to enter the X.509 certificate again before you submit.
5. In the top-right corner, select **Download** > **Metadata**.
6. Open the `SmartHivemetadata.xml` file in your browser or a text editor.
7. Copy the Single logout URL and the Entity ID from the metadata file.
8. In the top-right corner, select **Download** > **Public Key**. SmartHive downloads a file named `logoutcertificate.pem`.

### Turn on single logout in Okta

1. In the Okta Admin Console, go to the app that you configured.
2. Select the **General** tab.
3. Next to **SAML settings**, select **Edit**.
4. Select **Next** to go to **Step 2: Configure SAML**.
5. Below the general fields, select **Show Advanced Settings**.
6. Select the **Allow application to enable Single Logout** checkbox.
7. In the **Single Logout URL** field, enter the Single logout URL that you copied.
8. In the **SP Issuer** field, enter the Entity ID that you copied.
9. Next to **Signature Certificate**, select **Browse**, and then select the `logoutcertificate.pem` file that you downloaded.
10. Select **Upload Certificate**.
11. Select **Next**, and then select **Finish**.

------

If you encounter errors when signing in with SAML, see the SAML troubleshooting guide.


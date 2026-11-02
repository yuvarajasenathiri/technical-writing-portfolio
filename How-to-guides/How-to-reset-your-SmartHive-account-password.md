# Reset your SmartHive account password

Use this procedure to reset your forgotten password.

> **Note:** If you remember your password and want only to change it, see [Change your password](https://help.SmartHive.com/portal/en/kb/accounts/manage-your-SmartHive-account/articles/securing-your-SmartHive-account#Change_Password).

## Table of contents

1.  - [Prerequisites(#prerequisites)
2.  - [Reset your password](#reset-your-password)
3.  - [Verify your identity](#verify-your-identity)
      - [Verify with an OTP sent to your email address](#verify-with-an-OTP-sent-to-your-email-address)
      - [Verify with an OTP sent to your mobile number](#verify-with-an-OTP-sent-to-your-mobile-number)
      - [Verify with a push notification sent to your recovery device](#verify-with-a-push-notification-sent-to-your-recovery-device)
      - [Verify by proving domain ownership](#verify-by-proving-domain-ownership)
4.  - [Reset a user's password as an organization admin](#reset-a-user's-password-as-an-organization-admin)
5.  - [Troubleshooting](#troubleshooting)
      - [Email address or mobile number verification](#email-address-or-mobile-number-verification)
      - [Recovery device verification](#recovery-device-verification)
      - [Domain verification](#domain-verification)
----

## Prerequisites

To verify your identity, you need at least one of the following:

- A recovery email address that's associated with your SmartHive account
- A recovery mobile number that's associated with your SmartHive account
- A recovery device (for example, OneAuth without multifactor authentication turned on)
- A domain that's added and verified with your SmartHive organization, if you're an organization admin

If your account is secured with multifactor authentication, you must also be able to complete the multifactor authentication verification.

## Reset your password

1. Go to the [Forgot Password](https://accounts.SmartHive.com/password) page. Alternatively, go to the [sign-in page](https://accounts.SmartHive.com/), and then select **Forgot Password**.
2. Enter your email address or mobile number, and then select **Next**.
3. Enter the CAPTCHA, and then select **Next**.
4. Select **Continue** to reset your password.
5. Verify your identity by using a recovery option that you configured for your account. For details, see [Verify your identity](#verify-your-identity).
6. If you turned on multifactor authentication for your account, complete the multifactor authentication verification.
7. Enter your new password, enter it again to confirm it, and then select **Change Password**.
8. If you want to end your active sessions or API tokens, select them, and then select **Continue**.
9. Sign in to your account by using your new password.

## Verify your identity

You can verify your identity by using a one-time password (OTP), a push notification, or proof of domain ownership. Use a recovery option that you configured for your account.

### Verify with an OTP sent to your email address

1. Select **Send OTP**. SmartHive sends the OTP to the email address that you used to start the request. To verify with a different email address that's associated with your account, select it from the list of available email addresses on the page.
2. If SmartHive prompts you, enter the full email address to send the OTP to.
3. Enter the OTP that you received, and then select **Verify**.

### Verify with an OTP sent to your mobile number

1. Select **Send OTP**. SmartHive sends the OTP to the mobile number that you used to start the request. To verify with a different mobile number that's associated with your account, select it from the list of available numbers on the page.
2. If SmartHive prompts you, enter the full mobile number to send the OTP to.
3. Enter the OTP that you received, and then select **Verify**.

### Verify with a push notification sent to your recovery device

1. If SmartHive prompts you, select **Verify using device**. SmartHive sends a push notification to your recovery device.
2. In OneAuth, approve the request.

### Verify by proving domain ownership

1. Select **View all options**.
2. If SmartHive prompts you, select **Verify via domain**. SmartHive shows the instructions.
3. Read the instructions, and then select **Proceed**.
4. If SmartHive prompts you, select the domain to continue with.
5. Enter the full domain name, and then select **Next**.
6. Select one of the methods that SmartHive shows for proving domain ownership:
   - Add a TXT record in your domain host.
   - Add a CNAME record in your domain host.
   - Upload an HTML file to the root directory of your website.
7. Enter the email address where you want to receive instructions for proving domain ownership, and then select **Send Email**.
8. Follow the instructions in the email.
9. In the email, select the **Change Password** link. SmartHive validates whether the DNS record or HTML file was added.
   - If it was added, SmartHive shows a success message. You can continue changing your password.
   - If it wasn't added, SmartHive shows an error message. The record that you added might not have propagated to all Domain Name System (DNS) servers yet, depending on the time-to-live (TTL) value. Wait a few minutes, and then refresh the page.

## Reset a user's password as an organization admin

If you're an administrator of an organization, you can reset passwords for users who can't reset them on their own. The following link provide the option 

To reset users' passwords, see [SmartHive Directory](https://help.SmartHive.com/portal/en/kb/directory/admin-guide/users/articles/reset-password-mfa): Recommended for admins who want to manage users across apps from a single place

## Troubleshooting

If you have trouble verifying your identity, review the following troubleshooting information. If you still can't verify your identity, contact support at [support@SmartHiveaccounts.com](mailto:support@SmartHiveaccounts.com).

### Email address or mobile number verification

| Issue     | Solution | 
|---|---|
| I don't remember my email address or mobile number| -Check the partially hidden email address or mobile number on the page. It might help you identify the one to enter.<br> - If you have other recovery options, verify by using one of them. |
| I lost access to my recovery email address or mobile number| - If you have other recovery options, verify by using one of them.|
| I get the error "Enter a valid email address or mobile number"| - Check that you entered the email address or mobile number that's partially hidden on the page.<br>- If the error continues, verify by using another recovery option, if one is available.|
| I'm not receiving the one-time password (OTP) in my email | - Check your spam folder. The email might be filtered as spam.<br>- Wait a few minutes. Your mail server or network provider might delay the email.<br>- Wait 30 seconds, and then select **Resend OTP**.<br>- If you have other recovery options, verify by using one of them. |
| My mobile number isn't listed as a verification option | - You can use only recovery mobile numbers for this verification.<br>- If you added a mobile number for multifactor authentication, that number doesn't appear here. It's available only during multifactor authentication verification. |
| I get the error "Incorrect OTP. Please try again" | - Check that you entered the OTP that SmartHive sent to your inbox.<br>- If you selected **Resend OTP** more than once, enter the OTP from the latest email or SMS message that you received.<br>- Alternatively, select the **RESET PASSWORD** link in the email, below the OTP, to reset your password. |

### Recovery device verification

| Issue     | Solution | 
|---|---|
| I set up OneAuth for my account, but I don't have an option to verify by using my device | - If you set up multifactor authentication by using OneAuth, you can verify by using OneAuth only during the multifactor authentication verification stage of recovery. The **Verify using device** option doesn't appear during this verification. |
| I'm not receiving push notifications | - Your device settings might be blocking the notifications. To change those settings, see our help article. |
| I can't find the option to verify by using a QR code or TOTP | - For this verification, the **Verify using device** option supports only push notifications. QR code and time-based one-time password (TOTP) modes aren't available.|
|  I get the error "Device authentication rejected" or "Device authentication pending" | - Select **Resend Push** to send another push notification to your device.<br>- If the error continues, verify by using another available option. |

### Domain verification

#### Domain ownership not proven yet

Domain ownership verification might fail for any of the following reasons:

- Incorrect values
- A higher time-to-live (TTL) value than expected
- A registrar conflict with the Domain Name System (DNS) provider

##### Incorrect values

**Cause:** You might have entered the CNAME values incorrectly on the DNS settings page for your domain.

**Solution:** Verify that you entered the following information correctly on the DNS settings page for your domain:

- The CNAME value that's provided in the email
- The domain name `https://domain.SmartHive.com`
- A TTL value of 1 hour

##### Higher TTL value

**Cause:** If the TTL value that you entered is higher than the value in the email, the CNAME records that you added in your DNS provider might not propagate in time for the verification process.

**Solution:** Check the TTL value, and then try to verify again after a while.

##### Registrar conflict with the DNS provider

**Cause:** You registered the domain with one provider but pointed the name servers to another provider. In this case, the CNAME records that you added at your domain registrar aren't valid. This might happen because you changed the DNS provider, either accidentally or to host your website, or because of your previous email provider configuration.

**Solution:** The CNAME records that you add at the provider where the name servers point are the valid ones. To check where the name servers point, do one of the following:

- Do a name server lookup for your domain to find where your domain is hosted.
- Ask your domain registrar or the technical contact for your domain where the name servers point.

#### I get the error "Maximum number of emails limit reached. Try again later."

**Cause:** You sent the domain verification instructions by email multiple times. To prevent email spamming, SmartHive doesn't send more emails for the next 24 hours.

**Solution:** Use one of the following options:

- Use the email that you already received, which has the CNAME records.
- To send instructions to a different email address after you sent multiple instructions, try again after 24 hours.
- Verify by using an alternate recovery option, if one is available.

----

*This document is part of the [technical-writing-portfolio](./README.md). SmartHive is a fictional software product created for the [technical-writing-portfolio](./README.md) repository.*


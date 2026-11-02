# Manage your SmartHive account

Use this procedure to manage the security, profile, and settings of your SmartHive account.

## Table of contents

1.  [Security](#security)
      - [Change your password](#change-your-password)
      - [Improve your account security](#improve-your-account-security)
      - [Allowed IP address](#allowed-ip-address)
      - [Application-specific passwords](#application-specific-passwords)
      - [Device sign-ins](#device-sign-ins)
2.  [Profile](#profile)
      - [Change your profile picture](#change-your-profile-picture)
      - [Edit your personal details](#edit-your-personal-details)
      - [Add an email address](#add-an-email-address)
      - [Change your primary email address](#change-your-primary-email-address)
      - [Add a mobile number](#add-a-mobile-number)
      - [Change your primary mobile number](#change-your-primary-mobile-number)
3.  [Settings](#settings)
      - [Preferences](#preferences)
      - [Authorized websites](#authorized-websites)
      - [Linked accounts](#linked-accounts)
	  
----

## Security

### Change your password

To change your SmartHive account password, sign in at accounts.SmartHive.com. If you forgot your password and can't sign in, reset your password instead.

> **Note:** By default, SmartHive requires passwords to meet the following criteria. A password must:
>
> - Be at least 8 characters long
> - Not contain parts of your email address, first name, last name, or display name
> - Not contain consecutive characters (such as `000`) or sequential characters (such as `123` or `abc`)
> - Not be a breached password
>
> When you enter a password, SmartHive checks whether it appears in any previous breaches by using Troy Hunt's breached password collection. If it does, SmartHive prompts you to enter a different password.

**To change your password:**

1. Sign in at accounts.SmartHive.com.
2. In the left menu, select **Security**.
3. In the **Password** section, select **Change Password**.
4. Enter your current password and your new password in the respective fields.
5. In the **Confirm New Password** field, enter your new password again.
6. Select **Change Password**.
7. When SmartHive asks whether you want to end your active sessions, select the option to end them, and then select **Terminate**. You can also revoke access to your connected apps that you previously gave permission to.

> **Note:** If your organization administrator turned on custom single sign-on (SSO) authentication for your account, you can't change your password. Contact your administrator for more information.

### Improve your account security

In addition to passwords and multifactor authentication, you can take other measures to improve the security of your account. The following sections describe some of them.

#### Allowed IP address

An allowed IP address is an IP address or a range of IP addresses that you set up to restrict access to your SmartHive account. After you configure an allowed IP address, you can sign in to your account only from the allowed IP addresses.

To set up an allowed IP address:

1. Sign in to your SmartHive account.
2. Under **Security**, select **Allowed IP Address**.
3. Select **Add Allowed IP Address**.
4. Select your current IP address, or manually enter the IP address that can access your SmartHive account. You can also enter a range of IP addresses.
5. Select **Next**.
6. Optional: Enter a name for the IP address.
7. Select **Add**.

> **Warning:** Use a static IP address. Dynamic IP addresses change, and you might be locked out of your account.

To turn off IP restriction for your SmartHive account:

1. Sign in to your SmartHive account from the IP address that you configured.
2. Under **Security**, select **Allowed IP Address**.
3. Select the IP address that you want to remove, and then select **Delete**.

#### Application-specific passwords

Application-specific passwords are 12-character passcodes that give an app permission to access your SmartHive Mail from email clients (for example, Microsoft Outlook and Mozilla Thunderbird), Jabber clients, and standalone apps.

If you turned on multifactor authentication:

- You can't use your SmartHive account password directly to access POP or IMAP email clients.
- You must use an application-specific password to access those apps. If an email client is compromised, you can still protect your SmartHive account by revoking the application-specific password that you generated for that client.

> **Note:** We recommend using application-specific passwords for your email clients even if you haven't turned on multifactor authentication for your SmartHive account.

**To generate an application-specific password:**

1. Sign in to your SmartHive account.
2. On the **Security** tab, go to **App passwords**.
3. Under **Application-Specific Password**, select **Generate New Password**.
4. Enter a name for the app that you want to create a password for, and then select **Generate**.
5. Copy the generated password. For security, SmartHive doesn't display it again.
6. In your email client, enter this password instead of your account password. Your user name stays the same.

#### Device sign-ins

**Device Sign-ins** lists the devices that you used to sign in to your SmartHive account. For each device, you can see information such as the names of the browsers that you signed in from and the time of each sign-in.

To remove a browser session from a device:

1. Sign in to your SmartHive account.
2. Under **Security**, select **Device Sign-ins**.
3. Select the device that you want to view.
4. Select the icon next to the browser that you want to remove.

---

## Profile

### Change your profile picture

1. Sign in to your [SmartHive account](https://accounts.SmartHive.com/).
2. Under **Profile**, select **Personal Information**.
3. Hover over your profile picture, and then select the icon that appears.
4. In the dialog, select the image that you want to use as your profile picture, and then select **Open**.

   > **Note:** Supported formats: JPG, JPEG, PNG, and GIF. Maximum file size: 10 MB.

5. Select who can view your profile picture:
   - **SmartHive users**
   - **Employees of my organization** (for organization users)
   - **Anyone** (To learn more, select the information icon.)
   - **Only myself**
6. Crop your picture, and then select **Update**.

> **Note:** To improve performance, SmartHive caches your profile picture locally when users in other datacenters view it.

### Edit your personal details

1. Sign in to your [SmartHive account](https://accounts.SmartHive.com/).
2. Under **Profile**, select **Personal Information**.
3. In the top-right corner of the **Personal Information** section, select **Edit**.
4. Edit your **First Name**, **Last Name**, **Nick Name**, **Gender**, **Language**, **Country**, and **Time zone**.
5. Select **Save**.

### Add an email address

1. Sign in to your [SmartHive account](https://accounts.SmartHive.com/).
2. Under **Profile**, select **My Email Addresses**.
3. Select **Add Email Address**.
4. Enter the email address, and then select **Add**.
5. Enter the one-time password that SmartHive sent to your email address, and then select **Verify**.

> **Note:** You can't edit an email address in your SmartHive account. To change an address, delete it, and then add a new one.

### Change your primary email address

1. Sign in to your [SmartHive account](https://accounts.SmartHive.com/).
2. Under **Profile**, select **My Email Addresses**.
3. Hover over the email address that you want to make primary, and then select the icon that appears.
4. Select **Make Primary**.

### Add a mobile number

1. Sign in to your [SmartHive account](https://accounts.SmartHive.com/).
2. Under **Profile**, select **My Mobile Numbers**.
3. Select **Add Mobile Number**.
4. Enter the mobile number, and then select **Add**.
5. Enter the one-time password that SmartHive sent to your mobile number, and then select **Verify**.

### Change your primary mobile number

1. Sign in to your [SmartHive account](https://accounts.SmartHive.com/).
2. Under **Profile**, select **My Mobile Numbers**.
3. Hover over the mobile number that you want to make primary, and then select the icon that appears.
4. Select **Update**.

---

## Settings

### Preferences

In the **Preferences** section, you can:

- [Change the date format](#change-the-date-format)
- [Change profile picture visibility](#change-profile-picture-visibility)
- [Turn email notifications on or off](#turn-email-notifications-on-or-off)

#### Change the date format

Choose a date format for **Activity Sessions**, **Activity History**, **App Sign-Ins**, and email notifications. You can select a predefined date format from the list, or you can set a custom date format.

To select a predefined date format:

1. Sign in at [accounts.SmartHive.com](https://accounts.SmartHive.com/).
2. In the left menu, select **Settings** > **Preferences**.
3. In the **Date Format** field, select the date format that you want from the list.

To set a custom date format:

1. Sign in at [accounts.SmartHive.com](https://accounts.SmartHive.com/).
2. In the left menu, select **Settings** > **Preferences**.
3. In the **Date Format** field, select **Custom**.
4. Enter the date format that you want.
5. Select **Save**.

#### Change profile picture visibility

You can restrict who can see your SmartHive account profile picture. Select one of the following options:

- Only registered SmartHive users
- Only contacts I chat with
- Only users in my organization
- Everyone
- Only myself

To change who can view your SmartHive account profile picture:

1. Sign in at [accounts.SmartHive.com](https://accounts.SmartHive.com/).
2. In the left menu, select **Settings** > **Preferences**.
3. Under **Profile Picture Visibility**, select the option that you want.

#### Turn email notifications on or off

SmartHive Accounts sends you the following emails. Some of them are turned on by default, and you can turn off the notifications that you don't need.

##### Password expiration alert

SmartHive sends this email when your SmartHive account password is about to expire, based on your organization's policy. If your organization sets an expiration time for your password, you must change your password before then. If no such policy applies in your organization, you don't see this alert in your preferences.

##### New sign-in to your account alert

SmartHive sends this email when you sign in to your SmartHive account from a new device, browser, or location. You can't turn off this notification if your administrator enforces it.

##### Third-party app access alert

SmartHive sends this email when your SmartHive account is signed in to a new third-party app (for example, an IMAP or POP client such as a mail app or calendar app), or when a third-party app that's already signed in accesses your SmartHive account from a new location. You can't turn off this notification if your administrator enforces it.

##### Newsletter subscription

SmartHive or its regional partners send this email. It contains information about SmartHive products, services, and events.

To turn an email notification on or off:

1. Sign in at [accounts.SmartHive.com](https://accounts.SmartHive.com/).
2. In the left menu, select **Settings** > **Preferences**.
3. Under **Email notifications**, turn the notifications that you want on or off.

### Authorized websites

Authorized websites are the websites that you gave permission to access your SmartHive account.

To view or remove authorized websites:

1. Sign in at [accounts.SmartHive.com](https://accounts.SmartHive.com/).
2. Under **Settings**, select **Authorized Websites**.
3. Select the website that you want to view or remove.
4. To prevent the website from accessing your SmartHive account, select **Revoke Access**.

### Linked accounts

Linked accounts are the third-party online accounts that you linked with your SmartHive account. You can sign in to your SmartHive account by using these linked accounts through federated sign-in.

To add a linked account:

1. Sign in at [accounts.SmartHive.com](https://accounts.SmartHive.com/).
2. Under **Settings**, select **Linked Accounts**.
3. Select **Add New Account**, and then select the account that you want to add.
4. Sign in to the selected account to link it to your SmartHive account.

To remove a linked account:

1. Sign in at [accounts.SmartHive.com](https://accounts.SmartHive.com/).
2. Under **Settings**, select **Linked Accounts**.
3. Hover over the account that you want to remove, and then select the icon that appears.
4. Select **Remove**.

----

*This document is part of the [technical-writing-portfolio](./README.md). SmartHive is a fictional software product created for the [technical-writing-portfolio](./README.md) repository.*
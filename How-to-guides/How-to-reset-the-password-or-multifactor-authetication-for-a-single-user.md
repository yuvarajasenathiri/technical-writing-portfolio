# Reset the password or multifactor authentication for a single user

Use this procedure to reset a user's password or multifactor authentication in SmartHive.

## Table of contents

1.  - [Prerequisites](#prerequisites)
2.  - [Select the user](#select-the-user)
3.  - [Reset the user's password](#reset-the-user's-password)
4.  - [Reset the user's multifactor authentication](#reset-the-user's-multifactor-authentication)

---- 

## Prerequisites

You need the following permissions:

- **Reset password**
- **Manage MFA**

## Select the user

1. Sign in to [SmartHive](https://directory.SmartHive.com/).
2. In the left menu, select **Admin Panel**.
3. Go to **User Management**. The **Users** tab opens by default.
4. Select the user whose password or multifactor authentication you want to reset.

> **Note:** You can reset the password or multifactor authentication only for confirmed users. You can't reset the password for users who have the **Yet to Verify** tag and a verified-domain email address. After the user approves the email address, you can use it to reset the password.

## Reset the user's password

1. Select **Reset Password**, and then enter the new password or select **Generate Password**.
2. To require the user to change the password the next time the user signs in, select **Force users to change the password on login**.
3. Under **Active login sessions**, review the following options:
   - **Web sessions will be cleared automatically**: This option is selected by default, and you can't clear it. The user is signed out of all active web sessions and must sign in again with the new password.
   - **Clear mobile sessions and API tokens**: Select this option if you need it. The user is signed out of all active mobile app sessions and must sign in again with the new password.
4. Enter your password to confirm the password reset.
5. To tell the user the new password, select **Email the new password to the users**.
6. Select **Reset**.

## Reset the user's multifactor authentication

1. Select **Reset MFA**, and then enter your password to confirm the reset of the user's multifactor authentication mode.
2. Select **Yes, Reset**.
3. In the confirmation dialog that appears, select **Yes, Reset**.

----

*This document is part of the [technical-writing-portfolio](./README.md). SmartHive is a fictional software product created for the [technical-writing-portfolio](./README.md) repository.*

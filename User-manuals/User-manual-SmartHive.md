# SmartHive user manual

- Version: 1.0
- Last updated: May 2026
- Applies to: SmartHive web app and mobile app

---

## Table of contents

1.  [Introduction](#introduction)
     - [Who this manual is for](#who-this-manual-is-for)
     - [What you'll learn](#what-youll-learn)
     - [How to use this manual](#how-to-use-this-manual)
     - [Related documentation](#related-documentation)
2.  [Overview](#overview)
     - [About SmartHive](#about-SmartHive)
     - [Key features](#key-features)
     - [How SmartHive works](#how-SmartHive-works)
     - [Core concepts](#core-concepts)
     - [User roles and permissions](#user-roles-and-permissions)
     - [System requirements](#system-requirements)
3.  [Getting started](#getting-started)
     - [Create your account](#create-your-account)
     - [Sign in to SmartHive](#sign-in-to-SmartHive)
     - [Set up your profile](#set-up-your-profile)
     - [Navigate the dashboard](#navigate-the-dashboard)
     - [Install the mobile app](#install-the-mobile-app)
     - [Invite your team](#invite-your-team)

---

## Introduction

### Who this manual is for

This manual is for support agents and team leads at customer support and SaaS companies who use SmartHive to manage cases and track team performance.

You don't need a technical background to use this manual. If you're a developer or system administrator who wants to configure or integrate SmartHive, see the [SmartHive Developer's manual](#) and the [SmartHive API Documentation](#).

### What you'll learn

This manual covers:

- What SmartHive is and how it works
- The user roles and permissions in SmartHive
- How to create your account, sign in, and set up your profile
- How to navigate the dashboard
- How to install the mobile app
- How to invite your team

### How to use this manual

If you're new to SmartHive, read this manual from start to finish. If you're looking for something specific, use the table of contents to go to that section.

This manual uses the following callouts:

> **Note:** Additional context or information that's worth knowing.

> **Important:** Information that you must read before you continue.

> **Warning:** Actions that might have irreversible consequences.

> **Tip:** Suggestions that help you work more efficiently.

### Related documentation

| Document | Description |
|---|---|
| [SmartHive Installation manual](#) | How to set up and deploy SmartHive for your organization |
| [SmartHive Developer's manual](#) | Technical manual for developers who build on SmartHive |
| [SmartHive API Documentation](#) | Complete reference for the SmartHive API |
| [SmartHive Mobile App manual](#) | Full list of features that the mobile app supports |
| [SmartHive Design Document](#) | Architecture and system design documentation |
| [SmartHive Release Notes](#) | Summary of changes in each SmartHive release |

---

## Overview

### About SmartHive

SmartHive is a case management platform for customer support and SaaS teams. You can use SmartHive as a cloud service or deploy it on your own servers. SmartHive gives support agents a single place to receive, manage, and resolve customer cases. It also gives team leads the visibility they need to monitor workload, track performance, and identify issues before they escalate.

SmartHive connects your support channels (email, live chat, web forms, and phone) in one platform. Every customer interaction becomes a case that you can track, assign, prioritize, and resolve without switching between tools.

### Key features

#### Case management

Create, assign, and resolve cases from a single interface. Set priorities, due dates, and custom fields to match your team's workflow. Track every update and communication in the full case history.

#### Omnichannel case intake

Receive cases from email, live chat, web forms, and phone in one place. SmartHive automatically deduplicates contacts and links related cases, so agents always have full context.

#### Smart assignment

Automatically assign cases to the right agent based on skills, availability, workload, or round-robin rules. Set escalation paths so that high-priority cases aren't missed.

#### Collaboration tools

Add internal notes, mention teammates, and share cases across teams without showing internal discussions to the customer. Link related cases, and merge duplicates in one step.

#### Service level agreement (SLA) management

Define SLA policies for different case types and customers. SmartHive tracks SLA compliance in real time and alerts agents and team leads before a breach occurs.

#### Knowledge base

Build and maintain an internal knowledge base that agents can search directly from a case. SmartHive automatically suggests relevant articles based on case content. You can publish articles to the customer portal.

#### Reporting and analytics

Track team performance, case volume, resolution times, customer satisfaction scores, and SLA compliance through built-in dashboards and customizable reports. Schedule reports to arrive in your inbox automatically.

#### Automation and workflows

Automate repetitive tasks by using the SmartHive workflow builder. Trigger actions based on case properties, status changes, or time conditions, without writing code.

#### Customer portal

Give customers a self-service portal where they can submit cases, check status updates, and browse your knowledge base. You can brand the portal to match your company.

#### Mobile app

Manage cases, respond to customers, and monitor team performance from the SmartHive iOS and Android apps.

### How SmartHive works

SmartHive organizes your support operation around three core activities:

1. Receive: Cases arrive in SmartHive from all your support channels. SmartHive automatically organizes them into queues based on your configuration.
2. Resolve: Agents pick up cases from their queue, communicate with customers, collaborate with teammates, and work toward resolution.
3. Review: Team leads monitor case volume, agent performance, and SLA compliance through dashboards and reports to keep the team on track.

SmartHive logs every action, so you always have a complete, auditable history of what happened, who did it, and when.

### Core concepts

Understanding these concepts helps you use SmartHive effectively.

#### Case

A case is a single customer issue or request. Every case has a unique ID, a status, a priority, and a history of all communications and actions taken. Cases are the primary unit of work in SmartHive.

#### Queue

A queue is a filtered view of cases. Queues organize cases by team, channel, priority, or any combination of criteria that you define. Agents work from queues instead of a single shared list of all cases, which avoids duplicate effort.

#### Project

A project is a collection of related cases. Use projects to group cases by customer, product, campaign, or initiative. Projects give team leads a high-level view of work across multiple cases.

#### Contact

A contact is a customer record in SmartHive. SmartHive automatically creates and updates contact records based on inbound case activity. Each contact has a full history of every case that the customer submitted.

#### SLA policy

An SLA policy defines the response and resolution time targets that apply to a case. SmartHive tracks SLA compliance automatically and shows breach warnings to agents and team leads.

#### Workflow

A workflow is an automated sequence of actions that SmartHive performs when certain conditions are met. Workflows reduce manual work and make sure that common case types are handled consistently.

#### Knowledge base article

A knowledge base article is a document that agents use to answer common questions. Articles can be internal (visible only to agents) or public (visible to customers through the customer portal).

### User roles and permissions

SmartHive has four built-in user roles. Your role determines what you can see and do in SmartHive.

| Role | Description | Key permissions |
|---|---|---|
| Admin | Full access to all SmartHive settings and features | Manage users, configure channels, set SLA policies, access all reports, and manage billing |
| Team Lead | Access to team management and reporting features | View all team cases, assign cases, access reports, manage queues and workflows, and invite users |
| Agent | Access to case management features | Create and resolve cases, communicate with customers, and access the knowledge base |
| Viewer | Read-only access | View cases and reports. Can't create or update cases. |

> **Note:** Admins can create custom roles with specific permission sets. If you need access to features that your role doesn't include, contact your SmartHive admin.

### System requirements

#### Web app

| Requirement | Minimum |
|---|---|
| Browser | Google Chrome 110 or later, Mozilla Firefox 110 or later, Microsoft Edge 110 or later, or Safari 16 or later |
| Internet connection | 5 Mbps or faster |
| Screen resolution | 1280 x 720 or higher |

> **Note:** SmartHive doesn't support Internet Explorer.

#### Mobile app

| Requirement | iOS | Android |
|---|---|---|
| Operating system | iOS 16.0 or later | Android 11.0 or later |
| Storage | 200 MB of free space | 200 MB of free space |
| Internet connection | 4G LTE or Wi-Fi | 4G LTE or Wi-Fi |

---

## Getting started

### Create your account

How you create a SmartHive account depends on how your organization set up SmartHive.

#### If your organization uses single sign-on (SSO)

1. Go to your organization's SmartHive URL. This is typically `https://yourworkspace.SmartHive.io`. If your admin set up a custom domain, use that URL instead.
2. Select **Sign in with SSO**.
3. Enter your work email address, and then select **Continue**.
4. Complete authentication through your organization's identity provider.

#### If your organization uses email and password

1. Check your inbox for the SmartHive invitation email from your admin.
2. In the email, select **Accept invitation**.
3. On the SmartHive sign-up page, enter your full name and create a password. The password must be at least 12 characters and include one uppercase letter, one number, and one special character.
4. Select **Create account**.
5. Verify your email address by selecting the link in the confirmation email that SmartHive sends you.

> **Note:** Invitation links expire after 72 hours. If your link expires, ask your SmartHive admin to resend the invitation.

### Sign in to SmartHive

#### Web app

1. Go to your organization's SmartHive URL (for example, `https://yourworkspace.SmartHive.io`).
2. Enter your email address and password.
3. Select **Sign in**.

If your organization turned on multifactor authentication, SmartHive prompts you for a verification code after you enter your password. Get the code from your authenticator app or email.

> **Tip:** Select **Remember this device for 30 days** to reduce how often you're prompted for multifactor authentication on trusted devices.

To reset a forgotten password:

1. On the sign-in page, select **Forgot password**.
2. Enter your email address, and then select **Send reset link**.
3. Check your inbox for the password reset email, and then select **Reset password**.
4. Enter and confirm your new password, and then select **Save**.

#### Mobile app

1. Open the SmartHive app on your device.
2. Tap **Sign in**.
3. Enter your organization's SmartHive URL, email address, and password.
4. Tap **Sign in**.

If multifactor authentication is turned on, enter the verification code when prompted.

### Set up your profile

Set up your profile so that your teammates can identify you and you receive the right notifications.

1. Select your avatar in the top-right corner of the screen.
2. Select **Profile settings**.
3. Update the following information:

   | Field | Description |
   |---|---|
   | **Full name** | Your display name across SmartHive |
   | **Profile photo** | A photo in JPG or PNG format. Maximum size: 5 MB. |
   | **Job title** | Your job title in the organization |
   | **Time zone** | The time zone that SmartHive uses to display time stamps and schedule reports |
   | **Language** | The SmartHive interface language. Supported languages: English, French, German, Spanish, Portuguese, and Japanese. |
   | **Notification preferences** | How and when SmartHive notifies you about case activity |

4. Select **Save changes**.

#### Set your availability status

Your availability status tells your team whether you're available to take new cases.

1. Select your avatar in the top-right corner of the screen.
2. Select your current status (for example, **Online**).
3. Select a status from the list:

   | Status | Description |
   |---|---|
   | **Online** | You're available and can receive new case assignments. |
   | **Busy** | You're available but at capacity. Smart assignment gives you lower priority for new cases. |
   | **Away** | You're temporarily unavailable. SmartHive doesn't assign new cases to you. |
   | **Offline** | You're not available. SmartHive doesn't assign new cases to you. |

> **Tip:** Set your status to **Away** or **Offline** when you take a break or leave for the day, so that SmartHive doesn't assign cases to you while you're unavailable.

### Navigate the dashboard

When you sign in to SmartHive, the dashboard is the first screen that you see. It gives you a real-time overview of your work and your team's activity.

#### Dashboard layout

The SmartHive interface has four main areas:

| Area | Description |
|---|---|
| Left navigation panel | Links to all main sections of SmartHive |
| Top navigation bar | The global search field, notification bell, help center link, and your account avatar |
| Main content area | The content for the section that you select in the left navigation panel |
| Right detail panel | When you open a case, the case details, contact information, and related cases |

The left navigation panel has the following sections:

| Section | Description |
|---|---|
| **Dashboard** | Your personal overview and team summary |
| **Cases** | All cases that you have access to |
| **Inbox** | Cases assigned directly to you |
| **Queues** | Shared queues for your team |
| **Projects** | Cases organized by project |
| **Contacts** | Customer contact records |
| **Knowledge base** | Internal and public articles |
| **Reports** | Performance dashboards and analytics |
| **Automation** | Workflow rules and triggers |
| **Settings** | Account and team configuration |

#### Your personal dashboard

Your personal dashboard shows:

- **My open cases:** Cases assigned to you that aren't resolved yet
- **Due today:** Cases assigned to you that have a due date of today
- **SLA at risk:** Cases where the SLA deadline is approaching
- **Recently updated:** Cases that you recently worked on
- **Team activity:** A real-time feed of your team's case activity

> **Tip:** Select **Customize dashboard** in the top-right corner of the dashboard to add, remove, or rearrange the widgets.

#### Use global search

Use the search bar at the top of the screen to find cases, contacts, articles, and teammates quickly.

1. Select the search bar, or press **Ctrl+K** (Windows) or **Command+K** (Mac).
2. Enter your search term.
3. Review the results, which SmartHive groups by type: Cases, Contacts, Articles, and Users.
4. Select a result to open it.

> **Tip:** Use search operators to narrow the results. For example, enter `status:open assignee:me` to find all open cases that are assigned to you.

### Install the mobile app

The SmartHive mobile app is available for iOS and Android. Use it to manage cases, respond to customers, and check your dashboard when you're away from your desk.

#### iOS

1. Open the **App Store** on your iPhone or iPad.
2. Search for **SmartHive**.
3. Tap **Get**, and then complete the installation.
4. Open SmartHive, and sign in. For details, see [Sign in to SmartHive](#sign-in-to-SmartHive).

#### Android

1. Open **Google Play** on your Android device.
2. Search for **SmartHive**.
3. Tap **Install**.
4. Open SmartHive, and sign in. For details, see [Sign in to SmartHive](#sign-in-to-SmartHive).

> **Note:** The SmartHive mobile app requires an active internet connection. Some features that are available in the web app might have limited functionality on mobile. For a full list of supported features, see the [SmartHive Mobile App manual](#).

#### Turn on push notifications

SmartHive sends push notifications for case assignments, mentions, SLA warnings, and customer replies.

##### iOS

1. Open **Settings** on your device.
2. Find **SmartHive** in the list, and then tap it.
3. Tap **Notifications**, and then turn on **Allow Notifications**.
4. Select the alert types that you want to receive.

##### Android

1. Open **Settings** on your device.
2. Tap **Apps** > **SmartHive** > **Notifications**.
3. Turn on notifications, and then select the alert types that you want to receive.

> **Tip:** You can also manage notification preferences in the SmartHive app. Tap **Profile settings** > **Notification preferences**.

### Invite your team

> **Note:** To invite new users to SmartHive, you need the **Admin** or **Team Lead** role.

To invite teammates to SmartHive:

1. In the left navigation panel, select **Settings**.
2. Select **Users and permissions**.
3. Select **Invite users**.
4. Enter the email addresses of the people you want to invite. Separate multiple addresses with commas.
5. Select a role for each user: **Admin**, **Team Lead**, **Agent**, or **Viewer**.
6. Optional: Assign the users to one or more teams.
7. Select **Send invitations**.

SmartHive sends each person an invitation email with a link to create an account. Invitation links expire after 72 hours.

#### Manage pending invitations

To view, resend, or cancel pending invitations:

1. Select **Settings** > **Users and permissions**.
2. Select the **Pending invitations** tab.
3. To resend an invitation, select **Resend** next to the user's email address.
4. To cancel an invitation, select **Revoke**.

---

*This document is part of the [technical-writing-portfolio](./README.md). SmartHive is a fictional product created for the [technical-writing-portfolio](./README.md) repository.*


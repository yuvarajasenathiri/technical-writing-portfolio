# Release notes for version 4.2

## 1. Release summary

### 1.1 Version number and build date

- Version: 4.2
- Build date: To be confirmed

### 1.2 Executive summary of the release

Release 4.2 adds the ability to update lien information on a loan after you create it. Before this release, you had to contact Operations whenever lien details changed, which caused delays and extra work. Now, users who have the Loan Maintenance role can update lien information directly on the **Loan Setup** page.

The system validates required fields before it saves your changes. It also shows a message when an update succeeds or fails, so you know the result right away.

---

## 2. What's new (major features)

### 2.1 Lien information updates: Key capabilities and how to access

#### Key capabilities

- **Update lien information after loan creation.** In the **Lien Information** section, you can change one or more of these fields:
  - **Lien Position**
  - **Recording Date**
  - **Assignment Date**
  - **Assignment Reference Number**
  - **Mortgage Amount**
- **Get validation feedback.** The system validates required fields before it saves your changes. If validation fails, the system displays a message and highlights the affected fields.
- **Get confirmation of a successful update.** If the update succeeds, the system displays a confirmation message and saves the revised lien information to the loan record.
- **Control who can edit.** Users who have the Loan Maintenance role can edit lien information. Users who don't have this role can view lien information but can't edit it.

#### How to access

To update lien information on a loan:

1. Open the loan record.
2. Go to the **Loan Setup** page.
3. In the **Lien Information** section, select **Edit**.
4. Change one or more of the available fields.
5. Select **Save**.

---

## 3. Enhancements and improvements

### 3.1 UI/UX updates

- The **Lien Information** section on the **Loan Setup** page now includes an **Edit** option.
- If validation fails, the system displays a message and highlights the affected fields.
- After a successful update, the system displays a confirmation message.

### 3.2 Performance and stability tuning

This release doesn't include performance or stability changes.

---

## 4. Bug fixes

### 4.1 Resolved issues list

This release doesn't resolve any tracked issues, so there are no tracking IDs to list.

---

## 5. Known issues and workarounds

### 5.1 Unresolved bugs

No unresolved bugs are reported for this release. The following limitations apply to lien information updates:

| Limitation | Description |
|---|---|
| No lien history | The system doesn't track a history of changes to lien information. |
| No rollback | You can't roll back a saved lien update to an earlier version. |
| View-only access without the Loan Maintenance role | Users who don't have the Loan Maintenance role can view lien information but can't edit it. |

Lien history tracking and rollback aren't included in Release 4.2.

### 5.2 Temporary mitigations

| Limitation | Mitigation |
|---|---|
| No lien history | Before you select **Edit**, note the current lien values if you need a record of them. |
| No rollback | To restore earlier values, select **Edit** again, enter the earlier values, and then select **Save**. |
| View-only access without the Loan Maintenance role | Ask your administrator to assign you the Loan Maintenance role, or contact Operations to update the lien information for you. |

---

## 6. Migration and upgrade instructions

### 6.1 Breaking changes and compatibility warnings

Release 4.2 doesn't introduce breaking changes. Review the following compatibility information before you upgrade:

- **Role requirement.** Only users who have the Loan Maintenance role can edit lien information. Users who don't have this role can view lien information but can't edit it.
- **Borrower Information.** You can continue to update borrower contact information, including **Primary Phone**, **Secondary Phone**, **Email Address**, **Preferred Contact Method**, **Communication Language**, and **Do Not Contact** preferences. This section doesn't change.
- **Escrow Information.** This section doesn't change in this release.
- **Existing loan records.** Existing lien information stays the same until a user edits it.

### 6.2 Step-by-step upgrade process

1. Identify the users who need to edit lien information.
2. Confirm that each of these users has the Loan Maintenance role. Assign the role to users who don't have it.
3. Upgrade to Release 4.2 by following your organization's standard deployment process.
4. Sign in as a user who has the Loan Maintenance role, and open a loan record.
5. Go to the **Loan Setup** page, and confirm that the **Lien Information** section includes the **Edit** option.
6. Sign in as a user who doesn't have the Loan Maintenance role, and confirm that the user can view lien information but can't edit it.
7. Tell your teams that they can now update lien information directly and no longer need to contact Operations.

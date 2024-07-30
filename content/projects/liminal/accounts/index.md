---
title: "Accounts"
showDate: false
summary: "How the account system is set up and various protections in place"
showSummary: True
showReadingTime: False
---
## Main concepts
- Passwords are hashed and never visible to administrators
- 4 main types of account: Developer, Manager, Student, Restricted
- You can reset your password at any time
____

## Role Higherarchy System
{{< mermaid >}}
graph BT;
R([Restricted])-->S([Student]);
S-->M([Manager])
M-->D([Developer])
{{< /mermaid >}}

| Role          | Permissions |
| -----         | ---               |
| Developer     | Debug and developer page        |
| Manager       | Manage user accounts           |
| Student       | Use printers          |
| Restricted    | View printers          |
## Password Reset system <kbd>All Users</kbd>

There is a very simple password reset system with a few options
### 1. User submitted
Once logged in, a user can request their password to be reset
### 2. Manager submitted
Managers have an account management page that can also request that each users password be reset

### My password is reset, now what?
Upon your next login, the password used is what will be set
____

## User Configuration <kbd>Manager</kbd> <kbd>Developer</kbd>
Visible by clicking the `Account Management` button on the home page
This enables you to do the following
- Update a users role
- Reset their password
    - You cannot view or manually change their password
    - This reset does not require knowledge of their existing password
- Revoke their login
- Create new users



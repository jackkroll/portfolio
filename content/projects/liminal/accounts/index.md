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
____

## Password Verification & Lockout protections
There are various protections set inplace to ensure security, but also make sure users aren't locked out from the system
### Standard Password Verification Process
When a user logs in, it will search for the user (not case sensitive) in the registered users and will compare hashes

As part of the password reset function or account creation process a hash could be set to <kbd>null</kbd> in which case it will hash and set the users password to that and let them in regardless

### Account lockout protections
There are a few cases in which users will be automatically let in
1. `/ref/config.json` does not exist
2. `students` does not exist in the config file
3. Username submitted is "team302" with any capitalization

____

## Role authentication & Lockout protections

### How a users role is determined after setup
Your role is assigned to you by a <kbd>manager</kbd>, or a <kbd>developer</kbd>\
<mark>They have a dashboard to change this if needed</mark>\
If a user does not have a role defined in `/ref/config.json` then they are automatically assigned <kbd>restricted</kbd>

### How a users role is determined during setup
During setup, the root user is automatically given the role of <kbd>developer</kbd> to ensure they have adaquite permissions to continue setup

### Role lockout protections
There are a few cases in which users will be automatically assigned as a <kbd>developer</kbd>
1. `/ref/config.json` does not exist
2. `students` does not exist in the config file
3. Username submitted is "team302" with any capitalization


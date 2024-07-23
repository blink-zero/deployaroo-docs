# User and Group Management

Manage users and groups in Deployaroo via **Settings > Users / Groups**.

## Create Users

You can create as many users as neeeded. When a user is created they are automatically assigned with 'Reader' permissions.

1. **Navigate to User Management**:
   - Go to the `User Management` section.

2. **Create a New User**:
   - Click the `Create New User` button.
   - Enter the username and a password, then click `Create User`.

## Edit Users

Editing a user allows you to change a username of a selected user.

1. **Edit a User**:
   - Click the `Edit` button next to the username you wish to edit.
   - Modify the username, then click `Save changes`.

## Reset User Password

You are able to reset a users password if needed. Generating a password is supported.

1. **Reset a User Password**:
   - Click the `Reset Password` button next to the username you wish to reset the password for.
   - Type a password into the **New Password** field and again into the **Confirm New Password** field.
   - Aternatively, use the generate button to auto fill a strong password into both fields.
   - Click `Reset Password` once filled out.

## Delete Users

Should you need to remove any users, you can use the delete button next to a username. 
> Please note: You cannot remove the first user created when deployaroo was first deployed. 

1. **Delete a user**:
   - Click `Delete` button next to the username you wish to remove from the deployaroo application.
   - Confirm that you do want to remove the user and click `Delete`.


## Manage Groups

Groups are a good way to restrict access if needed. in deployaroo the following Groups are default: Administrators and Readers. Administrators can use the entire application without restriction. The Reader group is able to view history, logs and the home dashboard. Readers cannot access settings or deploy virtual machines.

1. **Navigate to Group Management**:
   - Go to the `Group Management` section.

2. **Create a New Group**:
   - Click the `Create a Group` button to add a new group.

## Edit Groups

1. **Edit a Group**:
   - Click on `Edit` next to the group you wish to modify.
   - Modify the Group Name and Group Description.
   - Click `Save Changes`.

## Delete Groups

> Note: You cannot remove the Administrators or Readers groups. This includes even if you were to edit them and change the name.

1. **Delete a Group**:
   - Click on `Delete` next to a group you wish to remove.
   - Press `Delete` to confirm you want to remove the group.

## User-Group Association

To add/remove users to group follow the below
   
1. **Add Users to Groups**:
   - Add users to groups as needed using `+ Add to group`.

2. **Remove Users from Groups**:
   - Remove users from groups as needed using `- Remove from Group`.

![User Management](../assets/screenshots/user_management.png)

---

**Simplify your VM deployments with Deployaroo**

[Get Started](getting-started/overview.md) | [View Demo (Coming soon)](#) | [Report Bug](https://github.com/blink-zero/deployaroo/issues) | [Request Feature](https://github.com/blink-zero/deployaroo/issues)
# User Management in Linux

## Introduction to User Management in Linux
Linux is a multi-user operating system, meaning multiple users can operate on a system simultaneously. Proper user management ensures security, controlled access, and system integrity. 

Key files involved in user management:
- `/etc/passwd` – Stores user account details including username, UID, GID, home directory, and shell. Each line represents one user account.
- `/etc/shadow` – Stores encrypted user passwords and password-related information like expiration dates. This file is only readable by root.
- `/etc/group` – Stores group information including group name, GID, and group members. Each line represents one group.
- `/etc/gshadow` – Stores secure group details including encrypted group passwords and group administrators. This file is only readable by root.

## Creating Users in Linux
To create a new user in Linux, use:

### `useradd` Command (For most Linux distributions)
```bash
useradd username
```
This creates a user without a home directory. The user will be assigned:
- A unique UID (User ID)
- A primary group with the same name as the username
- A default shell (usually /bin/sh)
- No password (account will be locked)

To create a user with a home directory:
```bash
useradd -m username
```
The `-m` flag creates a home directory at `/home/username` and copies default files from `/etc/skel`.

To specify a shell:
```bash
useradd -s /bin/bash username
```
Common shell options:
- `/bin/bash` - Bourne Again Shell (most common)
- `/bin/sh` - Bourne Shell
- `/bin/zsh` - Z Shell
- `/sbin/nologin` - No login shell (for system accounts)

### `adduser` Command (For Debian-based systems)
```bash
adduser username
```
This is an interactive command that:
- Creates a home directory
- Sets up a default shell
- Prompts for a password
- Asks for user information (full name, phone, etc.)
- Creates a primary group
- Copies default files from `/etc/skel`

## Managing User Passwords
To set or change a user's password:
```bash
passwd username
```
This command will:
- Prompt for the new password twice
- Enforce password complexity rules
- Update the password in `/etc/shadow`

### Enforcing Password Policies
- **Password expiration**: Set password expiry days
  ```bash
  chage -M 90 username
  ```
  This sets the maximum number of days a password can be used before it must be changed.

- **Lock a user account**
  ```bash
  passwd -l username
  ```
  This prevents the user from logging in by adding a '!' at the start of their password hash.

- **Unlock a user account**
  ```bash
  passwd -u username
  ```
  This removes the '!' from the password hash, allowing the user to log in again.

## Modifying Users
Modify an existing user with `usermod`:
- Change the username:
  ```bash
  usermod -l new_username old_username
  ```
  This changes the username while preserving the UID and all other settings.

- Change the home directory:
  ```bash
  usermod -d /new/home/directory -m username
  ```
  The `-m` flag moves the contents of the old home directory to the new location.

- Change the default shell:
  ```bash
  usermod -s /bin/zsh username
  ```
  This changes the user's login shell to the specified shell.

## Deleting Users
To remove a user but keep their home directory:
```bash
userdel username
```
This removes the user account but preserves their home directory and files.

To remove a user and their home directory:
```bash
userdel -r username
```
The `-r` flag removes:
- The user account
- The home directory
- All files owned by the user
- The user's mail spool

## Working with Groups
### Creating Groups
```bash
groupadd groupname
```
This creates a new group with:
- A unique GID (Group ID)
- No members initially
- No password

### Adding Users to Groups
```bash
usermod -aG groupname username
```
The `-a` flag appends the user to the group (doesn't remove from other groups).
The `-G` flag specifies the group to add the user to.

### Viewing Group Memberships
```bash
groups username
```
This shows all groups the user belongs to, including:
- Primary group
- Secondary groups

### Changing Primary Group
```bash
usermod -g new_primary_group username
```
This changes the user's primary group, which affects:
- Default group ownership of new files
- Group permissions for the user

## Sudo Access and Privilege Escalation
### Adding a User to Sudo Group
On Debian-based systems:
```bash
usermod -aG sudo username
```
This allows the user to execute commands with root privileges using `sudo`.

On RHEL-based systems:
```bash
usermod -aG wheel username
```
The `wheel` group serves the same purpose as `sudo` in Debian-based systems.

### Granting Specific Commands with Sudo
Edit the sudoers file:
```bash
visudo
```
This opens the sudoers file in a safe way that prevents syntax errors.

Then add:
```bash
username ALL=(ALL) NOPASSWD: /path/to/command
```
This configuration:
- Allows the user to run specific commands without a password
- Restricts the user to only those commands
- Can be customized with specific hosts, users, or command paths
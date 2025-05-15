![](/images/sshclient.png)

# Connecting to a Linux Server

## Using SSH (Secure Shell)

SSH is a secure protocol used to connect to remote Linux servers. Here are the key points about SSH connections:

### Basic SSH Command
```bash
ssh username@hostname
```

### Common SSH Options
- `-p`: Specify a custom port (default is 22)
- `-i`: Use a specific private key file

## Enabling Password Authentication for SSH

By default, some Linux servers disable password authentication for SSH for security reasons. If you need to enable it, follow these steps:

1. **Edit the SSH configuration file:**
   
   Open the relevant configuration file (for example, `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`) with a text editor:
   ```bash
   vim /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
   ```

2. **Set `PasswordAuthentication` to `yes`:**
   
   Add or modify the following line:
   ```
   PasswordAuthentication yes
   ```

3. **Verify the change:**
   
   You can check the file to ensure the setting is correct:
   ```bash
   cat /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
   ```

4. **Restart the SSH service:**
   
   For the changes to take effect, restart the SSH service:
   ```bash
   sudo systemctl restart ssh
   ```

**Note:** Enabling password authentication can make your server more vulnerable to brute-force attacks. It is recommended to use SSH keys for authentication whenever possible and to secure your server with firewalls and fail2ban.



---
sidebar_position: 3
---

import TOCInline from '@theme/TOCInline';

# Setting Up SSH Authentication

## TOC

<TOCInline toc={toc} />

## Quickstart

### Setting Up Passwordless SSH Login for Your VPS

1. **Generate an SSH key pair locally:**
   Run the following command in your local terminal (skip this step if you already have a key pair):

```bash
ssh-keygen -t ed25519
```

2. **Specify storage location:**
   Press `Enter` to use the default directory (`C:\Users\Username\.ssh\` on Windows or `~/.ssh/` on Linux/macOS), or specify a custom path.
3. **Understand the key pair:**

- **Public Key (`.pub`):** Uploaded to the remote server to grant access.
- **Private Key (no extension):** Remains strictly local on your machine as your secret credential.

4. **Copy the public key to the server:**
   Use **Git Bash** on Windows (since default PowerShell/CMD lack `ssh-copy-id`). Replace the host details with your own:

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub <username>@<your_ip>
```

Enter your server password one last time to authorize the transfer.

5. **Verify key-based login:**

:::warning

Connect to your server using Git Bash or a standard terminal. If you connect successfully without being prompted for a password, key authentication is working. Do not close your terminal.

```bash
ssh <username>@<your_ip>
```
:::

6. **Disable password authentication for security:**

- Open the SSH configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```

- Locate `PasswordAuthentication`. Remove the leading `#` if commented out, and set its value to `no`:

```text
PasswordAuthentication no
```

- Save (`Ctrl + O`, `Enter`) and exit (`Ctrl + X`).
- Restart the SSH service:

```bash
systemctl restart ssh.service
```

7. **Test password rejection:**
   **Do not close your current active terminal session!** Open a **new terminal** tab/window and attempt to force a password login:

```bash
ssh -o PubkeyAuthentication=no <username>@<your_ip>
```

- If the server responds with `Permission denied (publickey)`, password authentication is successfully disabled.

---

## Description

### Why Use SSH Keys Instead of Passwords?

- **Brute-Force Protection:** Passwords can be targeted by automated dictionary attacks. Ed25519 SSH keys provide 256-bit cryptographic security, making brute-force cracking virtually impossible.
- **Zero-Knowledge Proof:** Your private key never leaves your local machine during authentication.
- **Convenience & Automation:** Key-based authentication provides fast, passwordless terminal logins and enables secure automated deployments.

---

## Further References

- [OpenSSH Official Documentation](https://www.openssh.com/)

---
sidebar_position: 2
---

import TOCInline from '@theme/TOCInline';

# vServer Login

This page explains how to log in to a vServer.

## TOC

<TOCInline toc={toc} />

### First login to the VPS using username and password:

1. **Open local console and run the SSH command:**

```bash
ssh <username>@<your_ip>
```

2. **Accept the host fingerprint:**
   Confirm the prompt on your first connection by typing `yes` and entering your password.

3. **You're logged in!**
   Your terminal prompt will change to show that you are connected:

```bash
username@servername:~#
```

:::note Host Fingerprint
A **host fingerprint** is a unique cryptographic hash of a server's public key used to verify its identity.

- **Identity Verification:** Ensures you are connecting to the correct server on your first login.
- **Security:** Protects against Man-in-the-Middle attacks. Your system saves the fingerprint in `known_hosts` and alerts you if it changes unexpectedly in the future.
:::

4. Next Step: [Set up SSH authentication on your vServer](sshkey.md) for better security.

## Further References

- [OpenSSH Official Documentation](https://www.openssh.com/manual.html)
- [SSH Key Management Best Practices](https://www.ssh.com/academy/ssh/key)

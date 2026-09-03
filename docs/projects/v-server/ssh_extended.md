---
sidebar_position: 30
---

import TOCInline from '@theme/TOCInline';


# Extended SSH Knowledge

Managing Commands and SSH Connections with Short Aliases.

## TOC

<TOCInline toc={toc} />

## Quickstart

### Creating an SSH Alias

When working with multiple SSH keys and servers, long SSH commands can become difficult to remember.

For example:

```bash
ssh -o -i ~/.ssh/id_ed25519 <username>@<your_ip>
```

:::note
Use **Git Bash** for the following commands, as alias is a Bash command and is not supported by Windows CMD or handled the same way in PowerShell.
:::

The command can be shortened by creating an alias:

```bash
alias myserver="ssh -o -i ~/.ssh/id_ed25519 <username>@<your_ip>"
```

You can now connect to the server using:

```bash
myserver
```

### Understanding the SSH Options

- `-i` specifies the **private SSH key** used for authentication:

```bash
-i ~/.ssh/id_ed25519
```

The path depends on where your SSH key is stored. `~/.ssh/id_ed25519` is a common location, but paths such as `../id_ed25519` are also possible.

- `-o` allows additional SSH configuration options to be specified directly in the command.

- `StrictHostKeyChecking=False` disables the normal SSH host-key confirmation.

> **Security note:** Disabling `StrictHostKeyChecking` is convenient for temporary setups, but it reduces SSH's protection against connecting to an unexpected server. For regular or production environments, keeping the default host-key checking enabled is recommended.

### Finding Your Current Directory

You can use:

```bash
pwd
```

`pwd` stands for **print working directory** and displays your current directory.

For example:

```bash
pwd
```

may return:

```text
/home/<username>
```

This is useful when working with relative paths such as:

```text
../id_ed25519
```

Keep in mind that `pwd` shows the directory of the machine where the command is executed. After connecting via SSH, it shows the directory on the remote server.

### Checking an Alias

List all currently configured aliases:

```bash
alias
```

To find a specific alias:

```bash
alias | grep myserver
```

or directly:

```bash
alias myserver
```

The output shows the command assigned to the alias:

```text
alias myserver='ssh -o -i ~/.ssh/id_ed25519 <username>@<your_ip>'
```

### Getting Help for `alias`

`alias` is usually a shell built-in command, so `alias -h` or `alias --help` may not work.

For Git Bash, use:

```bash
help alias
```

On Linux, you can also use the manual pages:

```bash
man alias
```

> **Note:** `man` is commonly available on Linux and other Unix-like systems, but not in standard Windows CMD or PowerShell. Git Bash provides access to many Unix-style commands, including `man` on installations where the manual pages are available.


### Making the Alias Permanent

Aliases created directly in the terminal normally only exist for the current shell session.

To make an alias permanent in Bash, open `.bashrc` and add the alias:

```text
nano ~/.bashrc
```

Add this alias at the end of the file, for example:

```bash
...
alias myserver="ssh -o -i ~/.ssh/id_ed25519 <username>@<your_ip>"
```

After changing the file, reload it. Alternatively, open a new terminal.

```bash
source ~/.bashrc
```

The alias will then also be available in new terminal sessions.

:::note
**Note:** The first time you use Git Bash, you may see a message asking to create `~/.bash_profile` to load `~/.bashrc`. Git Bash normally creates the required file automatically. This message should only appear during the initial setup and should not appear again afterwards.
:::

### Multiple SSH Keys

Aliases are especially useful when different servers require different SSH keys:

```bash
alias devserver="ssh -i ~/.ssh/dev_ed25519 developer@<dev_ip>"
alias testserver="ssh -i ~/.ssh/test_ed25519 tester@<test_ip>"
alias production="ssh -i ~/.ssh/prod_ed25519 admin@<prod_ip>"
```

Connections can then be established with short commands:

```bash
devserver
testserver
production
```

This makes it easier to keep track of which SSH key belongs to which server.

:::note
**Important:** Private SSH keys must never be committed to Git or shared with others. Public keys (`*.pub`) can be placed on the server for authentication.
:::

---

## SSH Config

Instead of using a shell alias, SSH provides its own configuration file. This allows you to define different **hosts, users, and SSH keys** and connect using a short, unique name.

The previous command was:

```bash
ssh -o -i ~/.ssh/id_ed25519 <username>@<your_ip>
```

With an SSH configuration, the goal is to connect using:

```bash
ssh <unique_name>
```

### 1. Create or edit the SSH config

The SSH configuration file is located in:

```text
~/.ssh/config
```

Check if the file already exists:

```bash
cat ~/.ssh/config
```

The file may be empty or already contain existing configurations.

Open it with an editor such as `nano` or `vim`:

```bash
nano ~/.ssh/config
```

Add a configuration for your server:

```text
Host <unique_name>
    HostName <your_ip>
    User <username>
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_ed25519
```

* `Host` defines the name used when connecting.
* `HostName` specifies the server's IP address or hostname.
* `User` specifies the username used for the connection.
* `IdentityFile` specifies which SSH private key should be used.

Save the file and exit the editor.

### 2. Connect using the SSH config

You can now connect using the name defined in `Host`:

```bash
ssh <unique_name>
```

SSH automatically uses the configured IP address, username, and private key.

For example:

```text
Host <your_servername>
    HostName <your_ip>
    User <your_username>
    IdentityFile ~/.ssh/id_ed25519
```

You can then simply use:

```bash
ssh myserver
```

### 3. Multiple SSH configurations

This becomes especially useful when using multiple servers or SSH keys:

```text
Host development
    HostName <dev_ip>
    User <username>
    IdentityFile ~/.ssh/dev_ed25519

Host production
    HostName <prod_ip>
    User <username>
    IdentityFile ~/.ssh/prod_ed25519
```

You can then connect with:

```bash
ssh development
```

or:

```bash
ssh production
```

This keeps the different servers and SSH keys organized in one configuration file.

### Conclusion

For SSH connections, using `~/.ssh/config` is preferable to creating shell aliases. The command

```bash
ssh <unique_name>
```

clearly indicates that an SSH connection is being established while keeping the actual connection details in the SSH configuration.

Shell aliases are still useful for shortening other long commands, but for SSH specifically, the built-in SSH configuration is the cleaner approach.

---

## Description

### Why Use SSH Aliases?

SSH aliases are useful when:

- Multiple servers need to be accessed regularly.
- Different SSH keys are used for different environments.
- Long SSH commands become difficult to remember.
- You want simple commands such as `devserver` or `production`.

For larger SSH setups, the SSH configuration file `~/.ssh/config` is an even better solution because it is specifically designed to manage multiple hosts and SSH keys.

---

## Further References

- [OpenSSH Documentation](https://www.openssh.com/manual.html)

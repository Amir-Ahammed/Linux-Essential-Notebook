# Differences Between `ssh_config`, `sshd_config`, `ssh_config.d/`, and `sshd_config.d/`

The files and directories `ssh_config`, `sshd_config`, `ssh_config.d/`, and `sshd_config.d/` play distinct roles in configuring SSH on a Linux system. Here’s an explanation of their purposes and differences.

---

## **1. `ssh_config`**
- **Purpose**: Configures the **SSH client** (the program you use to connect to an SSH server).
- **Location**: 
  - System-wide settings: `/etc/ssh/ssh_config`
  - User-specific settings: `~/.ssh/config`
- **Scope**: Affects all outgoing SSH connections made by the client.
- **Example Configuration**:
  ```plaintext
  Host *
      ForwardAgent yes
      ForwardX11 yes
      ServerAliveInterval 60
  ```
  - `Host *`: Applies settings to all SSH connections.
  - `ServerAliveInterval`: Specifies the interval for sending keep-alive messages.

- **Common Use Cases**:
  - Configure default behavior for outgoing SSH connections (e.g., preferred key types, default usernames).
  - Define settings for specific hosts (e.g., `Host github.com`).

---

## **2. `sshd_config`**
- **Purpose**: Configures the **SSH server** (the service running on the server to accept SSH connections).
- **Location**: `/etc/ssh/sshd_config`
- **Scope**: Affects all incoming SSH connections to the server.
- **Example Configuration**:
  ```plaintext
  PermitRootLogin no
  PasswordAuthentication yes
  Port 22
  ```
  - `PermitRootLogin`: Controls whether the root user can log in via SSH.
  - `PasswordAuthentication`: Enables/disables password-based authentication.
  - `Port`: Specifies the port number for the SSH server.

- **Common Use Cases**:
  - Configure access control, authentication methods, and security policies for the server.

---

## **3. `ssh_config.d/` Directory**
- **Purpose**: A directory for storing **additional client configuration files** for `ssh_config`.
- **Location**: `/etc/ssh/ssh_config.d/`
- **Scope**: Allows modular configuration for SSH clients, with settings split into multiple files.
- **How It Works**:
  - Files in this directory are read by the SSH client in addition to `/etc/ssh/ssh_config`.
  - Files are processed in alphabetical order.

- **Example**:
  - `/etc/ssh/ssh_config.d/10-defaults.conf`:
    ```plaintext
    Host *
        ServerAliveInterval 60
    ```
  - `/etc/ssh/ssh_config.d/20-custom.conf`:
    ```plaintext
    Host example.com
        User customuser
    ```

---

## **4. `sshd_config.d/` Directory**
- **Purpose**: A directory for storing **additional server configuration files** for `sshd_config`.
- **Location**: `/etc/ssh/sshd_config.d/`
- **Scope**: Allows modular configuration for the SSH server, with settings split into multiple files.
- **How It Works**:
  - Files in this directory are read by the SSH daemon (`sshd`) in addition to `/etc/ssh/sshd_config`.
  - Files are processed in alphabetical order.

- **Example**:
  - `/etc/ssh/sshd_config.d/10-defaults.conf`:
    ```plaintext
    PermitRootLogin no
    ```
  - `/etc/ssh/sshd_config.d/20-custom.conf`:
    ```plaintext
    Port 2222
    ```

---

## **Key Differences Between Them**

| **File/Directory**   | **Purpose**                      | **Scope**            | **Affects**                 |
|-----------------------|----------------------------------|----------------------|-----------------------------|
| `ssh_config`          | SSH client global config        | Outgoing connections | SSH client behavior         |
| `sshd_config`         | SSH server global config        | Incoming connections | SSH server behavior         |
| `ssh_config.d/`       | Modular client configurations   | Outgoing connections | SSH client behavior         |
| `sshd_config.d/`      | Modular server configurations   | Incoming connections | SSH server behavior         |

---

## **Why Modular Directories (`*.d/`) Are Useful**
1. **Organization**: Instead of managing one large file, you can break configurations into smaller, purpose-specific files.
2. **Ease of Automation**: Tools or scripts can drop specific configuration files into these directories without editing the main file.
3. **Default and Custom Configurations**: Keep system-provided defaults and custom configurations separate.

---

## **Tips for Managing These Files**
- Always back up configuration files before making changes.
- After modifying `ssh_config` or `sshd_config`, test the changes:
  - For the client:
    ```bash
    ssh -v <hostname>
    ```
  - For the server:
    ```bash
    sudo sshd -t
    sudo systemctl restart ssh
    


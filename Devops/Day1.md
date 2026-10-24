# 🚀 100 Days of DevOps — Day 01

## 📌 Day 1: Linux User Management & SSH

Welcome to Day 1 of my **100 Days of DevOps Learning Challenge!**

Today, I started learning basic Linux concepts used in DevOps. I learned how to connect to a remote server, understand Linux user accounts, and create a user with a non-interactive shell.

My goal is to learn something new every day, practice it, and document my progress on GitHub.

---

## 🎯 Topics Learned Today

- SSH (Secure Shell)
- Username, hostname, and password
- Linux user accounts
- Shell and non-interactive shell
- Linux directories and system binaries
- Creating users with `useradd`
- Using `sudo` for administrative commands
- Verifying users with `getent`
- Understanding service accounts

---

## 1. What is SSH?

**SSH stands for Secure Shell.**

SSH is a protocol that allows us to securely connect to and manage a remote computer or server using a terminal.

For example, I started on a jump host and connected to App Server 2.

```bash
ssh steve@stapp02
```

**Command breakdown:**

- `ssh` — securely connect to a remote server.
- `steve` — the username on the remote server.
- `stapp02` — the hostname of App Server 2.

After connecting, the terminal prompt changed to:

```bash
[steve@stapp02 ~]$
```

This indicated that I was working on App Server 2.

### Why is SSH useful in DevOps?

DevOps engineers frequently use SSH to access remote servers, troubleshoot problems, deploy applications, and manage infrastructure.

---

## 2. Difference Between Username, Hostname, and Password

These three terms are important when connecting to servers.

| Term | Meaning | Example |
|---|---|---|
| Username | The account used to log in | `steve` |
| Hostname | The name of the computer or server | `stapp02` |
| Password | A secret used to authenticate the user | The assigned login password |

**Easy way to remember:**

- Username = Who are you?
- Hostname = Which server do you want to access?
- Password = How do you prove your identity?

Different servers can have different login details. Always check the provided infrastructure information rather than assuming the credentials are the same.

---

## 3. What Is a Linux User Account?

A Linux user account represents a person, service, or automated process on a Linux system.

For example:

- `steve` — an account used by a human administrator.
- `rose` — a dedicated account intended for an automated backup agent.

Creating separate accounts helps administrators control access and permissions.

### What Is a Service Account?

A service account is an account intended for a particular application or system service.

For example, a backup agent might run under a dedicated account instead of using an administrator's account.

This helps separate the application's identity and permissions from those of human users.

**Important:** Creating a service account does not automatically configure the application or grant it access to files. Those permissions and configurations must be handled separately.

---

## 4. What Is a Shell?

A **shell** is a program that allows a user to interact with Linux by entering commands.

For example, when I type:

```bash
ls
```

A shell interprets the command, and Linux lists the files in the current directory.

Some common shells and shell-related programs are:

| Path | Purpose |
|---|---|
| `/bin/bash` | A common interactive command-line shell |
| `/bin/sh` | A standard shell interface often used for scripts |
| `/sbin/nologin` | A program that prevents normal interactive login |

The shell assigned to a user is recorded in the user's account information.

---

## 5. What Does `/sbin/nologin` Mean?

Let's break down the path:

- `/` — the root of the Linux filesystem.
- `sbin` — traditionally a directory for system administration programs and utilities.
- `nologin` — a program that rejects normal interactive login sessions.

The full path is:

```bash
/sbin/nologin
```

When this is assigned as a user's shell, the account cannot normally log in and use an interactive terminal through that shell.

This is useful for accounts intended for automated services rather than human terminal sessions.

**Note:** A non-interactive shell does not automatically prevent every possible process from running under the account. The behavior depends on how the service is configured.

---

## 6. Practical Task: Create a User With a Non-Interactive Shell

### Task

Create a user named `rose` with a non-interactive shell on **App Server 2 (`stapp02`)**.

### Command

```bash
sudo useradd -s /sbin/nologin rose
```

### Command breakdown

| Part | Meaning |
|---|---|
| `sudo` | Run the command with elevated privileges, subject to authorization |
| `useradd` | Create a new Linux user account |
| `-s` | Specify the user's login shell |
| `/sbin/nologin` | Prevent normal interactive login through the assigned shell |
| `rose` | The name of the new user |

### Step-by-step process

**Step 1: Connect to App Server 2**

From the jump host, run:

```bash
ssh steve@stapp02
```

Use the correct username and hostname from the infrastructure details.

**Step 2: Create the user**

After connecting to App Server 2, run:

```bash
sudo useradd -s /sbin/nologin rose
```

Enter the password if prompted.

**Step 3: Verify the user**

Run:

```bash
getent passwd rose
```

Example output:

```text
rose:x:1002:1002::/home/rose:/sbin/nologin
```

The numeric IDs may differ. The important part for this task is that the final field is `/sbin/nologin`.

**Step 4: Verify the task**

After confirming the user has the correct shell, use the task platform's verification option.

### Important lesson

The command must contain the correct absolute path:

```bash
/sbin/nologin
```

For example, `sbin/nologin` is missing the leading `/` and is not the same path.

---

## 7. What Is the Difference Between `steve` and `rose`?

| Feature | `steve` | `rose` |
|---|---|---|
| Purpose | Account used to administer the server | Account intended for an automated backup agent |
| Shell | A normal shell, depending on configuration | `/sbin/nologin` |
| Interactive login | Normally possible, subject to authentication and restrictions | Normally prevented through the assigned shell |
| Permissions | Depends on the account's configuration | Depends on permissions granted to the account |

Creating `rose` does not start the backup agent automatically. The agent must be configured to use the account, and the account must have the appropriate permissions.

---

## 8. Questions I Asked Today

These are the questions I explored while learning the concepts.

1. **Why must the task be completed on App Server 2 only?**  
   Because the task specifies the target server. Changes should be made on the correct machine, not on the jump host or another server.

2. **What does a non-interactive shell mean?**  
   It prevents normal interactive terminal login through that shell.

3. **What does SSH mean?**  
   SSH stands for Secure Shell. It is used to securely connect to remote systems.

4. **What is the difference between username, hostname, and password?**  
   The username identifies the account, the hostname identifies the server, and the password is one possible authentication method.

5. **Why do we create separate user accounts?**  
   To give people and applications separate identities and control their access to system resources.

6. **What does `/sbin` mean?**  
   It is a traditional Linux directory for system administration programs and utilities.

7. **What is a shell?**  
   A program that interprets commands and lets a user interact with the operating system.

8. **Can a backup agent use an account without a normal interactive login?**  
   Yes, if the service is configured appropriately. A non-interactive shell does not by itself configure the service or grant permissions.

9. **Does creating a user automatically assign it work?**  
   No. Creating an account establishes the identity; applications, tasks, and permissions must be configured separately.

10. **Why did my original command fail?**  
    I used an incorrect shell path. Linux could not find the specified shell. The correct path for this task is `/sbin/nologin`.

---

## 9. Commands Learned Today

| Command | Purpose |
|---|---|
| `ssh steve@stapp02` | Connect to App Server 2 |
| `sudo useradd -s /sbin/nologin rose` | Create `rose` with a non-interactive shell |
| `getent passwd rose` | Display the account information for `rose` |
| `ls` | List files and directories |
| `pwd` | Display the current working directory |

---

## 10. Key Takeaways

Today, I learned that:

- SSH is used to connect securely to remote servers.
- A username identifies an account, while a hostname identifies a server.
- Linux supports separate accounts for people and automated services.
- A shell determines how a user can interact with the system.
- `/sbin/nologin` prevents normal interactive login through the assigned shell.
- `sudo` is used to execute commands with elevated privileges.
- `useradd` creates a user, and `getent passwd` helps verify account information.
- Commands must be executed on the correct server.
- Creating an account does not automatically configure a service or grant permissions.

### Today's Progress

- [x] Learned basic SSH usage.
- [x] Understood username, hostname, and password.
- [x] Learned about Linux users and shells.
- [x] Studied the purpose of a non-interactive shell.
- [x] Practiced the command for creating a service account.
- [x] Learned how to verify user account information.

---

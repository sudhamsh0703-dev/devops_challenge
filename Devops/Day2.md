# Day 02 — Linux User Management: Account Expiry Date

## 🎯 Today's Task

Create a temporary user account named `rose` on **App Server 1 (`stapp01`)** in the Stratos Datacenter and set its expiry date to **December 7, 2026**.

## 🧠 What I Learned Today

### 1. What Is a Temporary User Account?

A temporary user account is intended to be used for a limited period. For example, a developer may need access to a server only while working on a temporary project assignment.

Linux allows administrators to set an account expiry date so the account becomes invalid for normal authentication after that date.

### 2. What Is an Account Expiry Date?

An account expiry date determines when a user account expires.

For this task, the required expiry date is:

`2026-12-07`

The date format is `YYYY-MM-DD`:

- `2026` — Year
- `12` — Month (December)
- `07` — Day

**Important:** Expiring an account does not automatically delete the user or their files. The account can remain on the server even after it expires.

### 3. What Is App Server 1 (`stapp01`)?

`stapp01` is the hostname of App Server 1.

The task requires creating `rose` on `stapp01`, not on App Server 2 (`stapp02`). Always check the target server before running administrative commands.

## 🛠️ Commands Used

### Step 1: Connect to App Server 1

From the jump host, connect using the SSH username provided in the lab's server details:

```bash
ssh <username>@stapp01
```

Replace `<username>` with the actual username provided by the lab.

### Step 2: Create the User With an Expiry Date

```bash
sudo useradd -e 2026-12-07 rose
```

**Command breakdown:**

- `sudo` — Runs the command with administrative privileges.
- `useradd` — Creates a new Linux user.
- `-e` — Specifies the account expiry date.
- `2026-12-07` — The required expiry date.
- `rose` — The username, written in lowercase.

### Step 3: Verify the Expiry Date

```bash
sudo chage -l rose
```

This command displays password-aging and account-expiry information for the user `rose`.

**Command breakdown:**

| Part | Meaning |
|---|---|
| `sudo` | Runs the command with administrative privileges. |
| `chage` | Displays or manages password-aging and account-expiry settings. |
| `-l` | Means **list**; displays the current settings. |
| `rose` | The username whose settings we want to check. |

Look for a line similar to:

```text
Account expires : Dec 07, 2026
```

The exact formatting may vary depending on the Linux system.

**Important:** `chage -l` only displays the settings. It does not change the expiry date.

## 📝 Understanding Markdown Tables

Markdown tables organize information into rows and columns in a README file.

Example:

```markdown
| Item | Command |
|---|---|
| Verify account expiry | `sudo chage -l rose` |
```

It appears like this:

| Item | Command |
|---|---|
| Verify account expiry | `sudo chage -l rose` |

**Markdown symbols explained:**

- `|` — Separates columns.
- `---` — Separates the header row from the table content.
- Backticks (`` ` ``) — Format commands or other text as code.

A table needs a header row, a separator row, and one or more content rows to display useful information.

## ❓ Questions and Concepts

**Q1. What does `-e` do in `useradd`?**

It sets the date when the account expires.

**Q2. Does an expired account get deleted automatically?**

No. The account and its files can remain on the server. Expiration restricts normal account authentication; it does not delete the account.

**Q3. Why must I use `stapp01`?**

Because the task specifically requires the user to be created on App Server 1. Creating the user on another server would not satisfy the task.

**Q4. How can I check whether the expiry date was set correctly?**

Run `sudo chage -l rose` and check the `Account expires` field.

**Q5. What does `-l` mean in `chage -l rose`?**

It means **list**. It displays the user's current password-aging and account-expiry information without changing it.

**Q6. Why do we use Markdown tables in a README?**

Tables make information easier to read by organizing related details, such as commands and their purposes, into columns.

## ✅ Today's Key Takeaways

- Learned how to create a Linux user with an expiry date.
- Learned that `useradd -e` sets the account expiry date.
- Practiced verifying account expiry information with `chage -l`.
- Learned the difference between expiring an account and deleting it.
- Learned how Markdown table symbols work.
- Learned to confirm the target server before performing administrative tasks.

## 📌 Day 2 Task Summary

| Item | Value |
|---|---|
| Server | App Server 1 (`stapp01`) |
| Username | `rose` |
| Expiry date | `2026-12-07` |
| Creation command | `sudo useradd -e 2026-12-07 rose` |
| Verification command | `sudo chage -l rose` |

**Status:** Mark complete after verifying the expiry date and passing the lab's task check.

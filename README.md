# 🐧 Linux Account Management Lab

In this lab, I explored **user and group management** on a Linux system. The lab involved identifying account types, inspecting UID/GID, managing sudo privileges, and creating new users and groups.

---

## 📋 Lab Overview

**Goal:**

* Identify types of user accounts
* Inspect user IDs (UID) and group memberships
* View sudo access
* Examine access control files for passwords
* Create new users and groups
* Assign custom UID/GID and login shells

**Learning Outcomes:**

* Use `id` to check user UID and GID
* View sudo privileges via `/etc/sudoers`
* Inspect `/etc/shadow` for encrypted passwords
* List user information via `/etc/passwd`
* Check group membership via `/etc/group`
* Add users (`useradd`) and groups (`groupadd`) with custom IDs and shells
* Set user passwords securely

---

## 🛠 Step-by-Step Journey

### Step 1: Identify Account Type

* Determine the type of account for a user (e.g., Bob):

```bash
id bob
```

* **Output example:** `uid=1000(bob) gid=1000(bob) groups=1000(bob),27(sudo)`
* **Account type:** Standard user account

---

### Step 2: Check sudo Access

* View sudo privileges:

```bash
sudo cat /etc/sudoers
```

* Check if the user has root permissions:

```
bob ALL=(ALL:ALL) ALL
```

💡 **Tip:** Membership in the `admin` or `sudo` group grants root privileges.

---

### Step 3: Inspect Access Control Files

* Encrypted passwords are stored in:

```bash
sudo cat /etc/shadow
```

* User account details, full name, and default shell:

```bash
cat /etc/passwd | grep chris
```

* Example output: `chris:x:1001:1001:Chris Hunter:/home/chris:/bin/bash`

* Check group memberships:

```bash
sudo grep -i chris /etc/group
```

* Example output: `chris:x:1001:chris,sapphire`

---

### Step 4: Create a New User

* Create user **Sarah** and set password:

```bash
sudo useradd sarah
sudo passwd sarah
```

* Password set to `calisthenol321` (for lab purposes).

---

### Step 5: Create a New Group

* Create a group **John** with custom GID:

```bash
sudo groupadd -g 1010 john
```

---

### Step 6: Create a User with Specific UID, Primary Group, and Login Shell

* Create user **John** with UID `1010`, primary group `John`, and login shell `/bin/sh`:

```bash
sudo useradd -u 1010 -g john -s /bin/sh john
```

* Verify:

```bash
id john
```

* Example output: `uid=1010(john) gid=1010(john) groups=1010(john)`

---

## ✅ Key Commands Summary

| Task                            | Command / Notes                                          |
| ------------------------------- | -------------------------------------------------------- |
| Check user UID & GID            | `id <username>`                                          |
| View sudo privileges            | `sudo cat /etc/sudoers`                                  |
| Check encrypted passwords       | `sudo cat /etc/shadow`                                   |
| View user info                  | `cat /etc/passwd`                                        |
| List group memberships          | `sudo grep -i <username> /etc/group`                     |
| Add new user                    | `sudo useradd <username>`                                |
| Set user password               | `sudo passwd <username>`                                 |
| Add new group                   | `sudo groupadd -g <GID> <groupname>`                     |
| Add user with UID, group, shell | `sudo useradd -u <UID> -g <group> -s /bin/sh <username>` |

---

## 💡 Notes / Tips

* Always use `sudo` for commands requiring root privileges.
* The **shadow file** stores hashed passwords; do not edit directly.
* Use `/etc/passwd` and `/etc/group` for reference and verification.
* Custom UID/GID ensures no conflicts with existing users/groups.
* Assigning a specific shell (e.g., `/bin/sh`) sets the default login environment.

---

## 📌 Lab Summary

| Step                  | Status | Key Takeaways                                 |
| --------------------- | ------ | --------------------------------------------- |
| Identify account type | ✅      | Bob is a standard user                        |
| Check sudo access     | ✅      | Bob can gain root privileges                  |
| Inspect `/etc/shadow` | ✅      | Encrypted passwords located here              |
| View user info        | ✅      | Chris Hunter identified with default shell    |
| List group membership | ✅      | Chris in groups `chris, sapphire`             |
| Create new user Sarah | ✅      | Password set successfully                     |
| Create new group John | ✅      | GID 1010 assigned                             |
| Create new user John  | ✅      | UID 1010, primary group John, shell `/bin/sh` |

---

## ✅ References

* [Linux `useradd` man page](https://man7.org/linux/man-pages/man8/useradd.8.html)
* [Linux `/etc/passwd` file](https://man7.org/linux/man-pages/man5/passwd.5.html)
* [Linux `/etc/group` file](https://man7.org/linux/man-pages/man5/group.5.html)
* [Linux sudoers configuration](https://man7.org/linux/man-pages/man5/sudoers.5.html)

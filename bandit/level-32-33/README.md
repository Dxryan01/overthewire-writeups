**Bandit Level 32 → Level 33**

**Goal**: Find the next password despite a special shell that turns any input into uppercase and, thereby preventing the use of standard commands

**Reasoning**: Since every command entered by the user is converted to uppercase, common binaries such as `cat` or `ls` become unusable. However, the shell variable `$0`, which expands to the path of the currently running shell (e.g. `/bin/sh`), is still interpreted correctly during shell expansion. Executing `$0` spawns a normal shell, allowing us to navigate the filesystem and retrieve the password.

**Solution**:
1. Connect as `bandit32` via SSH : `ssh bandit32@bandit.labs.overthewire.org -p 2220`. You get into the `uppercase shell`
2. Execute `$0` to spawn a regular shell, bypassing the uppercase restriction : `$0`
3. Verify that the new shell is running with the privileges of the `bandit33` user : `id`
4. Read the file containing `bandit33`'s password : `cat /etc/bandit_pass/bandit33`

**Lesson**: Naive input transformations are not a security mechanism. Understanding how the shell interprets variables and expands commands can reveal alternative execution paths that bypass such restrictions.

---
🔒 Password not disclosed — try it yourself on overthewire.org

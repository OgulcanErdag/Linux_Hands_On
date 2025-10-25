# Hands‑on Linux‑02 — Environment Variables (Lab)

**Purpose:**
This hands‑on lab explains Linux **environment variables**, **PATH**, **quoting**, and the **sudo/NOPASSWD** mechanism. It’s cleaned up and formatted for direct GitHub publishing.

---

## 🎯 Learning Outcomes

By completing this lab, you will be able to:

- Distinguish between **shell variables** and **environment variables**.
- Use `export`, `unset`, and `printenv` effectively.
- Modify the `PATH` variable to execute scripts globally.
- Understand **quoting** (`' '` vs `" ")` and variable interpolation.
- Recognize how `sudo` permissions and `NOPASSWD` operate.

---

## 🧩 Part 1 — Shell vs Environment Variables

### 🔹 Key Concepts

- **Shell variables** live only in the current shell.
- **Environment variables** propagate to child processes.

### ✅ Valid Names

Letters, digits, and underscores; must start with a letter or underscore.

```bash
KEY=value
_VAR=5
LINUX_way=test
```

### ❌ Invalid Names

```bash
3_KEY=value   # starts with digit
-VAR=5        # hyphen not allowed
LINUX-way=foo # hyphen not allowed
KEY?1=value   # invalid symbol
```

### 🧠 Commands

```bash
# list environment variables
printenv
env

# list all (env + shell + functions)
set

# create and export
echo "--- Shell variable ---"
MYVAR=hello
export MYVAR

# or shorter
export OTHER=world

# remove variable
unset MYVAR
```

### 🔍 Test — Exported vs Non‑Exported

```bash
MYKEY=local
export MYKEY1=exported
cat > showvars.sh <<'EOF'
#!/bin/bash
echo "MYKEY=$MYKEY"
echo "MYKEY1=$MYKEY1"
EOF
chmod +x showvars.sh
./showvars.sh   # prints only MYKEY1 (exported)
```

---

## ⚙️ Part 2 — PATH Variable & Script Execution

### 🔹 Concept

`PATH` defines where the shell looks for executables.

```bash
mkdir -p ~/lab/test
cat > ~/lab/test/test.sh <<'EOF'
#!/bin/bash
echo "Hello World"
EOF
chmod +x ~/lab/test/test.sh

# from home — will fail
test.sh            # command not found

# works with explicit path
./lab/test/test.sh

# temporarily extend PATH
export PATH="$PATH:$HOME/lab/test"
printenv PATH

# now works from anywhere
test.sh
```

To make it **permanent**:

```bash
echo 'export PATH="$PATH:$HOME/lab/test"' >> ~/.bashrc
source ~/.bashrc
```

### 🔍 Environment variable inside a script

```bash
cd ~/lab/test
export LINUX="env.var"
WAY="shell.var"
cat > test1.sh <<'EOF'
#!/bin/bash
echo "LINUX from env: $LINUX"
echo "WAY (shell-only): $WAY"
EOF
chmod +x test1.sh
./test1.sh
# LINUX visible ✅  WAY empty ❌
```

---

## 🗨️ Part 3 — Quoting & Variables

### 🔸 Double Quotes — interpolation

```bash
MYNAME=james
MYVAR="hello $MYNAME"
echo "$MYVAR"   # hello james
MYVAR="hello \$MYNAME"
echo "$MYVAR"   # prints literal $MYNAME
```

### 🔸 Single Quotes — literal text

```bash
echo '$SHELL'   # prints $SHELL literally
echo 'My\$SHELL'
```

💡 **Tip:** Always quote variables with potential spaces: `echo "$FILEPATH"`.

---

## 🔐 Part 4 — Sudo & NOPASSWD

### 🔹 Behavior Overview

- `sudo <cmd>` → authenticates the **current user’s** password.
- `su -` → asks for **root password**.
- On AWS EC2 and most cloud images, default users (`ec2-user`, `ubuntu`) have **NOPASSWD** sudo rights for automation.

### 🔍 Inspect Current Configuration

```bash
sudo grep -RIn "NOPASSWD" /etc/sudoers /etc/sudoers.d 2>/dev/null || true
sudo -l   # show your sudo rights
```

If you see something like:

```
ec2-user ALL=(ALL) NOPASSWD:ALL
```

→ passwordless sudo is enabled.

### ⚠️ Safe Editing

Always use `visudo` or `visudo -f /etc/sudoers.d/filename` to edit sudoers. Direct editing can break access.

Example:

```bash
sudo visudo -f /etc/sudoers.d/90-cloud-init-users
```

Change:

```
ec2-user ALL=(ALL) NOPASSWD:ALL
```

➡️ to:

```
ec2-user ALL=(ALL) ALL
```

Then assign a password if needed:

```bash
sudo passwd ec2-user
```

---

## 🧭 Exercises

1. Create a script printing one exported and one non‑exported variable.
   → Only the exported one should appear.
2. Add a `~/lab/bin` directory to PATH permanently and run a script from anywhere.
3. Demonstrate double vs single quotes using a variable with spaces.
4. Locate all `NOPASSWD` lines and describe their purpose.

---

## 🧩 Quick Solutions

```bash
# 1
export A=1; B=2
cat > test.sh <<'EOF'
#!/bin/bash
echo A=$A
 echo B=$B
EOF
chmod +x test.sh
./test.sh   # only A visible

# 2
mkdir -p ~/lab/bin
echo -e '#!/bin/bash\necho hi' > ~/lab/bin/hi
chmod +x ~/lab/bin/hi
echo 'export PATH="$PATH:$HOME/lab/bin"' >> ~/.bashrc
source ~/.bashrc
hi

# 3
X="a b"
echo "$X"   # a b
echo '$X'    # literal $X

# 4
sudo grep -RIn "NOPASSWD" /etc/sudoers /etc/sudoers.d
```

---

## Notes

- Updated `yum` → `dnf` for modern systems (Amazon Linux 2023).
- Fixed incorrect `env HOME` example.
- Added shebangs to all script examples.
- Added safe `.bashrc` PATH persistence.
- Clarified `sudo` vs `su` password logic and NOPASSWD meaning.

---

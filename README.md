# The Bash Shell – AWS Linux Lab

## Overview

This project documents a hands-on Bash shell lab performed on an Amazon Linux EC2 instance in an AWS Academy / Vocareum environment.

The lab covers Bash aliases, directory backups with `tar`, and the Linux `PATH` environment variable.

## Objectives

- Connect to an Amazon Linux EC2 instance using SSH.
- Create a reusable Bash alias for directory backups.
- Create and inspect a compressed `.tar.gz` archive.
- Understand how Bash searches for executable commands using `PATH`.
- Add a custom directory to `PATH` and execute a script by its command name.

## Environment

| Component | Details |
|---|---|
| Cloud platform | Amazon Web Services |
| Compute | Amazon EC2 |
| Operating system | Amazon Linux |
| User | `ec2-user` |
| Remote access | SSH |
| Shell | Bash |
| Archive utility | `tar` |

## Task 1 – Connect to EC2

Connect to the lab instance using SSH and the provided lab credentials. On Windows, PuTTY can use the supplied `.ppk` key.

Verify the session:

```bash
whoami
pwd
```

Expected user: `ec2-user`  
Expected home directory: `/home/ec2-user`

## Task 2 – Create a backup alias

Create an alias that invokes `tar` with gzip compression and verbose output:

```bash
alias backup='tar -cvzf '
```

Back up the `CompanyA` directory:

```bash
cd /home/ec2-user
backup backup_companyA.tar.gz CompanyA
```

Verify the archive:

```bash
ls -lh backup_companyA.tar.gz
tar -tzvf backup_companyA.tar.gz
```

### tar options

| Option | Purpose |
|---|---|
| `-c` | Create an archive |
| `-v` | Verbose output; list archived files |
| `-z` | Compress with gzip |
| `-f` | Use the following argument as the archive filename |

The alias is temporary and lasts only for the current shell session. To make it available in future Bash sessions, add it to `~/.bashrc`:

```bash
echo "alias backup='tar -cvzf '" >> ~/.bashrc
source ~/.bashrc
```

## Task 3 – Explore and update PATH

Move into the directory containing the script:

```bash
cd /home/ec2-user/CompanyA/bin
./hello.sh
```

Expected output:

```text
hello ec2-user
```

Move to the parent directory and run the script using a relative path:

```bash
cd ..
./bin/hello.sh
```

Try running it by command name:

```bash
hello.sh
```

Before the directory is added to `PATH`, Bash will normally report `command not found`, because it does not search the current directory automatically.

Display the current search path:

```bash
echo "$PATH"
```

Append the script directory for the current shell session:

```bash
PATH="$PATH:/home/ec2-user/CompanyA/bin"
export PATH
```

Now run:

```bash
hello.sh
which hello.sh
```

Expected script output:

```text
hello ec2-user
```

Expected location:

```text
/home/ec2-user/CompanyA/bin/hello.sh
```

To make the PATH change persistent for future Bash sessions:

```bash
echo 'export PATH="$PATH:/home/ec2-user/CompanyA/bin"' >> ~/.bashrc
source ~/.bashrc
```

> **Note:** The lab's original PATH assignment changes only the current shell. The `~/.bashrc` configuration above makes the change persistent for interactive Bash sessions. Ensure the directory exists and the script has execute permission.

## Key learnings

- Bash aliases provide shorter names for frequently used commands.
- `tar` can archive and gzip-compress directories.
- Linux uses the directories in `PATH` to locate commands.
- Relative paths and command lookup through `PATH` are different execution methods.
- Shell configuration files such as `~/.bashrc` can persist aliases and environment-variable settings.

## Practical relevance

These skills are useful in Linux administration, cloud operations, infrastructure support, troubleshooting, and basic automation.

## Lab validation checklist

- [ ] Connected to the EC2 instance using SSH.
- [ ] Verified the `ec2-user` account.
- [ ] Created the `backup` alias.
- [ ] Created and inspected `backup_companyA.tar.gz`.
- [ ] Ran `hello.sh` using relative paths.
- [ ] Identified why command-name execution initially failed.
- [ ] Added the script directory to `PATH`.
- [ ] Ran `hello.sh` by command name.

Only mark the checklist complete after performing and verifying each step in the lab environment.

## Author

Indrajit Wadgave

GitHub: https://github.com/Indrajit27

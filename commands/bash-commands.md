# Bash Commands – The Bash Shell Lab

## 1. Connect and verify

```bash
whoami
pwd
cd /home/ec2-user
```

## 2. Create and use the backup alias

```bash
alias backup='tar -cvzf '
alias backup
backup backup_companyA.tar.gz CompanyA
```

## 3. Verify the archive

```bash
ls -lh backup_companyA.tar.gz
tar -tzvf backup_companyA.tar.gz
```

## 4. Run the script using paths

```bash
cd /home/ec2-user/CompanyA/bin
./hello.sh
cd ..
./bin/hello.sh
hello.sh
```

The last command is expected to fail before the script directory is added to `PATH`.

## 5. Inspect and update PATH

```bash
echo "$PATH"
PATH="$PATH:/home/ec2-user/CompanyA/bin"
export PATH
hello.sh
which hello.sh
```

## 6. Persist alias and PATH settings

Run these commands only if you want the settings to remain available in future interactive Bash sessions:

```bash
echo "alias backup='tar -cvzf '" >> ~/.bashrc
echo 'export PATH="$PATH:/home/ec2-user/CompanyA/bin"' >> ~/.bashrc
source ~/.bashrc
```

Avoid appending the same lines repeatedly; duplicate entries can accumulate in `~/.bashrc`.

## Command reference

| Command | Purpose |
|---|---|
| `pwd` | Print current working directory |
| `whoami` | Display current user |
| `alias` | Define or display shell aliases |
| `tar -cvzf` | Create a gzip-compressed archive with verbose output |
| `ls -lh` | List files with human-readable sizes |
| `tar -tzvf` | List archive contents |
| `echo "$PATH"` | Display command search directories |
| `export PATH=...` | Export the updated PATH to child processes |
| `which hello.sh` | Show the executable found through PATH |
| `source ~/.bashrc` | Reload Bash configuration in the current shell |

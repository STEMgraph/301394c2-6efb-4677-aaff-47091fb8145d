<!---
{
  "id": "301394c2-6efb-4677-aaff-47091fb8145d",
  "teaches": "Secure File Transfer with SCP",
  "depends_on": ["8c79cd1f-f6bd-4930-b62c-b2970c412735"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-04-13",
  "keywords": ["scp", "ssh", "file transfer", "linux", "remote access"]
}
--->

# Secure File Transfer with SCP

> In this exercise you will learn how to use the `scp` command to securely transfer files between local and remote machines using SSH. Furthermore we will explore how to use SCP in combination with SSH keys and configuration files to streamline your workflows.

## Introduction

The `scp` (secure copy) command is a tool used to copy files and directories securely between hosts on a network. It leverages SSH (Secure Shell) for data transfer and authentication, ensuring that the transmitted data is encrypted and secure from eavesdropping or tampering. If you're already familiar with SSH — as covered in the [SSH Basics exercise](https://github.com/STEMgraph/8c79cd1f-f6bd-4930-b62c-b2970c412735) — you're well prepared to delve into SCP.

SCP is a command-line utility available on most Unix-like systems. Its basic syntax is simple but highly flexible:

```bash
scp [options] source target
```

Both source and target can be either local files or remote hosts specified in the format `user@hostname:path`. The command uses the same SSH authentication mechanisms, which means if you've set up asymmetric keys (as in [this tutorial](https://github.com/STEMgraph/b9e0a0a7-cce1-4d14-ae1c-5f8f57472c46)) or configured your `.ssh/config` file (see [this tutorial](https://github.com/STEMgraph/75f53c25-f20f-4dfd-b5c4-9251c83d64be)), your `scp` usage can be significantly more convenient.

Understanding how to use `scp` not only makes it easier to manage remote systems, but also enhances your toolkit for automated scripts and remote administration tasks. This exercise will guide you through several real-world scenarios for using `scp`, from copying a single file to synchronizing directory trees.

### Further Readings and Other Sources

- [scp man page (Linux)](https://man7.org/linux/man-pages/man1/scp.1.html)
- [OpenSSH documentation](https://www.openssh.com/manual.html)
- [DigitalOcean - How to Use SCP Command](https://www.digitalocean.com/community/tutorials/how-to-use-scp-command-to-securely-transfer-files)

## Tasks

### Task 1: Copy a Local File to a Remote Server

**Step 1:** Create a test file on your local machine:
```bash
echo "Hello from local machine" > testfile.txt
```

**Step 2:** Copy it to your home directory on the remote server:
```bash
scp testfile.txt username@remotehost:~
```
Replace `username` and `remotehost` with appropriate values.

**Step 3:** Log in using SSH and verify:
```bash
ssh username@remotehost
cat ~/testfile.txt
```
You should see the content of the file.

### Task 2: Copy a File from a Remote Server to Your Local Machine

**Step 1:** Still on the remote server, create another test file:
```bash
echo "Hello from remote server" > remotefile.txt
```

**Step 2:** From your local machine, copy it back:
```bash
scp username@remotehost:~/remotefile.txt .
```

**Step 3:** Check if it exists locally:
```bash
cat remotefile.txt
```

### Task 3: Copy a Directory Recursively

**Step 1:** Create a directory structure:
```bash
mkdir -p mydir/subdir
echo "Inside subdir" > mydir/subdir/file.txt
```

**Step 2:** Copy it recursively to the remote host:
```bash
scp -r mydir username@remotehost:~/
```

**Step 3:** SSH into the remote and verify the contents:
```bash
ssh username@remotehost
ls ~/mydir/subdir
cat ~/mydir/subdir/file.txt
```

### Task 4: Use `.ssh/config` to Simplify SCP

If you completed the `.ssh/config` tutorial, define a shortcut like:
```bash
Host myserver
  HostName remotehost
  User username
  IdentityFile ~/.ssh/id_rsa
```
Then use:
```bash
scp testfile.txt myserver:~
```
This avoids typing the full username and hostname every time.

## Questions

1. What are the security benefits of using `scp` over plain `ftp` or `telnet`?
2. How does `scp` use SSH under the hood?
3. What is the effect of the `-r` option?
4. Why might someone prefer using `.ssh/config` or SSH keys when using `scp`?
5. Can `scp` be used to transfer files between two remote hosts? If so, how?

## Advice

Don’t be discouraged if `scp` seems terse or cryptic at first. Like many Unix tools, its power lies in its simplicity and composability. If you find yourself typing the same commands repeatedly, consider setting up a `.ssh/config` file or SSH keys to streamline your access. Reviewing the SSH fundamentals [here](https://github.com/STEMgraph/8c79cd1f-f6bd-4930-b62c-b2970c412735) can reinforce your understanding, and working through the tutorials on [asymmetric keys](https://github.com/STEMgraph/b9e0a0a7-cce1-4d14-ae1c-5f8f57472c46) and [SSH configs](https://github.com/STEMgraph/75f53c25-f20f-4dfd-b5c4-9251c83d64be) will make your SCP usage much more efficient. Keep experimenting — every command you master adds to your superpowers as a developer or admin!


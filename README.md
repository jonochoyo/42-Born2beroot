# Born2beroot

## Summary

This project aims to introduce us to the wonderful world of virtualization.  
We will create our first machine in VirtualBox (or UTM if we can’t use VirtualBox) under specific instructions.  
Then, at the end of this project, we will be able to set up an operating system while implementing strict rules.

## General guidelines

- The use of VirtualBox is mandatory.  
- We only have to turn in a [signature.txt](signature.txt) file at the root of the repository. We must paste in it the signature of our machine’s virtual disk.

## Mandatory Part

- We must choose as an operating system either the latest stable version of Debian or Rocky.
- We must create at least 2 encrypted partitions using LVM.
- A SSH service will be running on port 4242 only. For security reasons, it must not be possible to connect using SSH as root.
- We have to configure the operating system with the UFW (or firewalld for Rocky) firewall and thus leave only port 4242 open.
- The hostname of the virtual machine must be our login ending with 42.
- We have to install and configure sudo following strict rules.
- In addition to the root user, a user with our login as username has to be present and belong to the *user42* and *sudo* groups.
- Password policy details:
  - Expires every 30 days.
  - Minimum of 2 days before the user can change it.
  - Warning message is sent 7 days before the expiry date.
  - Must be at least 10 characters long. It must contain an uppercase letter, a lowercase letter, and a number. No more than 3 consecutive identical characters are allowed.
  - The password must not include the name of the user.
  - The password must have at least 7 characters that are not part of the former password. (This doesn't apply to root)
  - The root password has to comply with the policy.
- Sudo group configuration:
  - Authentication using sudo has to be limited to 3 attempts in the event of an incorrect password.
  - A custom message has to be displayed if an error due to a wrong password occurs when using sudo.
  - Each action using sudo has to be archived, both inputs and outputs. The log file has to be saved in the */var/log/sudo/* folder.
  - The TTY mode has to be enabled for security reasons.
  - The paths that can be used by sudo must be restricted. Example: */usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin*
- We have to create a simple bash script called [monitoring.sh](monitoring.sh). At server startup, the script will display the following information on all terminals every 10 minutes:
  - The architecture of the operating system and its kernel version.
  - The number of physical processors.
  - The number of virtual processors.
  - The current available RAM on the server and its utilization rate as a percentage.
  - The current available memory on the server and its utilization rate as a percentage.
  - The current utilization rate of the processors as a percentage.
  - The date and time of the last reboot.
  - Whether LVM is active or not.
  - The number of active connections.
  - The number of users using the server.
  - The IPv4 address of the server and its MAC (Media Access Control) address.
  - The number of commands executed with the sudo program.

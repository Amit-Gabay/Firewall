# Description

A stateful Linux firewall based on kernel module. consists of firewall kernel module aside to 3 userspace proxy servers (FTP, HTTP, SMTP).
In addition, I've implemented an IPS (Intrusion Prevetion System) for HTTP traffic as an protection to the Pie-Reigster 3.7.1.4 RCE vulnerability.
The firewall includes a DLP system (Data Leak Prevention) for HTTP / SMTP traffic, in order to detect and prevent leakage of C source code.


## Idea

Kernel side-    Added a few modifications in order to intercept SMTP traffic into the SMTP proxy.

Userspace side- In the userspace side, I've added a proxy server at "smtp/smtp_proxy.py", with a DLP (Data Leak Prevention) system;
		Added a DLP & IPS systems to the HTTP proxy also.


## Usage

inside the "module" directory, open terminal and execute the following commands:
```
$ make						/* Compile the kernel module files with certain flags */
$ insmod firewall.ko				/* Install the firewall module in the kernel */
$ cd ../user/					/* Change directory to user */
$ make						/* Compile the userspace files with certain flags */
$ ./firewall_control load_rules rules.txt	/* In order to load rules.txt as rules table to the firewall */

In a new terminal (Inside the project directory):
$ cd ./http
$ sudo python http_proxy.py			/* In order to run the HTTP proxy server */

In another new terminal (Inside the project directory):
$ cd ./smtp
$ sudo python smtp_proxy.py			/* In order to run the SMTP proxy server */

$ rmmod firewall				/* Remove the firewall module from the kernel */
```

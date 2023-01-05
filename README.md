Redirect connections from different ports at one ipv4 address to unique random ipv6 address from \64 subnetwork. Based on 3proxy

![cover](cover.svg)

## Requirements
- Centos 8
- Ipv6 \64

## Installation
VPS from [Vultr *100$ free*](https://www.vultr.com/?ref=8809561) used as Centos setup

1. `bash <(curl -s "https://raw.githubusercontent.com/thuongtin/ipv4-ipv6-proxy/master/scripts/vultrcentos8.sh")`

1. After installation dowload the file `proxy.zip`
   * File structure: `IP4:PORT:LOGIN:PASS`
   * You can use this online [util](http://buyproxies.org/panel/format.php
) to change proxy format as you like

## Test your proxy

Install [FoxyProxy](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/) in Firefox
![Foxy](foxyproxy.png)

Open [ipv6-test.com](http://ipv6-test.com/) and check your connection
![check ip](check_ip.png)
--------------------------------------------------
https://www.thegeekdiary.com/how-to-enable-ipv6-on-centos-rhel-7/
enable ipv6 centos
How to enable IPv6 on CentOS / RHEL 7
by admin


IPv6 is enabled by default on RHEL / CenOS 7 systems. So, if IPv6 was disabled on the system intentionally, it can be re-enabled by the following either of the methods described below.
1. Enabling IPv6 in kernel module (requires reboot)
2. Enabling IPv6 using sysctl settings (no reboot required)

Enabling IPv6 in kernel module (requires reboot)
1. Edit /etc/default/grub and change the value of kernel parameter ipv6.disable from 1 to 0 in line GRUB_CMDLINE_LINUX, e.g.:

# cat /etc/default/grub
GRUB_TIMEOUT=5
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="ipv6.disable=0 crashkernel=auto rhgb quiet"
GRUB_DISABLE_RECOVERY="true"
Note: ipv6.disable=0 is the default value, so you can simply remove this argument ipv6.disable from GRUB_CMDLINE_LINUX argument list if you want.
2. Regenerate a GRUB configuration file and overwrite existing one using the command shown below.


# grub2-mkconfig -o /boot/grub2/grub.cfg
3. Restart system for the changes to take effect.

# shutdown -r now
Enabling IPv6 using sysctl settings (no reboot required)
In addition, even if the ipv6 kernel module is loaded, it could also be disabled by using sysctl settings.

1. In order to get ipv6 running online, please make sure below lines in /etc/sysctl.conf are commented out or removed.

# cat /etc/sysctl.conf | grep ipv6
# net.ipv6.conf.all.disable_ipv6 = 1     ### either comment/remove this line or change its value from 1 to 0
# net.ipv6.conf.default.disable_ipv6 = 1 ### either comment/remove this line or change its value from 1 to 0
2. Use the command ‘sysctl -p’ to re-read the configuration file /etc/sysctl.conf.

# sysctl -p
More about using sysctl settings
1. To dynamically disable ipv6 on an interface, use commands given below.

# sysctl net.ipv6.conf.[interface].disable_ipv6 = 1       ### put interface name here [interface], i.e. eth0
# sysctl net.ipv6.conf.default.disable_ipv6 = 1
2. To dynamically enable ipv6 on an interface, use the commands given below.

# sysctl net.ipv6.conf.[interface].disable_ipv6 = 0       ### put interface name here [interface], i.e, eth0
# sysctl net.ipv6.conf.default.disable_ipv6 = 0
3. To dynamically enable ipv6 on all interfaces, use the commands given below.

# sysctl net.ipv6.conf.all.disable_ipv6 = 0
# sysctl net.ipv6.conf.default.disable_ipv6 = 0
4. To dynamically disable ipv6 on all interfaces, use the commands given below.

# sysctl net.ipv6.conf.all.disable_ipv6 = 1
# sysctl net.ipv6.conf.default.disable_ipv6 = 1
Verify
To verify if IPv6 is enabled or not, execute :

# ifconfig -a | grep inet6
        inet6 fe80::211:aff:fe6a:9de4  prefixlen 64  scopeid 0x20
        inet6 ::1  prefixlen 128  scopeid 0x10[host]
As shown in the output above, IPv6 is enabled.

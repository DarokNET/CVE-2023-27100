# [CVE-2023-27100 - pfSense Anti-brute force protection bypass]

# Problem Description

The authentication system attempts to be informative and print extra information along with IP addresses to completely identify where a user logs in from when they login using the GUI. This includes the authentication source (e.g. local database, LDAP or RADIUS, authentication server name), plus contents of proxy headers X-Forwarded-For and Client-IP to further clarify the exact user location.

This extra information is printed after the IP address of the remote user in various places, including log messages for authentication. In the case of GUI login failures, the log entries included the contents of the proxy headers (X-Forwarded-For or Client-IP) submitted by the client.

This extra information confused the sshguard authentication log parser which made it fail to recognize the client IP address in authentication error messages.

# Impacted pfSense versions
- pfSense Plus software versions <= 22.05.1
- pfSense CE software versions <= 2.6.0

# Exploit

pfSense (see related versions above) is vulnerable to a bypass of the anti-brute force mechanism that is in place to block users that have reached the bad authentication limit. The code available in this repository ease this vulnerability exploit using the "X-Forwarded-For" header and the "anti-csrf" token.

# Links

Netgate Security Advisory : https://docs.netgate.com/downloads/pfSense-SA-23_05.sshguard.asc

Netgate associated Redmine ticket : https://redmine.pfsense.org/issues/13574

Patch : https://redmine.pfsense.org/projects/pfsense/repository/1/revisions/9633ec324eada0b870962d3682d264be577edc66

CVE : https://nvd.nist.gov/vuln/detail/CVE-2023-27100

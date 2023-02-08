### Recon-ng commands

1. Create workspace
~~~ ~~~
workspaces create target
~~~

2. Add domain name
~~~ ~~~
db insert domains
~~~
3. Add company name
~~~ ~~~
db insert companies
~~~
4. Modules 
~~~ ~~~
modules load recon/domains-hosts/brute_hosts
~~~
~~~ ~~~
modules load recon/domains-hosts/certificate_transparency
~~~
~~~ ~~~
modules load recon/domains-hosts/hackertarget
~~~
~~~ ~~~
modules load recon/domains-hosts/mx_spf_ip
~~~
~~~ ~~~
modules load recon/domains-hosts/netcraft
~~~
~~~ ~~~
modules load recon/domains-hosts/shodan_hostname
~~~
~~~ ~~~
modules load recon/domains-hosts/ssl_san
~~~
~~~ ~~~
modules load recon/domains-hosts/threatminer
~~~
~~~ ~~~
modules load recon/domains-hosts/threatcrowd
~~~
~~~ ~~~
modules load recon/hosts-ports/shodan_ip
~~~
5. Go to dashboard 
~~~ ~~~
dashboard
~~~
6. Show all hosts
~~~ ~~~
show hosts
~~~
7. Resolve hosts
~~~ ~~~
modules load recon/domains-hosts/resolve
~~~
8. Reverse resolve
~~~ ~~~
modules load recon/domains-hosts/reverse_resolve
~~~

9. Reporting
~~~ ~~~
modules search reporting
~~~
~~~ ~~~
modules load reporting/html
~~~

11. Report info
~~~ ~~~
info
~~~
12. Add Creator
~~~ ~~~
options set CREATOR raafet
~~~

13. Add customer
~~~ ~~~
options set CUSTOMER sony.com
~~~

14. Save Results
~~~ ~~~
options set FILENAME /path/sony.html
~~~
~~~ ~~~
modules load reporting/list
~~~
~~~ ~~~
options set FILENAME /path/ips.txt
~~~
~~~ ~~~
options set COLUMN host
~~~
~~~ ~~~
options set FILENAME /path/subdomains.txt
~~~

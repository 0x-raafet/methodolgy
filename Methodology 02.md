1. ###### Create Folders (subdomains, urls)
2. ###### Subdomain enumeration
~~~ ~~~
subfinder -d example.com -o subs.txt
~~~
~~~ ~~~
amass enum -passive -d example.com
~~~
~~~ ~~~
cat subs2.txt | sort | uniq | tee -a subs3.txt
~~~
 ## Passiv Recon Technique
  
1. ###### Create Folders (subdomains, ips, urls)

2. ###### [[recon-ng]]  - Recon Passively for subdomain/ips/ports

3. ###### Export lists from recon-ng and use ( httpx ) to create urls/probing (urls/ips/subdomains)

4. ###### Use ( isup.sh ) to filter Ips for only online ips 

5. ###### Use Nmap Aggressive scan & save to xml to import into Bounty platform
~~~  ~~~
nmap -il ips.txt -sSV -A -T4 -O -Pn -v  -F -oX nmap.xml
~~~
- `-sSV` Sort With Service Detection And Version Detection
- `-T4` is For speed
- `-O` Operation System information
- `-Pn` Bypass certain systems information about each device mechanism when you scan if they have firewalls
- `-F` Fast Port Scanning

6. ###### Vuln Scan
- using osmedeus 
*scanner for vulabilitues just give him list ips/subs (on vps only because is heavy)*
~~~ ~~~
osmedeus server
~~~
- Using one lineAmass powerful attack

>1. with Nuclei
~~~ ~~~
amass enum -passive -d [subdomain] -v | httpx -verbose | nuclei -t 
/root/nuclei-templates/cves/ -o result.txt
~~~
> 2. or Jaeles
~~~ ~~~
amass enum -passive -d [subdomain] -v | httpx -verbose | jaeles scan -s 'cves' 
-s 'sensitive' -s 'fuzz' -s 'common' -s 'routines' report -o /root/report.txt
~~~

7. ###### check for HeartBeat vulnability
~~~ ~~~
cat  subdomains.txt | while read line ; do echo "QUIT" | openssl s_client -connect $line:443 2>&1 | grep 'server extension "heartbeat" (id=15)' || echo $line: safe; done
~~~

8. ###### Extract Javascripts ,and Fetch Only Urls From Big Files, can also be used any type of huge data
- first use getJs to get javascripts
 ~~~ ~~~
getJs --url website.com --output /root/result.txt
 ~~~
~~~ ~~~
getJs --input urls.txt --output /root/result.txt
~~~
- Extract hidden urls from file 
    From files :
    ~~~ ~~~
    cat file | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*"*
    ~~~
    Direct from website :
    ~~~ ~~~
    curl https://website.com/file.js | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*"*
    ~~~

9. ###### ParamSpider
to hunt urls with Parameters automatically from wayback machine you can also use Arjun
~~~ ~~~
python3 paramspider.py --domain DOMAINNAME.com --exclude woff,png,svg,jpg --output params.txt
~~~

10. ###### check for domain takeover with takeover by M4llok
~~~ ~~~
takeover -l subs.txt -v -t 10
~~~

11. ###### Check for s3 buckets
~~~ ~~~
nuclei -l urls.txt -t /root/nuclei-templates/technologies/s3-detect.yaml
~~~

12. ###### pattern Check example with gf & gf-patterns:
*after you have the parameters Ghathered, we want check specific patterns and vulnrable urls
than can be attacked using Meg or other fuzzig tool*
~~~ ~~~
cat params.txt | gf xss | sed 's/FUZZ//g' >> xss_params_for_meg.txt
~~~

13. ###### Extra Sniper - webApp mode
~~~ ~~~
sniper -f /root/ips.txt -m massweb -w sony
~~~

14. ###### use Meg injection attack
we must remove 'FUZZ' from parameter and replace it with null character
~~~ ~~~
sed 's/FUZZ//g' file.txt
~~~
~~~ ~~~
meg -v worldlist.txt /root/urls.txt /root/result.txt -s 200
~~~

15. ###### JSSanner (if not using getJs)

*Scanning javascripts files for Endpoints, secrets, IDOR, Openredirect, crednetials*

- paste urls into alive.txt 
- run script alive.txt  
- use tree command, cat into subdirectories
~~~ ~~~
cat * */*.txt
~~~
~~~ ~~~
cat */*.js | gf api-keys
~~~
~~~ ~~~
cat /*/*.txt | gf ssrf > ssrf.txt
~~~

*Or other method with Gitleak*
- scan a Directory with javascripts, files, json, etc.. for secrets:
~~~ ~~~
gitleaks --path=/directory -v --no-git
~~~

- scan a file with any extenction for secrets:
~~~ ~~~
gitleaks --path=/file.xxx -v --no-git
~~~

16. ###### Xss scan with Dalfox
~~~ ~~~
cat xss_params.txt | dalfox pipe  | cut -d " " -f 2 > dalfox_output.txt
~~~
*Or*
~~~ ~~~
dalfox file xss_params.txt | cut -d " " -f 2 > output.txt
~~~
- for deeper attack add this argument:
~~~ ~~~
--deep-domxss
~~~
- print only only poc when found with this argument:
~~~ ~~~
Silence --silence
~~~

17. ###### when you find keys/tokens - check here
https://github.com/streaak/keyhacks

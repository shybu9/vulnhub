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
![rick netdiscover](https://user-images.githubusercontent.com/112984045/202394059-da3ca2e9-6765-48a2-b0c4-f593dd7055f0.png)<br>
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





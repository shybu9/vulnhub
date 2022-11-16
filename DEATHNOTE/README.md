
# DEATHNOTE
#### Download the machine from vulnhub or go for the [link](https://download.vulnhub.com/deathnote/Deathnote.ova).
![deathnote vulnhub](https://user-images.githubusercontent.com/112984045/201843771-c3f68b39-9b6e-4df4-9eef-0d90fa1c8445.png)<br>

* #### This is a direct walk-through to the flag. Hopping that you have given your best before referring to this write-up
* #### Do follow this page through out the line to void confusion.

### `setup the machine to vmware or virtualbox and run the machine.`
### ` After a successful setup go for the commands :`

## ENUMERATION :

```bash
netdiscover -i < interface >
```
![deathnote netdiscover](https://user-images.githubusercontent.com/112984045/201920948-904f4e4d-0ac8-42ac-bf79-49646b91c2f3.png)<br>

* For ENUMERATION we use nmap tool which come by default in kali linux.
 <br>command :
 
```bash
nmap -sC -sV -T4 -v < IP >
```
![deathnote nmap](https://user-images.githubusercontent.com/112984045/201921950-90d2d0a7-9879-4919-b4eb-397ba12743df.png)<br>
 ~ we can add -v argument for more verbose output.
 
  * I usually perform one more scan by using my personal tool : [port-scanner](https://github.com/shybu9/port-Scanner)
![deathnote portscanner](https://user-images.githubusercontent.com/112984045/201923393-7c7f0019-07c4-40cb-8f00-3ad50954bacd.png)
 ~ I prefer this tool because of its speed as you can see it just took 40 seconds for scanning 65535 ports.Even still some improvements to be done
 
 ### ANALYSING BOTH SCANS :
 * number of OPEN PORTS : 2
 * PORT NUMBERS : 22,80
 * OPERATING SYSTEM : Uinux, Linux
 * service running on PORT 22 : ssh
 * service running on PORT 80 : http
 
 * As the port 80 is open lets have a look on web pages using IP
 ```bash
 http://<IP>
 ```
 ![deathnote iponweb](https://user-images.githubusercontent.com/112984045/201925983-a0bcb8d9-91a8-4bf9-bcf1-67a0c31efb03.png)

 
 <br>
 
 * As the web-request is redirection to deathnote.vuln.. go for changing the host
 ```bash
 nano /etc/hosts
 ```
 * Add the ip and web domain<br>
 ![deathonte etchosts](https://user-images.githubusercontent.com/112984045/202195455-15b4f27b-efae-4331-8bf8-40886fcb5942.png)
<br>

```bash
 gobuster dir -u < IP >/  --no-error -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50
```
![deathnote gobuster](https://user-images.githubusercontent.com/112984045/202196928-a5a374e9-b12c-4146-bad0-a2b69c46696b.png)
```bash
gobuster dir -u < IP >/  --no-error -w /usr/share/wordlists/dirb/common.txt  -t 50
```
![deathnote gobuster common](https://user-images.githubusercontent.com/112984045/202197447-008f5b28-3b2e-41e4-85f3-cbd5325101ab.png)
<br>

* Web-request
```bash
http://< IP >/robots.txt
```
![deathnote robots](https://user-images.githubusercontent.com/112984045/202197893-4fdb3263-af51-4c5e-bb03-988b2e803244.png)<br>

`follow the lead`
```bash
http://< IP >/important.jpg
```
![deathnote importweb](https://user-images.githubusercontent.com/112984045/202199038-4d4e031e-c11d-4990-96bf-e84036559c65.png)
```bash
wget http://< IP >/important.jpg
```
![deathnote important crack](https://user-images.githubusercontent.com/112984045/202199212-ec1e495f-0b6a-46b8-84d2-0cd4a5ddc942.png)




 
 
 

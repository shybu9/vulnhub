
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
 
 * 

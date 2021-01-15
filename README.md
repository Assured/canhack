# Welcome to Assured CANHACK!
Public documentation for students attending the canhack course by Assured

# Student instructions
SSH key and student identification number will be provided by the instructor. 

## Setup student proxy
*NOTE! Port in this example could be any unused port over 1024.*

`studentX` should be `student1`, `student2`, `student3` etc.
```
ssh -i student -fND 9999 studentX@canhack.assured.se 
```

## SOCKS4 PROXY
Setup your browser to proxy traffic through IP 127.0.0.1 PORT 9999. 

The backend service and race-track will be located at `http://172.16.5.100`.

The cycar avaiable to you will be located at `http://172.16.5.10X` (where X corresponds to your student identification number).

## SSH to cycar
If your student username is `student1` then the IP address is `172.16.5.101`, if `student2` then the IP address is `172.16.5.102`, if `student10`then the IP address is `172.16.5.110` etc.
```
ssh -i student_private_key -o 'ProxyCommand nc -x 127.0.0.1:9999 %h %p' canuser@172.16.5.10X
```

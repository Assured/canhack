# Welcome to Assured CANHACK!
Public documentation for students attending the canhack course by Assured

# Student instructions
NOTE! Port in this example could be any port over 1024. 

## Setup student proxy
`studentX` should be `student1`, `student2`, `student3` etc.
```
ssh -i student -fND 9999 studentX@canhack.assured.se 
```

## SOCKS4 PROXY
Setup your browser to proxy traffic through IP 127.0.0.1 PORT 9999. 

## SSH to cycar
If your student username is `student1` then the IP address is `172.16.4.101`, if `student2` then the IP address is `172.16.5.102` etc. 
```
ssh -i student_private_key -o 'ProxyCommand nc -x 127.0.0.1:9999 %h %p' canuser@172.16.5.10X
```

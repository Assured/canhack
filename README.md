# Welcome to Assured CANHACK!
Public documentation for students attending the remote canhack course by Assured.

# Student instructions
SSH key and student id will be provided by the instructor. 

## Lab environment
The lab environment consists of three pieces which is used in this course. 

 - The canhack gateway to enable access to the lab environment.
 - The canhack backend to display the race and the scoreboard. 
 - The canhack cycar to be used for the labs.
 
The canhack cycar is the main component of the course and is where most labs will take place. It runs multiple services, connects to the CAN bus and a runs web service (dashboard). 

### Setup student proxy
*NOTE! Port in this example could be any unused port over 1024.*

To access the lab environment you'll need a student id and a private key for SSH. You'll use this secrets to establish a dynamic port forwarding proxy using SSH as seen here below. `studentX` should be `student1`, `student2`, `student3` etc.
```
ssh -i student_private_key -fND 9999 studentX@canhack.assured.se 
```

### SOCKS4 PROXY
To be able to access the web services of both cycar and backend you'll need to instruct your browser to connect through the SSH proxy. If you've used the same port number as the example above, instruct your browser to proxy traffic through IP 127.0.0.1 PORT 9999. 

The backend service and race-track will be located at `http://172.16.5.100`.

The cycar avaiable to you will be located at `http://172.16.5.10X` (where X corresponds to your student id).

### SSH to cycar
To access the labs and the CAN bus you'll need to connect to the cycar. If your username is `student1` then the IP address of the cycar is `172.16.5.101`, if `student2` then the IP address is `172.16.5.102`, if `student10`then the IP address is `172.16.5.110` etc.
```
ssh -i student_private_key -o 'ProxyCommand nc -x 127.0.0.1:9999 %h %p' canuser@172.16.5.10X
```

## Labs
### Lab 1 - Lies on the bus!
Number of flags: 3
Tools: cansend, candump

Create your own CAN frames using the command “cansend”. Interact with the system by sending your own CAN frames on the CAN bus.

Try to find which arbitration IDs exist, what their functions are and how to control these functions using the API.

 - Can you turn on/off the “warning light”? (Only the left and right turn signals!)
 - Can you turn on all the lights at the same time? 
 - Can you change the advertised speed?


### Lab 2 - Firmware update
Number of flags: 2
Tools: cansend, candump

The developers implemented a firmware update service. The service is password protected for security reasons, try to find out the username and password to access the service. Try to update the firmware of the device using this service. If something isn’t working, try to solve the issue.

*Don’t try to crack the security access key, as it shouldn’t be possible within the lab time.*

 - Which TCP port is exposing the firmware update service?
 - What are the login credentials?
 - Why is the firmware update failing?

### Lab 3 - I lost my keys!
Number of flags: 1
Tools: candump, calculator 

There’s an API call “/api/remote/engine/[start|stop]”.

Analyze what’s happening on the CAN bus during the remote engine start and stop. Your goal is to understand the algorithm and crack the security key to create your own security access session.

 - Is the seed predictable?
 - What algorithm is used to calculate the key?
 - What’s the secret?

Send the secret on arbitration ID 654 to check if it’s the correct one.
If you get the flag, the secret is correct!

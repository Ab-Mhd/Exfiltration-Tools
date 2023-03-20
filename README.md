# ExfiltrationTools
Two practicals preformed based on resources in "benstew / awesome-data-exfiltration" with description for each PRO/CON.



# :books: Why? 

I came across this GitHub repo in a class discussion; I never used or looked at exfiltration tools in depth. I decided to explore all the tools and then use four different devices to exfiltrate data to get a better understanding of the exfiltration process.

### Tools:

- badcookie.py 
- packetwhisper 
- cloackify 
- steghide


Resources:
https://github.com/benstew/awesome-data-exfiltration



## DNSExfiltrator

### Pros:
- Dns exfiltration is hard to detect, unlike with other methods, DNS must always be active so you cannot disable it or simply block the port. The only real way you can challenge this method is by either setting up dedicated DNS servers or by monitoring the difference in the amount of information being sent and received by a client or through the implementation of network inspection by using security products that analyze DNS traffic(eg TTL, Query sizes) and by whitelisting name servers. However, with DNS over HTTPS the traffic cannot be encrypted. DNSExfiltrator is a great tool to be used when the data being exfiltrated is small in size.

### Cons:
- The use of this method is relatively complicated, you have to make sure to properly set up the both the client and server-side scripts to run properly. There is also a dependency which must be installed which can cause errors if not installed properly. Issues can also arise due to the encoding used by DNSExfiltrator, by default base64 is used but some DNS resolvers will break this so the -b32 flag must be used to change the encoding to suite the resolver. So, the user must make sure that they know which encoding to use. Due to the nature of DNS requests the amount of data that can be exfiltrated cannot be large as it that would immediately raise red flags, so its best used with text files but is not suitable for
transferring large folders etc.



## Egress-Assess

### Pros:
- This tool provides a huge level of flexibility for exfiltrating data, it gives the attacker the option to use many different protocols like SMTP, (S)FTP, HTTP(S), ICMP. This allows the attacker to try many options and chose a protocol that suits their needs. For example, if transferring small text files ICMP would be ideal but when wanting to choose large sized data the attacker can choose a protocol like FTP. The attacker can even use this tool to set the data size they want the exfiltrated data to be transferred in. The detection of this tool can be hard because of the number of options that are available. The network admins must have all their bases covered for all the ports and must have an existing baseline set so that
they’re able to see the difference.

### Cons:
- Due to the large number of options, the set-up of this tool can be complicated, especially when wanting to use options like the SMTP protocol. For an experienced user this won’t be an issue but for a new one they must make sure that both sides using the tool are configured properly which can make them run into errors or cause difficulties. Another issue that may arise is that if the user tries many different ways, they may alert the admins because they may be using a protocol that is not usually used on the client
side so this may cause suspicion.



## PacketWhisper


### Pros:
- PacketWhisper is a great way to overcome whitelisting techniques. Through the use of steganography the attacker does not need to control their own DNS name server and can use the whitelisted ones. Sothe attacker is able to perform exfiltration in a way where it appears to the system that their own approved DNS name servers are being used except that the information never actually reaches the whitelisted name server and instead it’s received by the attacker. There are also no dependencies used so the project is fully atomic which promotes ease of use. Due to the tool using dns queries and not
responses we can send large files without detection.

### Cons:
- DNS data exfiltration can be a slow process so although we can exfiltrate large files using this specific tool it will take a while, also the volume of requests can be a huge indicator of compromise, as packetwhisper breaks down data into many consecutive queries the time between requests and the large amount of them would set off any rules in place to detect.


## Pulsar

### Pros:
- Pulsar is a simple yet effective tool, it allows us to create covert channels for data exfiltration, there is also a handler that enables the changing of data in transit. We can encode data using either base32/64 and it also supports the use of ciphers with keys. This keeps the data encrypted. Since TCP and UDP options are available, data exfiltration can happen at relatively high speeds.

### Cons:
- This tool is written in Go language which isn’t available by default on most machines so compiling the
tool may be an issue.


## PyExfil

### Pros:
- This tool provides a vast amount of options for data exfiltration, there are networking, communication, steganography and even physical techniques. This makes it extremely hard to detect as data could realistically be split into different parts and be transferred over the use of serval techniques. There are also many LAN methods available (eg ARP Broadcasts) that make it almost impossible to detect. But all of these options mean that the attacker can transfer large amounts of data without being detected.

### Cons:
- Due to the number of options, there are many dependencies that must be installed correctly, this tool can also be hard to use and a relatively large tool in comparison to the aforementioned ones. This tool is also unstable as it wasn’t originally made for red teaming and started out as a game so users can run into issues

## Powershell-RAT

### Pros:
- This RAT gives the attacker an almost live view of what the compromised user is doing. Through screen shots the attacker can see everything. The tool also gives us the option to create a backdoor into the machine which allows for the exfiltration of things such as clipboards, files and even gives the option of setting the wallpaper on the compromised host. The execution of screen shots can also be timed by the attacker. It can also be compiled into a windows executable so if python isn’t available the tool will still work. The tool is fully undetectable by AV software as it uses a living of the land technique and works on
fully patched windows environments.

### Cons:
- The tool needs a gmail account to work, registering a Gmail account can cause the attacker to be
identified.


## DET

### Pros:
- Allows for a huge number of plugins to suite specific data exfiltration and provides multi-channel
support. This allows for large data exfiltration.


### Cons:
- Requires dependencies, can be hard to setup and through network monitoring and DLP procedures it can be detected.


## SG1

### Pros:
- SG1 includes a large amount of options and protocols for data exfiltration, it allows for the transfer of data through the use of encrypted tunnels, its highly modulated so the user can use specific parts of the tool easily. The tool also enables the user to use self-deleting paste bins, this erase any trace of the
exfiltration. Large files can be transferred using this tool.


### Cons:
- This tool can be detected due to the simple nature of how the protocols are used and it is written using
Go language which is not available on systems by default. The tool is also hard to use as a beginner.

## ZLIB

### Pros:
- Includes a huge number of options for compressing data, this means that regardless of the system there
will almost definitely be an option that works on the compromised host. But it cannot be detected because of its nature and allows the transfer of large data.


### Cons:
- ZLIB is simply a library of compressing options so it does not provide any actual channels for data transfer. Also there are limitations for how the program can be compiled, for example it cant work with gcc 2.6.3 and wont work on RISCOS or BEOS, these configuration options make the library difficult to
use.


## DropFlop

### Pros:
- Allows the creation of a C2 Channel through the use of a widely used program and enables the attacker
to send tasks.

### Cons:
 
- Very incomplete README.md file which can make it hard to use if the user doesn’t know how to read
python. It also doesn’t provide any methods for the encryption of data into regularly used system command and is not a multi-channel tool.



## Badcookie

### Pros:

- A simple yet effective tool of transferring data over HTTP. Encodes the data so its not visibale to the naked eye and since it uses cookies which are encoded in the same base it is almost undetictable when
web requests are not limited or monitored.

### Cons:

- No actual description of how to use the script. It is hard to transfer large files using this technique. Since
HTTP is used instead of HTTPS, this can make the requests stand out.


## Cditter

### Pros:
- Unlike the other methods this provides the use of a physical medium.

### Cons:
- Very slow rate of data transfer, user must have a cd-drive which a lot of Laptops don’t come with these days. There must also be a camera aimed at the drive to calculate the messege and the picture must be clear enough for the Manchester code to be deciphered. This technique is very detectable as it uses theejection of the CD-Drive.


## Cloakify

### Pros:
- Allows transformation of any files into strings to avoid detection. It also gives the option to transform the files in a specific type of strings(eg. Pokémon names, ip addresses etc). This allows the transfer or large files across different security devices and lets the string meet rules that may otherwise block the transfer of strings. There are also baiting ciphers like MD5 that can be used to distract. This tool is very easy to use and comes with a great guide on how to use it. You are also able to create your own custom ciphers.

### Cons:
- There is no channel or way that is provided for actually transferring the data.


# spotexfil

### Pros:
- A very undepictable and unexpected way to exfiltrate data which is easy to use and relatively
undetectable if the user uses the spotify application regularly.
 

### Cons:
- Needs a Spotify username and since the transfer occurs using 300 bytes at a time the tool is unsuited for large data transfers. Spotify is almost never on work machines so the use case for this tool is very limited.


# Sneaky-creeper

### Pros:
- Enables the use of salesforce and google spreadsheets which are readily available on corporate
workstations. This method is relatively undetectable and easy to use.

### Cons:
- Needs the registration for whatever social media the attacker decides to use, there are issues with
dependencies which can cause problems when installing the tools. Due to the limitations usually placed on API’s from the issuing company this isn’t an ideal way for transferring large files.


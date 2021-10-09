# Snort-rules-with-some-instructions:

Snort instructions and rules
How to install Snort using the guide found on the website https://binexishatt.medium.com/installing-snort-on-kali-linux-9c96f3ab2910 by Alexis Rodriguez. After installing Snort, I created a directory called snort which I then ran everything under. I also created a directory called logs for the results to go under. I used nano to open and create a rule file called fullstack.rules. I used the following rules:
  alert tcp any any -> any 25 (msg: "SMTP Attack"; sid:10000001)
  alert tcp any any -> any any (msg: "XSS Attack"; content:"<script>javascript:alert(1)</script>"; sid:10000002)
  alert tcp any any -> any 23 (msg: "Telnet connection attempt"; sid:10000003)
  alert icmp any any -> any any (msg:”Possible Nmap ping sweep”; dsize:0; sid:1000004)
  alert tcp any any -> any any (msg:”TCP Port Scanning”; detection_filter:track by_src, count 30, seconds 60; sid:1000005)
  
I then opened wireshark from the command line using sudo and started recording. Opened the Metasploitable VM and ran an nmap scan, ping to host computer, as well as a telnet attempt. Ran Snort using "snort -k none -l ./logs/ -c ./fullstack.rules -r ./captured.pcap" to get my alerts. For my rules I did not specify my host machine as I then also ran Snort against the sample pcaps given. I then went into the logs directory to cat the alerts file. There I saw all the alerts for the scan based on my rules.

# Vicker's IP

***

## Description

```
Hi! It's good to see you again in my networking series.
There are total 18 challenges in this series & based on real life events of how can a server be compromised.
Please download the attachment which will be used to answer all the questions.
Don't make it too complex. Just keep it simple. Hope you'll solve them all.
Wish you all a very good luck.

Scenario: Recently one of Knight Squad's asset was compromised.
We've figured out most but need your help to investigate the case deeply.
As a SOC analyst, analyze the pacp file & identify the issues.

So let's start with the basic.

What is the victim & attacker ip?

Flag Format: KCTF{victimIp_attackerIp}
```

***

## Solution

we have a pcapng file. went ahead and opened it up on wireshark.

![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/945c38a3-8180-4bfe-b7e6-cb6f8a1bf993)

my first whim was from this,\
there was a huge amount of requests between 192.168.1.7 and 192.168.1.8.\
but I decided to try and confirm my hunches.

I googled `How to dentify a hacker of a tapped network of a pcap file?`\ 
and reached <a href = "https://osqa-ask.wireshark.org/questions/55868/identify-a-hacker-of-a-tapped-network-of-a-pcap-file/">this</a>\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/379a2cea-8db9-4cb3-8ced-7f1fcf6c8f32)\

I did exactly that.\
I put a filter with `http.request.method` and yes :\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/cf4cac53-2128-4f3f-bf03-5629c159d544)

***

### Flag > `KCTF{192.168.1.8_192.168.1.7}`

***



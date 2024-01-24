# Dragon's binary

***
## Description

```
In the mystical land of Eldoria, a fierce dragon had captured the kingdom's most precious treasure,
hiding it behind a magical binary. The bravest knight of the realm, Sir Emeric, known for both sword and wit,
embarked on a quest to retrieve the treasure. To succeed, he must reverse the dragon's binary.
As Sir Emeric's trusted apprentice in "Dragon's Binary" you are tasked with solving the cipher
to reveal the hidden treasure and help vanquish the dragon's spell.
Your journey is filled with mystery and danger, where only the sharpest mind can prevail.

Right Passcode is the flag.
```

***
## Solution

we got a file `dragon.binary`

on running it, it asks for a password\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/e588c13d-6a5d-47fe-a9b0-095178c46910)

on decomipiling it with ghidra\
Under defined strings I found something interesting\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/b0a1943d-c958-4cfb-b264-50a81007137b)

`IamDragon`

but that turned out to be a rabbit hole,\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/fb99df74-ad1f-4e6a-9f13-5a87269bd15e)

a while later I ran `strings` on it on a whim and\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/e41fcc79-e36c-4ea9-a10c-28e2bed9be19)

tried `letMeIn` and yes:

![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/5a6c1e4a-1ec6-4364-90a1-7a442b3c2881)

***

### Flag > `KCTF{letMeIn}`

***

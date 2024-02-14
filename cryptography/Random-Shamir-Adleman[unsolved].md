# **Random-Shamir-Adleman [unsolved]**

****

### Description
`This standard cipher comes with a twist! Flag Format:
KCTF{Fl4g_H3Re}`

****

### Solution

<br>
we are given with 2 attached text files :

[cipher.txt](https://github.com/IC3lemon/Knight-ctf/files/14000204/cipher.txt)
[note.txt](https://github.com/IC3lemon/Knight-ctf/files/14000212/note.txt)

As the name of the challenge, we probably are to decrypt this ciphertext using RSA,

```txt
c = 1913607487336850198612381177842742944535528551492332730687709803333994170933334235248158693072452023061642877943692858799822420964044267542215434514413393
```



but as we can see in `note.txt` we don't have a value for `p`, we're supposed to find that out<br>
We have a further hint in the note too :<br>
```txt
p = (A random 256 bit prime number)
q = 81950208731605030173072901497240676460946134422613059941413476068465656250011

e=65537

Hint: Alice told me to do an Axe-Ore between 'usedistofindouttheseed' and 'thisisthekeytogetyourseed' to obtain some numerical/integer value to help in the process of finding the value of p.

something to do with a "seed" I guess...is it?? idk...

As always..I have no idea what she meant. To be honest Im not even sure if it was Axe-Ore or was it Eksor...uggh...never mind
```
<br>

So they're telling us we gotta perform an XOR between `usedistofindouttheseed` and `thisisthekeytogetyourseed`<br>
and then do some "seed" stuff w/ it. I got no clue what that means.<br>

but first, I decided to XOR those two<br>
I used <a href = "https://www.dcode.fr/xor-cipher">this</a> site to do the same.<br>

and got this guy `413673984171035014537352995108480568815660353722135`
as the integer number result.

Now to use this thing as the "seed" for something.

a few minutes of googling later I found out about the `rand()` and `srand()` function in c++.\
and like in the challenge name, "***Random** Shamir Adleman*"\
I thought this was prolly the way to go.

I found out that you could "seed" the rand function. (couldn't get any more relevant)<br>
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/ba495b2c-ef4e-49e1-b849-350dc385063c)


So I opened up a python compiler and did this :<br>

```python
import random
random.seed(413673984171035014537352995108480568815660353722135)

print(random.getrandbits(256))
```
and got the output :
`1819857090125556605804890938921613656339483497772764807998369991456727263988`

So if what I did so far was correct, the above number should be p. \
P is also supposed to be prime. \
I decided to check that. 

![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/a745aa47-e5e8-406e-9109-361798e36794)


![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/db63c655-5228-4119-b8b6-ae61d15a485a)






UPDATE :


Turns out I was on the right track.\
This is almost a month after the ctf but I've managed to solve it.

I just had to find the next prime number to my earlier output.\
AND THAT WAS P.\
bruhhhh.

I did stuff in this order:\
1. XOR 'usedistofindouttheseed' and 'thisisthekeytogetyourseed'
2. seed the rand with this XOR'd value
3. get a 256 bit random number
4. find the nextprime to this random number
5. this guy is p
6. put p,q,c,e into an rsa decoder

here's the code I used : 

```python
from Crypto.Util.number import *
import sympy
import random

def sXOR(a,b):
    a_ke_bytes = []
    b_ke_bytes = []
    for i in a:
        a_ke_bytes.append(bin(ord(i))[2:])
    for i in b:
        b_ke_bytes.append(bin(ord(i))[2:])
    num1 = int(''.join(a_ke_bytes), 2)
    num2 = int(''.join(b_ke_bytes), 2)
    result = num1 ^ num2
    return result

str1 = 'usedistofindouttheseed'
str2 = 'thisisthekeytogetyourseed'

seed = sXOR(str1,str2)
random.seed(seed)
c = 1913607487336850198612381177842742944535528551492332730687709803333994170933334235248158693072452023061642877943692858799822420964044267542215434514413393
p = sympy.nextprime(random.getrandbits(256))
q = 81950208731605030173072901497240676460946134422613059941413476068465656250011
e = 65537
N = p * q
print("c => "+str(c))
print("p => "+str(p))
print("q => "+str(q))
print("e => "+str(e))
print("N => "+str(N))
```

```
c => 1913607487336850198612381177842742944535528551492332730687709803333994170933334235248158693072452023061642877943692858799822420964044267542215434514413393
p => 69741716681423118542834588968007281757658875608479690139723526814390717818213
q => 81950208731605030173072901497240676460946134422613059941413476068465656250011
e => 65537
N => 5715348239343085037628413821199168147425144754093390410437089483084108841828118188121729740762480994851807889187448972062093060449305836515479545177250343
```

![image](https://github.com/IC3lemon/Knight-ctf-2024/assets/150153966/df48f61d-895e-4d3e-869f-76f45b5f16c2)

![image](https://github.com/IC3lemon/Knight-ctf-2024/assets/150153966/d92229b8-d8b1-4ed5-afd9-7b64c9fc33ce)

***

### Flag > `KCTF{ju57_57d_r54_w17h_61v3n_533d_v4lu3_d6ae7c3f}`



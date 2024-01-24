# **Random-Shamir-Adleman [unsolved]**

****

## | Description
`This standard cipher comes with a twist! Flag Format:
KCTF{Fl4g_H3Re}`

****
### | Solution


<p>we are given with 2 attached text files :</p>

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
I used <a href = "https://toolslick.com/math/bitwise/xor-calculator">this</a> site to do the same.<br>

and got this guy `413673984171035014537352995108480568815660353722135`
as the decimal result.

Now to use this thing as the "seed" for something.<br>

a few minutes of googling later I found out about the `rand()` and `srand()` function in c++.<br>
and like in the challenge name "***Random** Shamir Adleman*" I thought this was prolly the way to go.<br>

I found out that you could "seed" the rand function. (couldn't get any more relevant)<br>
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/bd6db51a-b8e9-4e96-a63d-b73acb9b954e)

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






<h1>Random Shamir Adleman[unsolved]</h1>

#### ***Description -***
>This standard cipher comes with a twist!<br>
>Flag Format: KCTF{Fl4g_H3Re}

***

#### ***Solution -***
<p>we are given with 2 attached text files :</p>

[cipher.txt](https://github.com/IC3lemon/Knight-ctf/files/14000204/cipher.txt)
[note.txt](https://github.com/IC3lemon/Knight-ctf/files/14000212/note.txt)

As the name of the challenge, we probably are to decrypt the ciphertext using RSA,<br>
but as we can see in `note.txt` we don't have a value for `p`, we're supposed to find that out<br>
We have a further hint in the note too :<br>
```
Hint: Alice told me to do an Axe-Ore between 'usedistofindouttheseed' and 'thisisthekeytogetyourseed'
to obtain some numerical/integer value to help in the process of finding the value of p.

something to do with a "seed" I guess...is it?? idk...

As always..I have no idea what she meant. To be honest Im not even sure if it was Axe-Ore or was it Eksor...uggh...never mind
```
<br>

So they're telling us we gotta perform an XOR between `usedistofindouttheseed` and `thisisthekeytogetyourseed`<br>
and then do some "seed" stuff w/ it. I got no clue what that means.<br>

but first, I decided to XOR those two<br>
I used <a href = "https://toolslick.com/math/bitwise/xor-calculator">this</a> site to do the same.<br>

and got this guy `630196368849837217686964916396199804335596313572775163599617`
as the decimal result.

Now to use this thing as the "seed" for something.<br>

a few minutes of googling later I found out about the `rand()` and `srand()` function in c++.<br>
and like in the challenge name "***Random** Shamir Adleman*" I thought this was prolly the way to go.<br>

I found out that you could "seed" the rand function. (couldn't get any more relevant)<br>
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/bd6db51a-b8e9-4e96-a63d-b73acb9b954e)

So I opened up a C compiler and did this :<br>

```
#include <stdio.h>

int main() {
    
    srand(630196368849837217686964916396199804335596313572775163599617);
    printf("%d",rand());

    return 0;
}
```
and got the output :
`733241977`

So if what I did so far was correct, the above number should be p.<br>
P is also supposed to be prime. I decided to check that.<br>

![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/6e63edc7-7d7c-4dcf-a845-613960ee4c8e)

![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/e0049438-1af2-423b-8241-504187ef8abc)



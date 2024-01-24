# Knight-armoury [solved it later]

***

## Description

```
In a realm where magic and technology merge,
lies the Knight Armoury, home to the legendary "Sword of Bytes."
Forged by Knight Squad, this digital sword holds immense power.
Your mission: reverse the ancient binary guarding the Armoury and claim
the sword to become the protector of the digital kingdom.
Only the wisest and most skilled in reverse engineering can succeed.
Are you ready to embark on this epic journey?

Connection Information
nc 198.58.104.183 11337

Flag Format: KCTF{Fl4G_HeRe}
```
NOTE : managed to solve this *after* the ctf.

***

## Solution

we are given with a file `knight_armoury`\
decompiled it with binary ninja and found this guy in the strings\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/66d18d41-e9cc-40be-a0ea-8567b4304436)\
`IaMaKnight`

tried it, but it wasn't it.\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/f8b3dd4d-c69e-4358-8e4e-b00121cb3ba4)


I headed over to the function where the password was being checked\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/aac1c5bd-b38c-4dfc-9a53-e012075f7598)

![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/4c6a2c1d-f044-44c6-85db-5cdd9512a1d8)

it seemed to be performing some operation *on* `IaMaKnight`.

I couldn't figure out exactly what operation that was until after the ctf,\
when I put `IaMaKnight` into cyberchef and messed around.\
on hitting rot13 bruteforce, I tried each value, and on rot16 :\
![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/1021cb1e-e6d8-42c1-95c4-81b362191bd2)

![image](https://github.com/IC3lemon/Knight-ctf/assets/150153966/cd5f25d3-bda7-40b2-953c-046d9cf3d5a0)

If only I tried this shit earlier ffs.

***

## Flag > KCTF{kN1gHT_aRm0uRy_aCC3ss_GranTed}

***

# chall_00_pwn_writeup

Welcome to the UD Secure Software Design aka x86Exploit course challenge one. Course contents avalible at https://sec.prof.ninja/.

  Course Author: Professor Andy Novocin
  
# chall_00

We begin by performing some recon on the binary. We run 'file a.out' and 'checksec a.out'

![image](https://user-images.githubusercontent.com/79220528/159257085-83f775f2-8ed6-40d7-b8c2-10d242b9dc27.png)

Observe the following:
  1. file command output states it's **dynamically** linked and **64bit**
  2. checksec reports there is no stack canary, meaning we are free to smash the stack with a buffer overflow.

Next, we open the file using radare2. Entering the command 'r2 -Ad a.out', observe main:

![image](https://user-images.githubusercontent.com/79220528/159257787-5ec10b6b-5c83-4c72-b387-0c7965383889.png)

We can see the 0x1337, this is leet speak. Below that we see a call to gets to write to var_110 and a comparision that compares var_4 to 0x69420. Note that var_4 is 4 bytes, so we will use p32 to overwrite it. 

If var_4 == 0x69420, system call to /bin/sh/ will execute and we'll have our shell. 

We need a payload that is 0x110-0x4 bytes of junk + p32(0x69420)

We create and run the script below to solve the problem. 

![image](https://user-images.githubusercontent.com/79220528/159261668-e100bfca-3721-4b55-8db7-3f1d23a10547.png)








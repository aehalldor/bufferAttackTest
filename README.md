The buffer attack should give us root access from the vulnerable file
To test the buffer attack open a linux VM

DISABLE ADDRESS RANDOMIZATION (this just makes it faster)
$ su root
Password: (enter root password)
#sysctl -w kernel.randomize_va_space=0

Configure bin
$ sudo rm /bin/sh
$ sudo ln -s /bin/zsh /bin/sh

Compile stack.c without protections (stack.c is out vulnerable file)
$ gcc -o stack -z execstack -fno-stack-protector stack.c
$ chown root stack
$ chmod 4755 stack

Perform the attack
$ gcc -o exploit exploit.c
$./exploit
$./stack

After running the above code we should get root access

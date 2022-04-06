# CC: Radare2

{% embed url="https://tryhackme.com/room/ccradare2" %}
https://tryhackme.com/room/ccradare2
{% endembed %}

## Task 2 Command Line Options

#### What flag to you set to analyze the binary upon entering the r2 console

{% hint style="success" %}
`-A`
{% endhint %}

#### How do you enable the debugger?

{% hint style="success" %}
`-d`
{% endhint %}

#### How do you open the file in write mode?

{% hint style="success" %}
`-w`
{% endhint %}

#### How do you enter the console without opening a file

{% hint style="success" %}
`-`
{% endhint %}

## Task 3 Analyzation

#### What command "Analyzes Everything" (all functions and their arguments: Same as running with radare with -A)

{% hint style="success" %}
`aaa`
{% endhint %}

#### What command does basic analysis on functions?

![](<../../.gitbook/assets/Screenshot from 2022-04-06 18-46-31.png>)

{% hint style="success" %}
`af`
{% endhint %}

#### How do you list all functions?

![](<../../.gitbook/assets/Screenshot from 2022-04-06 18-51-28.png>)

{% hint style="success" %}
`afl`
{% endhint %}

#### How many functions are in the example1 binary?

```bash
r2 example1
> aaa
> afl
> aflc
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 18-55-14.png>)

{% hint style="success" %}
`12`
{% endhint %}

#### What is the name of the secret function in the example1 binary?

{% hint style="success" %}
`secret_func`
{% endhint %}

## Task 4 Information

#### What command shows all the information about the file that you're in?

{% hint style="success" %}
`ia`
{% endhint %}

#### How do you get every string that is present in the binary?

{% hint style="success" %}
`izz`
{% endhint %}

#### What if you want the address of the main function?

{% hint style="success" %}
`iM`
{% endhint %}

#### What character do you add to the end of every command to get the output in JSON format?

{% hint style="success" %}
`j`
{% endhint %}

#### How do you get the entrypoint of the file?

{% hint style="success" %}
`ie`
{% endhint %}

#### What is the secret string hidden in the example2 binary?

```bash
ra ./example2
> izz
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-01-56.png>)

{% hint style="success" %}
goodjob
{% endhint %}

## Task 5 Navigating Through Memory

#### How do you print out the the current memory address your located at in the binary?

{% hint style="success" %}
`s`
{% endhint %}

#### What command do you use to go to a specific point in memory with the syntax?

{% hint style="success" %}
`s`
{% endhint %}

#### What command would you run to go 5 bytes forward?

{% hint style="success" %}
`s+`
{% endhint %}

#### What about 12 bytes backward?

{% hint style="success" %}
`s- 12`
{% endhint %}

#### How do you undo the previous seek?

{% hint style="success" %}
`s-`
{% endhint %}

#### How would go to the memory address of the main function?

{% hint style="success" %}
`s main`
{% endhint %}

#### What if you wanted to go to the address of the rax register?

{% hint style="success" %}
`sr rax`
{% endhint %}

## Task 6 Printing

#### How would you print the hex output of where you currently are in memory?

{% hint style="success" %}
`px`
{% endhint %}

#### How would you print the disassembly of where you're currently at in memory?

{% hint style="success" %}
`pd`
{% endhint %}

#### What if you wanted the disassembly of the main function?

{% hint style="success" %}
`pd @ main`
{% endhint %}

#### What command prints out the emoji hexdump? (this is not useful at all I just find it funny)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-20-23.png>)

{% hint style="success" %}
`pxe`
{% endhint %}

#### What if you decided you were too good for rows and you wanted the disassembly in column format?

{% hint style="success" %}
`pC`
{% endhint %}

#### What is the value of the first variable in the main function for the example 3 binary?

```bash
r2 ./example3
> pd @main
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-22-52.png>)

{% hint style="success" %}
`1`
{% endhint %}

#### What about the second variable?

{% hint style="success" %}
`5`
{% endhint %}

## Task 7 The Mid-term

```
r2 ./midterm
```

#### How many functions are in the binary?

```bash
> aaa
> aflc
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-28-15.png>)

{% hint style="success" %}
`13`
{% endhint %}

#### What is the value of the hidden string?

```bash
> izz
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-29-23.png>)

{% hint style="success" %}
`you_found_me`
{% endhint %}

#### What is the return value of secret\_func()?

```bash
pd @sym.secret_func
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-30-23.png>)

{% hint style="success" %}
`4`
{% endhint %}

#### What is the value of the first variable set in the main function(in decimal format)?

```bash
> pd @main
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-32-10.png>)

{% hint style="success" %}
`12`
{% endhint %}

#### What about the second one(also in decimal format)?

{% hint style="success" %}
`192`
{% endhint %}

#### What is the next function in memory after the main function?

{% hint style="success" %}
`midterm_func`
{% endhint %}

#### How do you get a hexdump of four bytes of the memory address your currently at?

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-33-48.png>)

{% hint style="success" %}
`px 4`
{% endhint %}

## Task 8 Debugging

![](<../../.gitbook/assets/Screenshot from 2022-04-06 21-41-50.png>)

#### How do you set a breakpoint?

{% hint style="success" %}
`db`
{% endhint %}

#### What command is used to print out the values of all the registers?

{% hint style="success" %}
`dr`
{% endhint %}

#### How do you run through the program until the program either ends or you hit the next breakpoint?

{% hint style="success" %}
`dc`
{% endhint %}

#### What if you want to step through the binary one line at a time?

{% hint style="success" %}
`ds`
{% endhint %}

#### How do you go forth 2 lines in the binary?

{% hint style="success" %}
`ds 2`
{% endhint %}

#### How do you list out the indexes and memory addresses of all breakpoints?

{% hint style="success" %}
`dbi`
{% endhint %}

## Task 9 Visual Mode

#### How do you enter "graph mode" which allows everything to be organized in nice readable boxes?

{% hint style="success" %}
`VV`
{% endhint %}

#### What character do you press to run normal radare commands inside visual mode?

{% hint style="success" %}
`:`
{% endhint %}

#### How do you go back to the regular radare shell(leaving visual mode)?

{% hint style="success" %}
`q`
{% endhint %}

#### What if you want to step through the binary inside Visual mode?

{% hint style="success" %}
`S`
{% endhint %}

#### How do you add a comment?

{% hint style="success" %}
`;`
{% endhint %}

## Task 10 Write Mode

#### How do you write a string to the current memory address.

{% hint style="success" %}
`w`
{% endhint %}

#### What command lists all write changes?

{% hint style="success" %}
`wc`
{% endhint %}

#### What command modifies an instruction at the current memory address?

{% hint style="success" %}
`wa`
{% endhint %}

#### Get the example4 binary to show the You win! message

```bash
r2 -w -d ./example4
> aaa
> pd @main
> wx 837dfc04 @0x5585200006bf
> p8 @0x5585200006bf!4
> dc
```

![](<../../.gitbook/assets/Screenshot from 2022-04-06 22-32-05.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-06 22-34-03.png>)

## Task 11 The Final Exam

#### What is the password that outputs the you win! message?

![](<../../.gitbook/assets/Screenshot from 2022-04-06 23-42-51.png>)

```python
after = "youdidit"
for i in range(8):
    print(chr(ord(after[i]) - ord("\n")), end="")
```

{% hint style="success" %}
`oekZ_Z_j`
{% endhint %}

## Reference

{% embed url="https://monosource.gitbooks.io/radare2-explorations/content/intro/editing.html" %}

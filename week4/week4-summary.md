# Week 4 Summary

This week was focused on software exploits.  To examine the behavior of several example exploits, the WinDbg debugging tool was used.  Here is a summary of some useful commands for WinDbg.


## WinDbg

#### Basic memory commands
`lm` lists modules
`lmf` finds a module
`bp` breakpoint
`bl` breakpoint list
`dd` displays a dword of memory
`u` unassembles memory


`.hh` help

`.formats`
`dv` shows local variables
`db` shows bytes and ascii string representation 
`da <value>` show ascii string
`du` unicode strings

`t` step into
`p` step over
`g <address>` goes to address

`!teb` stack
`!peb` heap
`!address`

`k` shows stack

### Exploits

The exploits demonstrated in the labs are considered to be memory corruption vulnerabilities.  The labs covered two types of memory vulnerabilities: stack overflow and user after free.

Memory Corruption - 
	* vulnerabilities which depend on unexpected user input

Stack Overflow -
	* This is a type of memory corruption vulnerability.  By writing to memory in the program's stack, it is possible to overwrite a return address and control program execution

Use After Free -
	* Memory that is allocated is freed and replaced with a malicious object which the program then uses.


### Thoughts and Conclusions	

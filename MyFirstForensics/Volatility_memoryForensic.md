# The Volatility Framework

>* 
>* https://github.com/volatilityfoundation/volatility
 
>* 
>* 
```
```
## Using Volatility

https://github.com/volatilityfoundation/volatility/wiki/Volatility-Usage

$ python vol.py [plugin] -f [image] --profile=[profile] 

$ python volatility.py [plugin] -f [image] --profile=[profile] 

![Volatility指令格式](pic/Volatility-Usage.png)

常用指令

看看支援那些 profiles ==> $ python vol.py –info

看看支援那些Options: ==>volatility -h[Kali linux 2018.1(64bit)2018/6/17]

Options:
```
  -h, --help            list all available options and their default values.
                        Default values may be set in the configuration file  (/etc/volatilityrc)
  --conf-file=/root/.volatilityrc     User based configuration file
  -d, --debug           Debug volatility
  --plugins=PLUGINS     Additional plugin directories to use (colon separated)
  --info                Print information about all registered objects
  --cache-directory=/root/.cache/volatility     Directory where cache files are stored
  --cache               Use caching
  --tz=TZ               Sets the (Olson) timezone for displaying timestamps
                        using pytz (if installed) or tzset
  -f FILENAME, --filename=FILENAME
                        Filename to use when opening an image
  --profile=WinXPSP2x86
                        Name of the profile to load (use --info to see a list
                        of supported profiles)
  -l LOCATION, --location=LOCATION
                        A URN location from which to load an address space
  -w, --write           Enable write support
  --dtb=DTB             DTB Address
  --shift=SHIFT         Mac KASLR shift address
  --output=text         Output in this format (support is module specific, see
                        the Module Output Options below)
  --output-file=OUTPUT_FILE
                        Write output in this file
  -v, --verbose         Verbose information
  --physical_shift=PHYSICAL_SHIFT
                        Linux kernel physical shift address
  --virtual_shift=VIRTUAL_SHIFT
                        Linux kernel virtual shift address
  -g KDBG, --kdbg=KDBG  Specify a KDBG virtual address (Note: for 64-bit
                        Windows 8 and above this is the address of  KdCopyDataBlock)
  --force               Force utilization of suspect profile
  -k KPCR, --kpcr=KPCR  Specify a specific KPCR address
  --cookie=COOKIE       Specify the address of nt!ObHeaderCookie (valid for Windows 10 only)
```

	Supported Plugin Commands:
```
		amcache        	Print AmCache information
		apihooks       	Detect API hooks in process and kernel memory
		atoms          	Print session and window station atom tables
		atomscan       	Pool scanner for atom tables
		auditpol       	Prints out the Audit Policies from HKLM\SECURITY\Policy\PolAdtEv
		bigpools       	Dump the big page pools using BigPagePoolScanner
		bioskbd        	Reads the keyboard buffer from Real Mode memory
		cachedump      	Dumps cached domain hashes from memory
		callbacks      	Print system-wide notification routines
		clipboard      	Extract the contents of the windows clipboard
		cmdline        	Display process command-line arguments
		cmdscan        	Extract command history by scanning for _COMMAND_HISTORY
		connections    	Print list of open connections [Windows XP and 2003 Only]
		connscan       	Pool scanner for tcp connections
		consoles       	Extract command history by scanning for _CONSOLE_INFORMATION
		crashinfo      	Dump crash-dump information
		deskscan       	Poolscaner for tagDESKTOP (desktops)
		devicetree     	Show device tree
		dlldump        	Dump DLLs from a process address space
		dlllist        	Print list of loaded dlls for each process
		driverirp      	Driver IRP hook detection
		drivermodule   	Associate driver objects to kernel modules
		driverscan     	Pool scanner for driver objects
		dumpcerts      	Dump RSA private and public SSL keys
		dumpfiles      	Extract memory mapped and cached files
		dumpregistry   	Dumps registry files out to disk 
		editbox        	Displays information about Edit controls. (Listbox experimental.)
		envars         	Display process environment variables
		eventhooks     	Print details on windows event hooks
		evtlogs        	Extract Windows Event Logs (XP/2003 only)
		filescan       	Pool scanner for file objects
		gahti          	Dump the USER handle type information
		gditimers      	Print installed GDI timers and callbacks
		gdt            	Display Global Descriptor Table
		getservicesids 	Get the names of services in the Registry and return Calculated SID
		getsids        	Print the SIDs owning each process
		handles        	Print list of open handles for each process
		hashdump       	Dumps passwords hashes (LM/NTLM) from memory
		hibinfo        	Dump hibernation file information
		hivedump       	Prints out a hive
		hivelist       	Print list of registry hives.
		hivescan       	Pool scanner for registry hives
		hpakextract    	Extract physical memory from an HPAK file
		hpakinfo       	Info on an HPAK file
		idt            	Display Interrupt Descriptor Table
		iehistory      	Reconstruct Internet Explorer cache / history
		imagecopy      	Copies a physical address space out as a raw DD image
		imageinfo      	Identify information for the image 
		impscan        	Scan for calls to imported functions
		joblinks       	Print process job link information
		kdbgscan       	Search for and dump potential KDBG values
		kpcrscan       	Search for and dump potential KPCR values
		ldrmodules     	Detect unlinked DLLs
		lsadump        	Dump (decrypted) LSA secrets from the registry
		machoinfo      	Dump Mach-O file format information
		malfind        	Find hidden and injected code
		mbrparser      	Scans for and parses potential Master Boot Records (MBRs) 
		memdump        	Dump the addressable memory for a process
		memmap         	Print the memory map
		messagehooks   	List desktop and thread window message hooks
		mftparser      	Scans for and parses potential MFT entries 
		moddump        	Dump a kernel driver to an executable file sample
		modscan        	Pool scanner for kernel modules
		modules        	Print list of loaded modules
		multiscan      	Scan for various objects at once
		mutantscan     	Pool scanner for mutex objects
		notepad        	List currently displayed notepad text
		objtypescan    	Scan for Windows object type objects
		patcher        	Patches memory based on page scans
		poolpeek       	Configurable pool scanner plugin
		printkey       	Print a registry key, and its subkeys and values
		privs          	Display process privileges
		procdump       	Dump a process to an executable file sample
		pslist         	Print all running processes by following the EPROCESS lists 
		psscan         	Pool scanner for process objects
		pstree         	Print process list as a tree
		psxview        	Find hidden processes with various process listings
		qemuinfo       	Dump Qemu information
		raw2dmp        	Converts a physical memory sample to a windbg crash dump
		screenshot     	Save a pseudo-screenshot based on GDI windows
		servicediff    	List Windows services (ala Plugx)
		sessions       	List details on _MM_SESSION_SPACE (user logon sessions)
		shellbags      	Prints ShellBags info
		shimcache      	Parses the Application Compatibility Shim Cache registry key
		shutdowntime   	Print ShutdownTime of machine from registry
		sockets        	Print list of open sockets
		sockscan       	Pool scanner for tcp socket objects
		ssdt           	Display SSDT entries
		strings        	Match physical offsets to virtual addresses (may take a while, VERY verbose)
		svcscan        	Scan for Windows services
		symlinkscan    	Pool scanner for symlink objects
		thrdscan       	Pool scanner for thread objects
		threads        	Investigate _ETHREAD and _KTHREADs
		timeliner      	Creates a timeline from various artifacts in memory 
		timers         	Print kernel timers and associated module DPCs
		truecryptmaster	Recover TrueCrypt 7.1a Master Keys
		truecryptpassphrase	TrueCrypt Cached Passphrase Finder
		truecryptsummary	TrueCrypt Summary
		unloadedmodules	Print list of unloaded modules
		userassist     	Print userassist registry keys and information
		userhandles    	Dump the USER handle tables
		vaddump        	Dumps out the vad sections to a file
		vadinfo        	Dump the VAD info
		vadtree        	Walk the VAD tree and display in tree format
		vadwalk        	Walk the VAD tree
		vboxinfo       	Dump virtualbox information
		verinfo        	Prints out the version information from PE images
		vmwareinfo     	Dump VMware VMSS/VMSN information
		volshell       	Shell in the memory image
		windows        	Print Desktop Windows (verbose details)
		wintree        	Print Z-Order Desktop Windows Tree
		wndscan        	Pool scanner for window stations
		yarascan       	Scan process or kernel memory with Yara signatures
```

## The Volatility Framework:Volatility Plugins

>* http://www.forensicswiki.org/wiki/List_of_Volatility_Plugins

```
apihooks                   - Detect API hooks in process and kernel memory
crashinfo                  - Dump crash-dump information
dlldump                    - Dump DLLs from a process address space
dlllist                    - Print list of loaded dlls for each process
dumpfiles                  - Extract memory mapped and cached files
dumpregistry               - Dumps registry files out to disk
handles                    - Print list of open handles for each process
hashdump                   - Dumps passwords hashes (LM/NTLM) from memory
hibinfo                    - Dump hibernation file information
hivedump                   - Prints out a hive
hivelist                   - Print list of registry hives.
```

linux 相關plugins
```
linux_apihooks             - Checks for userland apihooks
linux_arp                  - Print the ARP table
linux_aslr_shift           - Automatically detect the Linux ASLR shift
linux_banner               - Prints the Linux banner information
linux_check_inline_kernel  - Check for inline kernel hooks
linux_check_modules        - Compares module list to sysfs info, if available
linux_check_syscall        - Checks if the system call table has been altered
linux_check_syscall_arm    - Checks if the system call table has been altered
linux_elfs                 - Find ELF binaries in process mappings
linux_lsof                 - Lists file descriptors and their path
linux_malfind              - Looks for suspicious process mappings
linux_memmap               - Dumps the memory map for linux tasks
linux_moddump              - Extract loaded kernel modules
```
## Youtube教學影片:

[Hacks Weekly #6: Memory Dump Analysis – extracting juicy data](https://www.youtube.com/watch?v=-8f8avZ2V7s)

## 實務演練環境:

#### 實務演練環境1:使用kali linux內附的

#### 實務演練環境2:使用Docker rekall image
```
1.下載:: docker pull remnux/volatility
2. 執行
sudo docker run --rm -it -v ~/memdumps:/home/nonroot/memdumps remnux/volatility bash
then run vol.py in the container with the desired parameters.

Before running the command above, create the "memdumps" directory on your host and make it world-accessible (e.g., chmod a+xwr ~/memdumps).
```
## 實務演練(1):SECCON CTF Quals 2016 : memory-analysis-100[網站已關閉]

>* https://github.com/ctfs/write-ups-2016/tree/master/seccon-ctf-quals-2016/forensic/memory-analysis-100

```
步驟一:volatility -f forensic_100.raw imageinfo

步驟二:顯示Processes運作狀態 ==> volatility -f forensic_100.raw --profile=WinXPSP2x86 pslist

WinXPSP2x86、WinXPSP3x86 結果都一樣

步驟三:一陣努力後者到關鍵的執行程式==>顯示IE瀏覽紀錄==>volatility -f forensic_100.raw --profile=WinXPSP2x86 iehistory


步驟四:

curl http://crattack.tistory.com/entry/Data-Science-import-pandas-as-pd

步驟五:
volatility -f forensic_100.raw --profile=WinXPSP2x86 connscan

當時的crattack.tistory.com是導向153.127.200.178

步驟六:
curl http://153.127.200.178/entry/Data-Science-import-pandas-as-pd

比賽已結束==>網站更新過==>沒有flag

```
[解答1](https://ctf.rip/seccon-2016-quals-memory-analysis-forensics-challenge/)

```
步驟一:
volatility -f forensic_100.raw imageinfo

步驟二:
volatility -f forensic_100.raw pslist | grep svchost

步驟三:
volatility -f forensic_100.raw -p 1704 -D dump procdump

步驟四:
volatility -f forensic_100.raw --profile=WinXPSP3x86 sockets

volatility -f forensic_100.raw --profile=WinXPSP3x86 pslist | grep tcp

volatility -f forensic_100.raw --profile=WinXPSP3x86 -p 3308 -D dump memdump

步驟五:

host crattack.tistory.com

echo 153.127.200.178 crattack.tistory.com >> /etc/hosts

curl http://crattack.tistory.com/entry/Data-Science-import-pandas-as-pd

SECCON{_h3110_w3_h4ve_fun_w4rg4m3_}



```

[解答2](https://blog.nhiroki.net/2016/12/11/seccon-2016-online-ctf-writeup)
```
步驟一:
$ volatility_2.5_linux_x86 -f ./forensic_100.dat --profile=WinXPSP2x86 connections

Foundation Volatility Framework 2.5
Offset(V)  Local Address             Remote Address            Pid
---------- ------------------------- ------------------------- ---
0x8213bbe8 192.168.88.131:1034       153.127.200.178:80        1080


步驟二:
$ strings forensic_100.dat | grep 153.127.200.178

153.127.200.178    crattack.tistory.com attack.tistory.com 
153.127.200.178    crattack.tistory.com 
153.127.200.178:80

步驟三:
$ strings forensic_100.dat | grep 'GET /' 

GET /image/237C0C3E576BA0AD06F720 HTTP/1.1
GET /entry/Data-Science-import-pandas-as-pd HTTP/1.1
GET /entry/Data-Science-import-pandas-as-pd HTTP/1.1
GET /entry/Data-Science-import-pandas-as-pd HTTP/1.1
GET /entry/Data-Science-import-pandas-as-pd HTTP/1.1

步驟四:
$ curl http://attack.tistory.com/entry/Data-Science-import-pandas-as-pd

SECCON{_h3110_w3_h4ve_fun_w4rg4m3_}
```


## 實務演練(2):nuit-du-hack-ctf-quals-2015-bpythonastic-300

>* https://github.com/ctfs/write-ups-2015/tree/master/nuit-du-hack-ctf-quals-2015/forensic/bpythonastic
>* https://wiki.zenk-security.com/doku.php?id=ndhquals2015:bpythonastic

步驟一:確定作業系統版本 ==> strings chall.raw | grep "Linux version"

步驟二:確認相關作業系統版本所需profile

https://packages.ubuntu.com/trusty/all/volatility-profiles/filelist

步驟三:執行基本分析

volatility --plugins=profiles -f chall.raw --profile=Linux_Debian_Squeeze_2_6_32-5-amd64_x64 -h | grep linux_

步驟四:

volatility --plugins=profiles -f chall.raw --profile=Linux_Debian_Squeeze_2_6_32-5-amd64_x64 linux_bash

步驟五:

volatility --plugins=profiles -f chall.raw --profile=Linux_Debian_Squeeze_2_6_32-5-amd64_x64 linux_pstree

volatility --plugins=profiles -f chall.raw --profile=Linux_Debian_Squeeze_2_6_32-5-amd64_x64 linux_proc_maps -p 2364


volatility --plugins=profiles -f chall.raw --profile=Linux_Debian_Squeeze_2_6_32-5-amd64_x64 linux_dump_map -p 2364 --dump-dir=dump

cd dump/
ls -l

strings task.2364.0x1a36000.vma

echo -n "KGljaGFsbApDaGFsbGVuZ2UKcDAKKGRwMQpTJ2ZsYWcnCnAyClMnYTYzOWEyMWE0YTc0NzAzZmEwNDJkNjE3NjgxYWE0NGJiNGQxYzA4YmM1ZmJmN2VmZDZiNDU1ODJiMGYwZDQwMycKcDMKc1MnaWQnCnA0CkkwCnNTJ2F1dGhvcicKcDUKUydZZ2dkcmFzaWwnCnA2CnNiLg==" | base64 -d

http://md5decrypt.net/en/Sha256/








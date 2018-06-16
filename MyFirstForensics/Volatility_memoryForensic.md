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

常用指令

看看支援那些 profiles ==> $ python vol.py –info

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

## 實務演練(1):


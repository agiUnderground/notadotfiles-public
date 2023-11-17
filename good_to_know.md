read OCSP stapling response if available:

```openssl s_client -connect stackoverflow.com:443 -status```


in case of VirtualBox stall(rshed problems, shed starvation, etc...):

```"vboxmanage modifyvm foo --hpet on" ```

send yourself a desktop notification:

```notify-send -u critical -i golang_icon.png 'summary' "It is a time to write more golang code. go1.21rc3 release is out.\nAnd this is multiline notification."```

connect to a host with a dynamic ip in a local network(knowing mac address):

```ssh $(arp | grep 00:00:00:00:00:00 | awk '{print "username@"$1;}```

poweroff the computer after N minutes(nice option if you want to close an ssh connection before that.):

```sudo shutdown -h +1```

get program memory usage(even with a picture):

```memusage -p thunar.png -T thunar```

get disasm of the symbol from the .so file:

```objdump -d /lib/x86_64-linux-gnu/libbfd-2.38-system.so | grep bfd_getb64```

get files access info in real time across the system:

```sudo /usr/sbin/opensnoop-bpfcc```

BPF tools(deb package):

```bpfcc-tools```

show aux verctor passed by kernel to the program:

```LD_SHOW_AUXV=true uname -a```

show colored diff in vim:

```diff -y asm1.s asm2.s | vim -```

`gnu c++filt` and `llvm-c++filt` - tools for c++ symbols demangling.

```https://github.com/llvm-mirror/llvm/blob/master/tools/llvm-cxxfilt/llvm-cxxfilt.cpp```

Disasm binary/so:

```alias disas='objdump -drwC -Mintel```

Custom/misc exec file formats(if you want to add detection of your custom file format without modifying a kernel):

```/proc/sys/fs/binfmt_misc/```

example:

```
~/ cat /proc/sys/fs/binfmt_misc/python3.10
enabled
interpreter /usr/bin/python3.10
flags: 
offset 0
magic 6f0d0d0a
```

llvm has it's own interpreter:

```/usr/lib/llvm-14/bin/lli --help```


`lli` directly executes programs in LLVM bitcode format. It takes a program in LLVM bitcode format and executes it using a just-in-time compiler or an interpreter.

lli is not an emulator. It will not execute IR of different architectures and it can only interpret (or JIT-compile) for the host architecture.

The JIT compiler takes the same arguments as other tools, like llc, but they don’t necessarily work for the interpreter.

If filename is not specified, then lli reads the LLVM bitcode for the program from standard input.


Get value of registers:

```sudo /usr/lib/linux-tools-5.15.0-79/perf record --intr-regs=CS```

```/usr/lib/linux-tools-5.15.0-79/perf script -F ip,sym,iregs | tail -20```

```
λ ~/perf_logs/ /usr/lib/linux-tools-5.15.0-79/perf script -F ip,sym,iregs | tail -20
 ffffffffa8027f2b vsnprintf ABI:2    CS:0x10 
     7ffbe3d1622e readlinkat ABI:2    CS:0x33 
 ffffffffa73547e5 futex_wake ABI:2    CS:0x10 
     7ffbe84d36e9 mmap_cache_get ABI:2    CS:0x33 
     55cec1e0e834 wtiNewIParam ABI:2    CS:0x33 
 ffffffffa430a1f0 do_idle ABI:1    CS:0x10 
 ffffffffa6052564 timerqueue_add ABI:1    CS:0x10 
 ffffffffa72f47a2 update_load_avg ABI:1    CS:0x10 
 ffffffffa734e641 rcu_preempt_deferred_qs ABI:1    CS:0x10 
 ffffffffa4277476 native_write_msr ABI:1    CS:0x10 
 ffffffffa7694bf5 flush_smp_call_function_queue ABI:1    CS:0x10 
 ffffffffa7d78eee menu_select ABI:1    CS:0x10 
 ffffffffa7dee805 skb_copy_bits ABI:1    CS:0x10 
 ffffffffa78b0d96 _copy_from_user ABI:2    CS:0x10 
 ffffffffa405e0c0 __get_user_8 ABI:2    CS:0x10 
     55a0561eb7c0 [unknown] ABI:2    CS:0x33 
 ffffffffa70db8ac __schedule ABI:1    CS:0x10 
 ffffffffa48dcd99 preempt_schedule_common ABI:2    CS:0x10 
 ffffffffa42e469c finish_task_switch.isra.0 ABI:2    CS:0x10 
 ffffffffa807f953 io_idle ABI:1    CS:0x10 
```

Get pid/name of the processes that hold open file descriptors for the directory:

```sudo fuser -v /```

Get mappings for io devices:

```sudo cat /proc/iomem```

```sudo cat /proc/ioports```

sudo timestamp stored at ```/var/run/sudo/ts/username```

check validity of the sudo timestamp: 

```
λ ~/ sudo pam_timestamp_check username
λ ~/ echo $?                     
7
```

check file permissions in numeric form etc:

```
stat filename
```

Get only text data from an elf section:

```
objdump -s --section .go.buildinfo vault > temp
cat temp | xxd -r
```

Forward all connections from remote 8200 port to a local 8080 port:

```ssh -L8080:localhost:8200 user@192.168.122.222 -p 22```

Explore big source code repos with a `cscope`:

```https://cscope.sourceforge.net/large_projects.html```

```/etc/skel/*``` - stores basic configs which is copied to a home dir of the newly created users.

```/usr/share/bash-completion/bash-completion``` - stores bash code for autocompletion.

```/etc/default/useradd``` - default config for the `useradd` command.

```usermod -L username``` - to lock user out of the system. It adds `!` to the `/etc/shadow` hashed password. Also use `-e 1` to set expire date.

```usermod -U username``` - unlock user.

```/proc/timer_list``` - list of the timers in the system.

```/boot/System.map-{kernel-version}``` - symbol table used by the kernel.

```nm -D pam_unix.so``` - show shared lib symbols.

```/usr/lib/x86_64-linux-gnu/security/``` - pam auth libs.

`write` - send message to another user.

`wall` - multicast message to all users.

`notify-send -u critical -i /home/user/golang_icon.png 'summary' "It is a time to write more golang code. go1.21rc3 release is out.\nAnd this is multiline notification."` - send desktop notification.


Single UNIX Specification, version 4 - `https archive d0t 0rg /details/single_unix_specification_version_4_2016_edition`

macos list shared libs - `otool -L /usr/bin/strings`

mac-o universal binaries header file - `$(xcrun --show-sdk-path)/usr/include/mach-o/fat.h`
 
machine types/cpu  types header file - `$(xcrun --show-sdk-path)/usr/include/mach/machine.h`

```
Do not stop at a first match, keep going. List all magic numbers found in a file.

user@laptop % file -k /bin/ls  
ls: Mach-O universal binary with 2 architectures: [x86_64:Mach-O 64-bit executable x86_64] [arm64e:Mach-O 64-bit executable arm64e]
ls (for architecture x86_64):	Mach-O 64-bit executable x86_64
- data
ls (for architecture arm64e):	Mach-O 64-bit executable arm64e
- data
- data
```

Show a hex dump with the offset(0x4000):
`xxd -seek 0x4000 -l 96 -c 12 /bin/ls`

Use sysctl to access hardware info about a mac:
`sysctl hw.l1icachesize`

`sysctl machdep.cpu.feature_bits`

List content of the .app applications file:
`tree -L 3 /System/Applications/Calculator.app`

Bash script, print multiline:
```
user@laptop ~ % cat <<-EOF
heredocd>   HI
heredocd>   I like Unix btw
heredocd>   And linux too btw
heredocd>   That's it.
heredocd> 
heredocd> EOF
```


print specific dom element from a page:

```js
function printDomElement(element) {
    element.classList.add("printCss");

    let printId = "printId";
    let name = ".printCss";
    let rules = "-webkit-print-color-adjust:exact;height:100%;width:100%;position:fixed;top:0;left:0;margin:0;";

    var style = document.createElement('style');
    style.id = printId;
    style.media = "print";
    document.getElementsByTagName('head')[0].appendChild(style);

    if (!(style.sheet || {}).insertRule)(style.styleSheet || style.sheet).addRule(name, rules);
    else style.sheet.insertRule(name + "{" + rules + "}", 0);

    window.print();

    setTimeout(() => {
      element.classList.remove("printCss");
      let elem = document.getElementById(printId);
      if (elem) elem.remove();
    }, 500);

  }
```

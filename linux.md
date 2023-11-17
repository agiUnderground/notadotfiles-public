Monitor device state change(detection etc):

```udevadm monitor```

Example ouput:

```
monitor will print the received events for:
UDEV - the event which udev sends out after rule processing
KERNEL - the kernel uevent

KERNEL[1200800.676000] add      /devices/pci0000:00/0000:00:19.0/usb1/1-3 (usb)
KERNEL[1200800.671000] bind     /devices/pci0000:00/0000:00:19.0/usb1/1-3/1-3:1.0 (usb)
KERNEL[1200801.677000] change   /devices/pci0000:00/0000:00:19.0/usb1/1-3/1-3:1.0/host0/target0:0:0/0:0:0:0 (scsi)
...
```


Query device attributes from udev database:

```udevadm info /dev/sdb1```


Get a filename which corresponds to the inode in /proc/locks:
```
sudo find -L /proc/1146/fd -maxdepth 1 -inum 1625 -print -exec readlink {} \;
```

lslocks - list local system locks

Really really useful and interesting stuff for profiling:
```
/sys/kernel/debug/tracing/events/
```

Monitor all hardware interrupts:
```
sudo perf trace -e hw_interrupts.received
```

Latency info(not a default tool) - `LatencyTOP`

Instantly crash the system:

```
echo c > /proc/sysrq-trigger
```

This tunable takes a value in the range [0, 100] with a default value of 20. This tunable determines how aggressively compaction is done in the background. 

```
sudo sysctl -a | grep compaction_proactiveness
```

Kill any process with a style:

```bash
sudo modprobe hwpoison-inject
sysctl -w vm.memory_failure_early_kill=1
git clone git@github.com:dwks/pagemap.git
cd pagemap
make
pidof watch  # 10144
sudo cat /proc/10144/maps # get a stack range 7ffc8da82000-7ffc8dabc000
sudo ./pagemap 10144 0x7ffc8da82000 0x7ffc8dabc000
# get first non-zero PFN - 35f848
sudo echo 0x35f848 > /sys/kernel/debug/hwpoison/corrupt-pfn
```

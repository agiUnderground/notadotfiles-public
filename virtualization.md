Create a new vm on top of KVM:

```
virt-install \
-n k8s_master \
--description “Ubuntu_22_04_server_k8s_master” \
--os-variant=ubuntu22.04 \
--ram=2048 \
--vcpus=2 \
--disk path=/var/lib/libvirt/images/k8s_master.img,bus=virtio,size=10 \
--graphics none \
--console pty,target_type=serial \
--location /home/user/ubuntu-22.04.3-live-server-amd64.iso,kernel=casper/vmlinuz,initrd=casper/initrd \
--network default,model='virtio' \
--extra-args console='ttyS0,115200n8 serial'
```


Connect to (vm) serial port using bash script instead of virsh etc:

```sudo chmod +x serial.sh```

```sudo chown :tty serial.sh```

```sudo ./serial.sh /dev/pts/3 9600```

```bash
#!/bin/bash

if [[ $# -lt 1 ]]; then
    echo "Usage:"
    echo "  femtocom <serial-port> [ <speed> [ <stty-options> ... ] ]"
    echo "  Example: $0 /dev/ttyS0 9600"
    echo "  Press Ctrl+Q to quit"
fi

set -e    # Exit when any command fails

# Save settings of current terminal to restore later
original_settings="$(stty -g)"

# Kill background process and restore terminal when this shell exits
trap 'set +e; kill "$bgPid"; stty "$original_settings"' EXIT

# Remove serial port from parameter list, so only stty settings remain
port="$1"; shift

# Set up serial port, append all remaining parameters from command line
stty -F "$port" raw -echo "$@"

# Set current terminal to pass through everything except Ctrl+Q
# * "quit undef susp undef" will disable Ctrl+\ and Ctrl+Z handling
# * "isig intr ^Q" will make Ctrl+Q send SIGINT to this script
stty raw -echo isig intr ^Q quit undef susp undef

echo "Connecting to $port. Press Ctrl+Q to exit."

# Let cat read the serial port to the screen in the background
# Capture PID of background process so it is possible to terminate it
cat "$port" & bgPid=$!

cat >"$port"   # Redirect all keyboard input to serial port

```

KVM install of FreeBSD (custom iso with a serial port):

```
virt-install \
-n freebsd_13_2_custom \
--description “Freebsd_13_2_custom” \
--os-variant=freebsd13.1 \
--ram=2048 \
--vcpus=2 \
--disk path=/var/lib/libvirt/images/freebsd_13_2_custom.img,bus=virtio,size=10 \
--graphics none \
--console pty,target_type=serial \
--cdrom /home/user/freebsd/custom_iso/FreeBSD_13_2_custom.iso \
--network default,model='virtio'
```

Customize OpenBSD ISO to support serial port:

```
apt install dvd+rw-tools
echo 'set tty com0' > boot.conf
growisofs -M install73_serial.iso -l -graft-points /etc/boot.conf=boot.conf
```

KVM install of OpenBSD(custom iso with a serial port):

```
virt-install \
--name openbsd_7_3 \
--description “OpenBSD_7_3” \
--os-variant=openbsd7.2 \
--ram=2048 \
--vcpus=2 \
--graphics none \
--disk none \
--console pty,target_type=serial \
--cdrom /home/username/openbsd/install73_serial.iso \
--network default,model='virtio' \
--disk path=/var/lib/libvirt/images/openbsd_7_3.img,bus=virtio,size=10 \
```

Run OpenBSD with a stock iso without any customizations(in terminal):

```kvm -m 1024 -cdrom install73.iso -boot d -curses```

KVM PVH mode, demo:

```
qemu-system-x86_64 -machine q35,accel=kvm \
    -m 1G \
    -smp cpus=2 \
    -kernel /home/user/pvh_kvm_test/vmlinux \
    -initrd /home/user/pvh_kvm_test/initrd.img-5.15.0-82-generic \
    -drive file=/home/user/pvh_kvm_test/rootfs.img,format=raw \
    -append 'root=/dev/sda rw console=ttyS0' -vga none -display none \
    -serial mon:stdio
```

How to create Alpine rootfs: https://github.com/firecracker-microvm/firecracker/blob/main/docs/rootfs-and-kernel-setup.md


Bhyve test(not working yet):

```bash
bhyve -ADHw -c 1 -m 1G -w -H \
        -s hostbridge \
        -s ahci-cd,/tmp/debian-live-12.2.0-amd64-standard.iso \
        -s virtio-blk,/dev/zvol/zroot/debianvm \
        -s virtio-net,tap0 \
        -s xhci,tablet \
        -l com1,/dev/nmdm0A \
        -l bootrom,/usr/local/share/uefi-firmware/BHYVE_UEFI.fd \
        debianvm
```

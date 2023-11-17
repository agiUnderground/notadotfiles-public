Monitor(read) events from device tree daemon devd:

```socat -u /var/run/devd.seqpacket.pipe /dev/ttyu0```

Example output:

```
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 " 
!system=CAM subsystem=periph type=error device=cd0 serial="QM00001" cam_status="0xcc" scsi_status=2 scsi_sense="70 02 3a 00" CDB="00 00 00 00 00 00 "
```

Switch to a different terminal(using cli):

```vidcontrol -s 1 < /dev/ttyv0```

Set normal v ttys screen size:

in /boot/loader.conf
`kern.vty=sc`

in /etc/rc.conf
`allscreens_flags="MODE_384"`

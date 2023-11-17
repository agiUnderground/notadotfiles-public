hex value to a little endian:

```
import struct
struct.pack("<I", 0x42424242)
```

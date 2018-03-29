# SFPTotal Protocol
Description of the command protocol for programmers SFPTotal


## Read and write commands

### rXYYAABBCC (RXYYAABBCC) ###

Command for reading memory of transceiver.

      r1A000007F
      Read 128 byte(s) Table 0xA0 from 0x00


            00  01  02  03  04  05  06  07  08  09  0A  0B  0C  0D  0E  0F

      00 :  03  04  07  20  00  00  00  00  00  00  00  06  67  00  0A  64
      01 :  00  00  00  00  4F  45  4D  20  20  20  20  20  20  20  20  20
      02 :  00  20  20  20  00  00  00  00  31  30  47  42  2D  53  46  50
      03 :  2D  4C  52  2D  45  20  20  20  31  2E  30  20  05  1E  00  F9
      04 :  00  1A  00  00  45  58  50  39  36  4C  30  31  31  20  20  20
      05 :  20  20  20  20  31  31  30  38  30  39  20  20  68  F0  03  02
      06 :  45  58  54  52  45  4D  45  20  4C  52  00  00  00  00  00  00
      07 :  00  00  00  00  00  00  00  00  00  00  00  00  00  00  00  00

      R1A000007F  
      03040720000000000000000667000A64000000004F454D202020202020202020
      0020202000000000313047422D5346502D4C522D45202020312E3020051E00F9
      001A000045585039364C30313120202020202020313130383039202068F00302
      45585452454D45204C5200000000000000000000000000000000000000000000



### wXYYAABBCC (WXYYAABBCC)
Command for writing to the memory of transceiver.

w — (1 byte) — Write command. Symbol register is responsible for the subsequent read after write. If you use uppercase (W) after the recording is complete programmer will make reading the memory area which has been overwritten. To write without return a write result of lower case (w) must be used.

X — (1 byte) — Transceiver type (1 - SFP, 2 - SFP+).

YY — (2 bytes) — The device address on the I2C bus.

AA — (2 bytes) — Address of additional table.

BB — (2 bytes) — Address table. Value in HEX. For example: A0 or A2.

СС — (2 bytes) — Write byte count. Hexadecimal value reduced by one. For example, for writing 128 bytes you should set this parameter in 7F (0x7F in HEX, 127 in decimal).

{DATA} — Write data in HEX, 2 characters for each byte of the parcel.


Examples

Write code 128 bytes in Table A0 Upper address 00 for SFP transceiver:

      W1A000007F
      03040720000000000000000667000A64000000004F454D202020202020202020
      0020202000000000313047422D5346502D4C522D45202020312E3020051E00F9
      001A000045585039364C30313120202020202020313130383039202068F00302
      45585452454D45204C5200000000000000000000000000000000000000000000
      
Write password 0123 (HEX: 30h 31h 32h 33h) in Table A2 address 7B for SFP+ transceiver:

      w2A2007B0330313233
      
Note: Write command should type without newline characters and spaces. Shifts are given for the convenience display of the material in the examples.

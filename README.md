First use the parse_modem.py to determine the physical start point of MAIN
Then strip the modem.bin to the MAIN's start

```Bash
python3 parse_modem.py modem.bin

dd if=modem.bin of=modem_MAIN_40010000.bin bs=1 skip=$((MAIN_START)) count=$((MAIN_LENTH))
# MAIN_START is the offset of MAIN from previous output
# MAIN_LENGTH is the size of MAIN from previous output
# For example:
# TOC Name: b'MAIN\x00\x00\x00\x00\x00\x00\x00\x00'
# Load address: 0x40010000
# Offset: 0x00003bc0
# Size: 0x03d00774
# Unk: 0x4ca55a7d
# ID: 2
# Final command should be: dd if=modem.bin of=modem_MAIN_40010000.bin bs=1 skip=$((0x00003bc0)) count=$((0x03d00774))

python3 decoder.py modem_MAIN_40010000.bin btl.btl
```

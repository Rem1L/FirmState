First use the parse_modem.py to determine the physical start point of MAIN
Then strip the modem.bin to the MAIN's start

````
python3 parse_modem.py modem.bin
dd if=modem.bin of=modem_MAIN_40010000.bin bs=1 skip=$((MAIN_START)) count=$((MAIN_LENTH))
python3 decoder modem_MAIN_40010000.bin btl.btl
````
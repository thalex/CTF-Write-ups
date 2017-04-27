# picoCTF: For: Connect The Wigle

**Category:** Forensics
**Points:** 140
**Description:**

> Identify the data contained within [wigle](https://github.com/dbaser/CTF-Write-ups/blob/master/picoCTF-2017/for140-connect_the_wigle/wigle) and determine how to visualize it.

**Hints:**

> Perhaps they've been storing data in a database. How do we access the information?

> How can we visualize this data? Maybe we just need to take a step back to get the big picture?

> Try zero in the first word of the flag, if you think it's an O.

## Write-up

let´s see what the type of [file](https://github.com/dbaser/CTF-Write-ups/blob/master/picoCTF-2017/for140-connect_the_wigle/wigle)

let´s extract the **Leftover Capture Data** with `tshark`

```bash
[dbaser@pwn4food]$ tshark -r data.pcap -T fields -e usb.capdata

00:00:09:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0f:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0a:00:00:00:00:00
00:00:00:00:00:00:00:00
20:00:00:00:00:00:00:00
20:00:2f:00:00:00:00:00
20:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:13:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
...
```    

we need only numbers without zeros and separators

```bash
[dbaser@pwn4food]$ tshark -r data.pcap -T fields -e usb.capdata
 | awk -F: '{print $3}' | grep -v 00 

09
0f
04
0a
2f
13
15
20
22
22
2d
27
11
...
```   

on the [pdf](http://www.usb.org/developers/hidpage/Hut1_12v2.pdf?) (Page 53), we have a key map of a USB Keyboard, just convert the output data with the key map

![keymap](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/picoCTF-2017/for80-just_keyp_trying/for80-just_keyp_trying-02.png)

but wait motherfucker! we have 29 lines of data, let's use a python script to do the work for us! :D

```python
#!/usr/bin/python
mappings = {
        0x04:"A",
        0x05:"B",
        0x06:"C",
        0x07:"D",
        0x08:"E",
        0x09:"F",
        0x0A:"G",
        0x0B:"H",
        0x0C:"I",
        0x0D:"J",
        0x0E:"K",
        0x0F:"L",
        0x10:"M",
        0x11:"N",
        0x12:"O",
        0x13:"P",
        0x14:"Q",
        0x15:"R",
        0x16:"S",
        0x17:"T",
        0x18:"U",
        0x19:"V",
        0x1A:"W",
        0x1B:"X",
        0x1C:"Y",
        0x1D:"Z",
        0x1E:"1",
        0x1F:"2",
        0x20:"3",
        0x21:"4",
        0x22:"5",
        0x23:"6",
        0x24:"7",
        0x25:"8",
        0x26:"9",
        0x27:"0",
        0x28:"\n",
        0x2C:" ",
        0x2D:"-",
        0x2E:"=",
        0x2F:"[",
        0x30:"]"
        }
 
nums = []
keys = open('data.txt')
for line in keys:
        nums.append(int(line.strip(),16))
keys.close()
 
output = ""
for n in nums:
        if n in mappings:
                output += mappings[n]
        else:
                output += 'x'
 
print 'output :' + output
```
run the script and get the flag!

```bash
[dbaser@pwn4food]$ python usbkeymap1.py
output :FLAG[PR355-0NWARDS-C98CCF99]C
```   
The flag is: `FLAG[PR355-0NWARDS-C98CCF99]`

## Update

When I was writing this write-up, I found this [script](https://github.com/dbaser/CTF-Write-ups/blob/master/picoCTF-2017/for80-just_keyp_trying/usbkeymap2.py) from this [write-up](https://webstersprodigy.net/2012/11/09/csaw-2012-quals-tutorialwriteup/) that do the same job just by specifying the pcap file in the script.
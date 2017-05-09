# Cryptorave: For: Maria strikes back

**Category:** Forensics
**Points:** 150
**Description:**

> Maria was fired from the company from which she was caught leaking data. She didn't learn the lesson. Now, Maria has met Sandrinha and they're planning something under the covers. The sysadmin took a [dump](https://github.com/dbaser/CTF-Write-ups/blob/master/CryptoRave-2017/for150-maria_strikes_back/logs.pcap) from the network from one of their hosts. See if you can find something. 

## Write-up

after several analysis on pcap file, we found a strange PC conversation in the port 1337, let's apply a filter `tcp.port eq 1337` to limit this conversation and `Follow TCP Stream` to read this entire conversation

![img](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/CryptoRave-2017/for150-maria_strikes_back/for150-maria_strikes_back-01.png)

looks like a convesartion with `Maria` and `Sandrinha`, we need to find what `Maria` tryed to sent to `Sandrinha`

![img](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/CryptoRave-2017/for150-maria_strikes_back/for150-maria_strikes_back-02.png)

hmm, found a JPEG signature in the packets, let's `Follow TCP Stream` again!

![img](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/CryptoRave-2017/for150-maria_strikes_back/for150-maria_strikes_back-03.png)

and save the data in raw format to view the file

![img](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/CryptoRave-2017/for150-maria_strikes_back/for150-maria_strikes_back-04.png)

we have a img file of the "new haircut" of Maria, let's analyze the file to find any clue for the flag

![img](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/CryptoRave-2017/for150-maria_strikes_back/img.jpeg)

trying analisys with common tool like strings, binwalk and stegsolve and nothing, but wait! there is a clue in this conversation with 'Maria' and 'Sandrinha', look with more attention, it looks like a password, right?

![img](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/CryptoRave-2017/for150-maria_strikes_back/img.jpeg)

so, let's try steghide tool with the possible password

```bash
[dbaser@pwn4food]$ steghide extract -sf img.jpeg
Enter passphrase: 
wrote extracted data to "flag.zip".
```   

yes! I was right! there is a file inside this img, but is protect with a password. let's bruteforce the zip file with 'fcrackzip' tool

```bash
[dbaser@pwn4food]$ fcrackzip -v -u -D -p /usr/share/wordlists/rockyou.txt flag.zip
found file 'flag.txt', (size cp/uc     48/    36, flags 9, chk 5c64)
PASSWORD FOUND!!!!: pw == ******
```   

unzip the file and get the flag!


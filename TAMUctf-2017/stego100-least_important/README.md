# TAMUctf: Stego100: Least Important


**Category:** Steganography
**Points:** 100
**Solves:** 111
**Description:**

> People say that this challenge is not important. In other words, it may be the least significant!

## Write-up

let's see what's the type of the [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/stego100-least_important/39e5b7d2b46fddf6)


```bash
$ file 39e5b7d2b46fddf6 

39e5b7d2b46fddf6: PC bitmap, Windows 3.x format, 2988 x 1573 x 24
```    

the description given us a hint: [**least significant**](https://en.wikipedia.org/wiki/Least_significant_bit), let's run `zsteg` tool

```bash
$ zsteg -a 39e5b7d2b46fddf6 | grep -i gigem

b1,rgb,lsb,xy       .. text: "58:gigem{this_is_pretty_significant_success_
f2df944768204c64}ch"

```    

The flag is: `gigem{this_is_pretty_significant_success_f2df944768204c64}`

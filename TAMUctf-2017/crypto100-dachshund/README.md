# TAMUctf: Crypto: Dachshund


**Category:** Cryptography
**Points:** 100
**Solves:** 66
**Description:**

> Attacking this challenge with a dachshund is your best bet at winning.

## Write-up

let's see what's the type of the [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/crypto100-dachshund/df5e76dedfe9afc0)

```bash
$ file df5e76dedfe9afc0 

df5e76dedfe9afc0: ASCII text, with very long lines
```    

the content of the file given us the `n` (modulus), `e` (public exponent) and `c` (cyphertext)

```bash
$ cat df5e76dedfe9afc0 

C: AR/ar3SualKVNKXZ4ox9JNlajNxTAhRRwI09n/F5LaL066s0LPZPdwwnU5r5h6oC2o2AS6vtEOwuORqaQpGhh1c2hgl3CDKk1nhJ44etjnWkHkAmuTnoSYIPBp+Di7+KBK84ll7tPA1Vd+1jRPa0MGxIxXYoQb6Rvvz7K9FdHSx8
e: MzY3MTgyMDc5NDYzMjY5NDg2OTg3MDcyODc2OTg0MzE0MDM3NDg2OTA2Mjg4OTk3NTI1OTQ3MDUwOTkzNTIwNjcxNjA1NjI4MjY0MDYwMTM3Mjg4MjE4OTc2NDQ4MzkwMjEwOTQyMDYzNDM3NjAyMzc2MTk4Mjk2NTc5NjkxNDI0ODg4ODIwMDUwNDYyMTE1MTYyODMzNzY2NjUxODYxOTA1OTM3MDYxMDc2MzYzMzc5NTQ4OTIzMzE2ODgwNjIwOTc4ODg0MDkxNjM0NzExNTExMjgwOTMwNzA5MDY0MTg0MjkzMzE5NDYxMTIzMTIyNDM3MDU1NjIxOTk4ODk1OTkwNzIyMjY1NjA1OTE2MDcwMDUxMzA1MTQwNDc3MjM3MzA2MDAyMzM4OTk1MzAwNjg3NDkx
N: NDY0NTE3NDY1NDA2Nzg1OTUzODU3NTU2NDU3NjQ5NTMxOTUwMjkzNzkyNDY5NzI5NzU5Njc1MDc1NzM1MTU2MDUxMjgxNjI5NjcwNzk3OTIyNTM5NzUyODc1ODk1NTQ2MDAyNTc4MDg3NjgxNjcwNzAzMTEwNjYxMDc4NjcxMjg2ODYxNDQzMjUwNTc5Mzg2MzU0MjQ2MjY1NTU4MjcxNTU5MDM4MTYxNTI1ODExNjU5MjAzMDcyODY2MTgzNjYzNjQzMjU1MTYzMjAxMDc4NjY1Mjg4ODk4MDQzNjYyOTc4NjQ5MjYzMzc3OTUwOTQzMDU5MTE0MDE5MDM5OTI0MjM3NjczNzExNTE1MTcyMjAzNDcxNTQyNTQzODI1Mzg1NzQ0ODc4MDc0MzU4NTU3MTg5Mzcz
```    



after google, we found this [write-up](http://capturetheswag.blogspot.com.br/2015/04/bctf-2015-warmup-crypto-challenge.html) with the solution to this chall, only replace `n`, `e` and `c`.

final script! we have to convert `n` and `e` from base64 to ascii and `c` from base64 to hex

{% gist e19d0853f9fb8f7721e8ad40531454e0 %}

run the script! (don't forget to clone this [repo](https://github.com/pablocelayes/rsa-wiener-attack) before running the script)

```bash 
$ python rsa.py  

Performing Wiener's attack. Don't Laugh...
d=34423659517451757817217793949772913434630556566965109599840482542632279361311
So the flag is:
gigem{h0Tdogs_85faf27b642d2f94}
```

The flag is: `gigem{h0Tdogs_85faf27b642d2f94}`
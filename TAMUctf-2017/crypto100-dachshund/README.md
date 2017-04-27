# TAMUctf: Crypto: Dachshund

**Solved by** @dbaser and @shrimpgo
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

the content of the file given us the `n` (modulus), `e` (public exponent) and `c` (cyphertext), RSA crypto here.

```bash
$ cat df5e76dedfe9afc0 

C: AR/ar3SualKVNKXZ4ox9JNlajNxTAhRRwI09n/F5LaL066s0LPZPdwwnU5r5h6o...
e: MzY3MTgyMDc5NDYzMjY5NDg2OTg3MDcyODc2OTg0MzE0MDM3NDg2OTA2Mjg4OTk...
N: NDY0NTE3NDY1NDA2Nzg1OTUzODU3NTU2NDU3NjQ5NTMxOTUwMjkzNzkyNDY5NzI...
```    

ok, after searching for dachshund on google, we found a hint for the attack type, because de nickname from de dachshund is "Wiener-Dog" 

![crypto100-dachsund.png](https://github.com/dbaser/CTF-Write-ups/blob/master/TAMUctf-2017/crypto100-dachshund/crypto100-dachsund.png)

![dachshund.jpg](https://github.com/dbaser/CTF-Write-ups/blob/master/TAMUctf-2017/crypto100-dachshund/dachshund.jpg)

there are some of types of [attacks](https://github.com/Ganapati/RsaCtfTool)

Attacks :

* Weak public key factorization
* **Wiener's attack** (*wiener-dog!*)
* Hastad's attack (Small exponent attack)
* Small q (q<100,000)
* Common factor between ciphertext and modulus attack
* Fermat's factorisation for close p and q
* Gimmicky Primes method
* Past CTF Primes method
* Self-Initializing Quadratic Sieve (SIQS) using Yafu
* Common factor attacks across multiple keys

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
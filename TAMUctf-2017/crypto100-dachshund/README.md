# TAMUctf: Crypto: Dachshund

**Solved by:** @dbaser and @shrimpgo
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

![crypto100-dachsund.png](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/TAMUctf-2017/crypto100-dachshund/crypto100-dachsund.png)

![dachshund.jpg](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/TAMUctf-2017/crypto100-dachshund/dachshund.jpg)

there are some of types of [attacks:](https://github.com/Ganapati/RsaCtfTool)

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

```python
#!/usr/bin/python  
import ContinuedFractions, Arithmetic, RSAvulnerableKeyGenerator
import time  
import sys  
import base64  
import binascii  
import gmpy  
import sympy  
import math  
import fractions  
import struct  
sys.setrecursionlimit(100000)  
# modulus from the RSA public key  
n=464517465406785953857556457649531950293792469729759675075735156051281629670797922539752875895546002578087681670703110661078671286861443250579386354246265558271559038161525811659203072866183663643255163201078665288898043662978649263377950943059114019039924237673711515172203471542543825385744878074358557189373  
# exponent from the RSA public key  
e=367182079463269486987072876984314037486906288997525947050993520671605628264060137288218976448390210942063437602376198296579691424888820050462115162833766651861905937061076363379548923316880620978884091634711511280930709064184293319461123122437055621998895990722265605916070051305140477237306002338995300687491  
# cyphertext converted to hex
c=0x011fdaaf74ae6a529534a5d9e28c7d24d95a8cdc53021451c08d3d9ff1792da2f4ebab342cf64f770c27539af987aa02da8d804babed10ec2e391a9a4291a18757368609770832a4d67849e387ad8e75a41e4026b939e849820f069f838bbf8a04af38965eed3c0d5577ed6344f6b4306c48c5762841be91befcfb2bd15d1d2c7c  
def hack_RSA(e,n):  
 print "Performing Wiener's attack. Don't Laugh..."  
 time.sleep(1)  
 frac = ContinuedFractions.rational_to_contfrac(e, n)  
 convergents = ContinuedFractions.convergents_from_contfrac(frac)  
 for (k,d) in convergents:  
   #check if d is actually the key  
   if k!=0 and (e*d-1)%k == 0:  
     phi = (e*d-1)//k  
     s = n - phi + 1  
     # check if the equation x^2 - s*x + n = 0  
     # has integer roots  
     discr = s*s - 4*n  
     if(discr>=0):  
       t = Arithmetic.is_perfect_square(discr)  
       if t!=-1 and (s+t)%2==0:  
         return d  
hacked_d = hack_RSA(e, n)  
print "d=" + str(hacked_d)  
m = pow(c, hacked_d, n)  
print "So the flag is:"  
print("%0512x" %m).decode("hex")  
```

run the script and don't forget to clone this [repo](https://github.com/pablocelayes/rsa-wiener-attack) before running the script

```bash 
$ python rsa.py  

Performing Wiener's attack. Don't Laugh...
d=34423659517451757817217793949772913434630556566965109599840482542632279361311
So the flag is:
gigem{h0Tdogs_85faf27b642d2f94}
```

The flag is: `gigem{h0Tdogs_85faf27b642d2f94}`
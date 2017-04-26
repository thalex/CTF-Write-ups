# TAMUctf: Stego100: Ghost Busters


**Category:** Steganography
**Points:** 100
**Solves:** 107
**Description:**

> Paul Combetta was apprehended at a French airport. Federal officials seized his laptop and found this audio file along with a link to a facebook profile http://facebook.com/profile.php?=73322363.

> There may be a classified code word hidden this file. Can you find it?

## Write-up

let´s see what the type of [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/stego100-jpeg_ocean/5bcf0846dd3cf595)

```bash
$ file 5bcf0846dd3cf595
    
5bcf0846dd3cf595: PC bitmap, Windows 3.x format, 440 x 440 x 32
```    

run the `stegsolve` to see the flag!

```bash
$ java -jar stegsolve.jar  
```

![stego100-jpeg_ocean-01.png](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/stego100-jpeg_ocean/stego100-jpeg_ocean-01.png)

The flag is: `gigem{water_w0rld_c4ae306239e48Be5}`
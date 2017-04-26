# TAMUctf: Stego100: JPEG Ocean

**Category:** Steganography
**Points:** 100
**Solves:** 264
**Description:**

> This picture was found on a high level target's computer. Analysts did a quick examination but could not find anything.
however, Nicholas Cage told us that the target may have used a method of message hiding similar to the method used on the back of the constitution.
The text could essentially be hiding in plain sight.

## Write-up

let´s see what the type of [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/stego100-jpeg_ocean/5bcf0846dd3cf595)

```bash
$ file 5bcf0846dd3cf595
    
5bcf0846dd3cf595: PC bitmap, Windows 3.x format, 440 x 440 x 32
```    

let's run the `stegsolve` tool to find the flag!

```bash
$ java -jar stegsolve.jar  
```

![stego100-jpeg_ocean-01.png](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/stego100-jpeg_ocean/stego100-jpeg_ocean-01.png)

The flag is: `gigem{water_w0rld_c4ae306239e48Be5}`

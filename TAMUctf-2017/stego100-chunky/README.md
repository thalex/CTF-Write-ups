# TAMUctf: Stego100: Chunky

**Category:** Steganography
**Points:** 100
**Solves:** 193
**Description:**

> https://www.youtube.com/watch?v=oacaq_1TkMU

## Write-up

let´s check the [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/stego100-chunky/ab5a0fcd1ff0ed04.png) with strings!

```bash
$ strings ab5a0fcd1ff0ed04.png | grep -i flag -A 1

HfLAgZ2lnZW17dGhlX2ZsYWdfdGhhdF9lYXRzX2xpa2VfYV9tZW
FsXzE0NTBkYmJlM2ZhOTQ2ODN96;IDATx
```    

extract the code after `fLAg` and before `;IDATx` and convert from base64 to ascii

```bash
$ echo "Z2lnZW17dGhlX2ZsYWdfdGhhdF9lYXRzX2xpa2VfYV9tZWFsXzE0NTBkYmJlM2ZhOTQ2ODN96" | base64 -d

gigem{the_flag_that_eats_like_a_meal_1450dbbe3fa94683}base64: invalid input
```

The flag is: `gigem{the_flag_that_eats_like_a_meal_1450dbbe3fa94683}`



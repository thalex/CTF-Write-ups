# TAMUctf: Stego100: Ghost Busters


**Category:** Steganography
**Points:** 100
**Solves:** 107
**Description:**

> Paul Combetta was apprehended at a French airport. Federal officials seized his laptop and found this audio file along with a link to a facebook profile http://facebook.com/profile.php?=73322363.

> There may be a classified code word hidden this file. Can you find it?

## Write-up

let´s see what the type of [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/stego100-ghost_busters/62beccfce5806775)

```bash
$ file 62beccfce5806775

62beccfce5806775: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 44100 Hz
```    

let's open the audio file with [Sonic Visualiser](http://www.sonicvisualiser.org/) and apply `Spectogram` filter

![stego100-ghost_busters-01.png)](https://raw.githubusercontent.com/dbaser/ctfs/master/TAMUctf-2017/stego100-ghost_busters/stego100-ghost_busters-01.png)

![stego100-ghost_busters-02.png)](https://raw.githubusercontent.com/dbaser/ctfs/master/TAMUctf-2017/stego100-ghost_busters/stego100-ghost_busters-01.png)

The flag is: `gigem{now_you_see_me_7e22995b5a3ae7fd}`

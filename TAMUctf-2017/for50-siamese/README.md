# TAMUctf: Stego50: Siamese

Stego - 50 Points (324 solves)

> The internet loves cats. Whats not to love?

## Write-up

let´s see what the type of [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/for50-siamese/8ff4da2f7368f800)

```bash
$ file 8ff4da2f7368f800
    
8ff4da2f7368f800: GIF image data, version 89a, 320 x 180
```    

run the binwalk to see hide files...

```bash
$ binwalk 8ff4da2f7368f800  
    
DECIMAL       HEXADECIMAL     DESCRIPTION
---------------------------------------------------------------------------
    0             0x0             GIF image data, version "89a", 320 x 180
    662419        0xA1B93         MySQL MISAM index file Version 10
    3204803       0x30E6C3        Zip archive data, at least v1.0
    3205027       0x30E7A3        End of Zip archive
```

... and extract the zip file with dcfldd

```bash
$ dcfldd if=8ff4da2f7368f800 bs=1 skip=3204803 of=file.zip

0 bs=1 skip=3204803 of=file.zip

246+0 records in
246+0 records out
```

unzip and cat the file!

```bash
$ unzip file.zip 

Archive:  file.zip
 extracting: 8ff4da2f7368f800.txt    

$ cat 8ff4da2f7368f800.txt | base64 -d

gigem{the_cat_goes_meow_3b96b806f6515c23}

```

the flag is: gigem{the_cat_goes_meow_3b96b806f6515c23}

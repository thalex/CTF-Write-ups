# picoCTF: For: Connect The Wigle

**Category:** Forensics
**Points:** 140
**Description:**

> Identify the data contained within [wigle](https://github.com/dbaser/CTF-Write-ups/blob/master/picoCTF-2017/for140-connect_the_wigle/wigle) and determine how to visualize it.

**Hints:**

> Perhaps they've been storing data in a database. How do we access the information?

> How can we visualize this data? Maybe we just need to take a step back to get the big picture?

> Try zero in the first word of the flag, if you think it's an O.

## Write-up

let's see what's the type of the [file](https://github.com/dbaser/CTF-Write-ups/blob/master/picoCTF-2017/for140-connect_the_wigle/wigle)

```bash
[dbaser@pwn4food:~]$ file wigle
wigle: SQLite 3.x database, last written using SQLite version 3008007
```    
hmm.. we need to explore the sql tables...

```bash
[dbaser@pwn4food:~]$ sqlite3 wigle .table
android_metadata  location          network 

[dbaser@pwn4food]$ sqlite3 wigle "select * from location;" 
0|fd:36:40:7f:3b:5e|-94|-4.0|-1.96|140.0|16.0|1490954696
1|5d:01:67:ca:14:77|-90|-3.99|-1.96|151.0|12.0|1490968400
2|59:9d:a9:66:82:0d|-91|-3.98|-1.96|141.0|6.0|1490956491
3|59:37:74:f0:9d:49|-88|-3.98|-1.955|133.0|6.0|1490955013
4|98:4f:c1:8f:bf:33|-91|-3.98|-1.95|131.0|6.0|1490960781
5|9e:fe:92:99:a7:df|-73|-3.97|-1.96|141.0|4.0|1490962139
6|c8:a4:3c:2a:f4:88|-80|-3.96|-1.96|136.0|6.0|1490968726
7|81:6c:9b:66:06:ab|-81|-3.96|-1.95|142.0|4.0|1490966713
...
```
...and extract latitude, longitude and changing the separator `|` to `,` with awk

```bash
[dbaser@pwn4food:~]$ sqlite3 wigle "select lat,lon from location;" | awk -F'|' 'BEGIN{OFS=",";} {print $1,$2}' 
-4.0,-1.96
-3.99,-1.96
-3.98,-1.96
-3.98,-1.955
-3.98,-1.95
-3.97,-1.96
-3.96,-1.96
...
```

just copy and paste the results from the last command in this [site](http://www.hamstermap.com/quickmap.php) (tks @intrd 4 the site) and get the flag!

![flag](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/picoCTF-2017/for140-connect_the_wigle/for140-connect_the_wigle.png)

The flag is: `FLAG{FOUND_M3_9114AFFC}`

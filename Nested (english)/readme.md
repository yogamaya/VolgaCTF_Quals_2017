<h1>Nested</h1>

There are too many bytes to be a simple transfer... can you investigate this?
dump.7z

Hints

1. Take a look at the source format and continue making y**our guess**es
2. gzsteg


Downloading dump.7z archive. It contains only one *.pcap file. Open it in Wireshark.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-29-34.png)

Nothing special. Let's search other file signatures in dump.pcap.

Opening dump.pcap in BLESS (or other HEX-editor). In this file we have a chance to find 7zip signature.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-32-14.png)

Extracting files.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-37-04.png)

Looking at extracted files: each.jpg and other.zip helps us to suppose that this files are dependent from each other.

After that we are looking for steganography utilities and remmeber task hint (y**our guess**es), so we understand that OutGuess is needed.

OutGuess installing.

Running command:

`outguess -k "other" -r each.jpg hidden.txt`

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-38-17.png)

Password for the other.zip:

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-38-48.png)

Extracting file is a gz-archive.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-39-40.png)

At this moment you should remember the 2d hint - gzsteg. This is a name of stegapower patch for gzip (v 1.2.4).
Downloading the source code, patching that with gzsteg-patch.

`patch -c < patch1
patch -c < patch2
patch -c < patch3`

Patch adds new option to standard gzip: "-s" or "--steg", which provides hiding/revealing of files into archive.

With the next command extracting hidden file:

`gzip -cds hide.txt hide.gz`

There is flag in hide.txt.

![screenshot of sample](https://github.com/yogamaya/VolgaCTF_Quals_2017/blob/master/other/Screenshot%20from%202017-03-27%2013-42-17.png)

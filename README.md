familytreemaker
===============

This program creates family tree graphs from simple text files.

The input file format is very simple, you describe persons of your family line
by line, children just have to follow parents in the file. Persons can be
repeated as long as they keep the same name or id. An example is given in the
file `LouisXIVfamily.txt` (you can create your own seperate file in this case like what I did but I have not committed this info).

Note: This branch version is optimized for chinese (and has been further modified). If other language for 
      input text file is used, command option gender (-g) has to be used to
      specify words of male and female, since their default values are set
      as "男" and "女" instead of origin "M" and "F".  

Credits to: Adrien Vergé and Bodhi Wang

Installation
------------

Simply clone the repo or install package familytree by pip as shown below:
```bash
pip install familytree
```

This script outputs a graph descriptor in DOT format. To make the image
containing the graph, you will need a graph drawer such as [GraphViz] [1].

[1]: http://www.graphviz.org/  "GraphViz"

Usage
-----
```
usage: familytreemaker.py [-h] [-a ANCESTOR] [-g GENDER] [-v INFOLEVEL]
                          [-o OUTFILE]
                          INPUTFILE

Generates a family tree graph from a simple text file

positional arguments:
  INPUTFILE     the formatted text file representing the family

optional arguments:
  -h, --help    show this help message and exit
  -a ANCESTOR   make the family tree from an ancestor (if omitted, the program
                will try to find an ancestor)
  -g GENDER     customized gender string, for example: "男,女" or "M,F"
  -v INFOLEVEL  Information level (0/1/2) to output. (0 - only name and
                surfname will be output; 1 - time of birthday and deathday
                will be invisable; 2 - all information will be output)
  -o OUTFILE    file name for output
```

The sample family descriptor `LouisXIVfamily.txt` is here to show you the
usage. Simply run:
```
python familytreemaker.py -a "王灿文" -v2 -o LouisXIVfamily.dot LouisXIVfamily.txt && \
    dot -Tsvg -o LouisXIVfamily.svg LouisXIVfamily.dot
```

If package familytree has been installed by pip, commands below can be performed to populate:
```bash
python -m familytree.familytreemaker -a "王灿文" -v2 -o LouisXIVfamily.dot LouisXIVfamily.txt && \
    dot -Tsvg -o LouisXIVfamily.svg LouisXIVfamily.dot
``` 

\* if code fails to run, try omitting the quotes in the name (i.e. `"王灿文"` -> `王灿文`

It will generate the tree from the infos in `LouisXIVfamily.txt`, starting from
*王灿文* and saving the image in `LouisXIVfamily.svg`.

![result: LouisXIVfamily.svg](./LouisXIVfamily.svg)

## Prerequisites

* Python 3.x < 3.10
* [GraphViz](https://graphviz.org/) (installing through `pip`, compiling from source or the provided `.msi` is fine.)
* Notepad++ (recommended, but not necessary, for `utf-8` and `ANSI` support).
* Windows Chinese Language Pack
* Registry change for Windows 10 (if you use US/UK English as a default language).
    * Add string `Autorun` with value `chpc 936` for Simplified Chinese (SG/Chinese) on command prompt startup
    * Reopen cmd

![image](https://user-images.githubusercontent.com/48358569/142719316-e1c54965-c99a-4970-81e6-3e372b99d81a.png)

![image](https://user-images.githubusercontent.com/48358569/142719435-dfb5c676-4d8e-463a-a71d-bf2938eda2c2.png)

    
## Notes

- May have to change encoding scheme (possible if using Notepad++) as per this article: https://community.notepad-plus-plus.org/topic/17226/wrong-encoding
- If one inserts 4 or more generations, tree might get unbalanced and so lines might not look aesthetic.


## Modifications to original
- Remove surname suffix at end of the name (i.e. `《陈》`)
- Change main styling of line to `ortho` (takes the "family tree" shape more) to allow for more generations

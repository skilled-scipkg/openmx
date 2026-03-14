<a id="SECTION000730000000000000000"></a>
# Output of large-sized files in binary mode

Large-scale calculations produce large-sized files in text mode such as cube files.
The IO access to output such files can be very time consuming in machines of which IO
access is not fast. In such a case, it is better to output those large-sized files in
binary mode. The procedure is supported by the following keyword:

```text

  OutData.bin.flag    on    # default=off, on|off
```

Then, all large-sized files will be output in binary mode.
The default is 'off'.

The output binary files are converted using a small code 'bin2txt.c' stored in the directory 'source'
which can be compiled as

```text

  gcc bin2txt.c -lm -o bin2txt
```

As a post processing, you will be able to convert as

```text

  ./bin2txt *.bin
```

The functionality will be useful for machines of which IO access is not fast.

---

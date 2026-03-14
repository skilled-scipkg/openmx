<a id="SECTION000116000000000000000"></a>
## Specification of a directory storing PAO and VPS files

<a id="664"></a>
The path to the VPS and PAO directories can be specified in your input file by the following keyword:

```text

    DATA.PATH    ../DFT_DATA19    # default=../DFT_DATA19
```

Both the absolute and relative specifications are possible.
PAO files in a database should not be used for the VPS in other databases,
since semicore states included in several elements are different from each other.
So, the consistency in the version of PAO and VPS must be kept.
For that reason, it would be better to store PAO and VPS files of
each version in different directories. In this case, the keyword is useful.

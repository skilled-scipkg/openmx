<a id="SECTION000188000000000000000"></a>
<a id="sec:md2axsf"></a>
## Converting the file format: md2axsf

In molecular dynamics simulations or geometry optimization, '*System.Name*.md' is generated
to save a series of structural change. Although '*System.Name*.md' being the xyz format can be read
in [[152](bibliography.md#YTL-OpenMX-Viewer),[151](bibliography.md#OpenMX-Viewer)] and XCrySDen [[105](bibliography.md#XCrySDen)], the copied cell in periodic systems
cannot be displayed in XCrySDen.
For such a purpose, a small post processing code is available to convert the format from 'xyz' to 'axsf'.
The first step to do that is to compile 'md2axsf.c' as

```text

    % gcc md2axsf.c -lm -o md2axsf
```

Then, you can convert a '*System.Name*.md' file as

```text

    % ./md2axsf System.Name.md System.Name.axsf
```

The '*System.Name*.axsf' file can be analyzed by using XCrySDen and other software.

---

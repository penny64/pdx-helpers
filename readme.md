# PDX Helpers

This document outlines a collection of utilities designed to assist in the management of PDX files, including pdxhtml which generates a static website after json data is generated

### Screenshots

![Mobile View](mobile.png)

![Desktop View](desktop.png)

### pdxrename

```
Usage: pdxrename [-h] [-d <directory>] [-r] [file]
Renames zipped pdx files to match their pdxinfo file.
Also deletes any __MACOSX folders.
You should run this on any collection you want to tag.

-d directory: Process all pdx files in the specified directory.
-r: Recursively process all pdx files in the specified directory and subdirectories. Must be used with -d.
file: Process a specific pdx file.

```

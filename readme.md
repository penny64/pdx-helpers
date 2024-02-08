# PDX Helpers
A collection of bash scripts to assist in the management and archival of PDX files, including pdxhtml which generates a static (but responsive!) webpage after json data is generated

## Screenshots

![Mobile View](mobile.png)

![Desktop View](desktop.png)

## Utilities

### zip_pdx

```
Usage: zip_pdx <dir> [-s]
Zips every pdx in a directory
Options:
  -s    Single fire at target dir
  -h    Display this help message

```


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

### pdxtag

```
Usage: pdxtag [-r] <directory> <output_file>
Generate a JSON array containing pdx data
Example: pdxtag -r . index
  -r                Recursively process files in the directory
  <directory>       Directory to process
  <output_file>     JSON output file
```

### pdxhtml

```
Usage: pdxhtml [OPTION]... [FILE]
Generate a PDX index page from PDX JSON data

  -h, --help       Display this help and exit
  -i, --input      Specify input JSON file (mandatory)
  -o, --output     Specify output HTML file. Defaults to games.html if unspecified

Example:
  ./pdxhtml --input games.json --output games.html
```

## Usage

Requires a modern version of bash, jq, GNU grep and GNU parallel. Only tested on Linux.

Get roms ready for processing with pdxrename- examine error output to determine if any repairs are needed

```
[penny@cake archives]$ pdxrename -r -d .
./Arduboy/all-the-demos.zip: multiple pdxinfo files found, aborting
./Arduboy/Rev B/playdate-arduboy-fw_2.0.3_recompile.zip: multiple pdxinfo files found, aborting

```

At that point, you can generate a json database of your roms, and then generate a webpage

```
$ time $(pdxtag -r . index; pdxhtml -i index)

real    0m8.675s
user    0m36.887s
sys     0m5.786s
```

### Notes

These use GNU parallel and I can't guarantee safety in any capacity- use at your own discretion, I probably won't help you use this.

Mac/UNIX: install a newer version from brew or otherwise, must support readarray. Change "grep" in the scripts to "ggrep" for GNU Grep

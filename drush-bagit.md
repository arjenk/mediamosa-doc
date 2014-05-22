# Import/export media in MediaMosa with Drush and BagIt

BagIt import and export is available since MediaMosa 3.5.1.


### BagIt

BagIt ([https://en.wikipedia.org/wiki/BagIt](https://en.wikipedia.org/wiki/BagIt)) is a hierarchical file
packaging format designed to support storage of digital content. A bag
consists of files and tags, describing the files.

BagIt is used in MediaMosa as the standard tool to import and export
assets. In the MediaMosa source tree a library phpBagit ([https://github.com/scholarslab/BagItPHP](https://github.com/scholarslab/BagItPHP)) is included, so there
is no need to install extra packages.

#### How to use

Drush needs to be told where the MediaMosa installation is, and what
uri we are talking to. For example

```
drush --uri=http://myurl --root=/srv/www/mediamosa mm-version
```
(tip: use a .drushrc)

There are two drush bagit commands: the import and the export.


#### Drush mm-export-bagit

All drush commands have inline help:

```bash
$ drush mm-export-bagit -h

Exports the content of an asset to a bagIt file.

Arguments:
 asset_id                             Asset id to be exported
 path                                    Path where the bagIt file is saved

Options:
 --quiet                                   Suppress messages.

Examples:
drush mm-export-bagit  h2LMORcSojgPhPH3ch5cVXX6 /tmp

Exports asset id h2LMORcSojgPhPH3ch5cVXX6 to /tmp/h2LMORcSojgPhPH3ch5cVXX6.zip.
```

#### Drush mm-import-bagit

```bash
$ drush --uri=http://myurl --root=/srv/www/mediamosa mm-import -h

Imports the content of a directory in a new asset. If the
directory contains a bag-info.txt, this file is used to add metadata
to the asset.

Examples:
 drush mmimp /mnt/media/item1              Import the contents of directory /mnt/media/item1 into a new asset.
 drush mmimp --symlink /mnt/media/item1    The same but now with symbolic links.


Arguments:
 path                                      Path to a directory that needs to be imported.
 app_id		id of the application this asset is imported into. Defaults to 1.
 owner		name of the owner this asset will get. Defaults to ‘N.N’.
```

The drush import can for example be used as follows;

```
drush --uri=http://myurl --root=/srv/www/mediamosa mm-import-bagit /srv/bagits/o204ureiwfjsv/ 2
```

This command will start an Bagit import in MediaMosa with the contents
of the directory /srv/bagits/o204ureiwfjsv/ into application with
id 2.

### Structure of a Bag-info.txt

The bag-info.txt is a file in the root of the bagit that describes the metadata for the bag, using colon-separated key/value pairs (similar to HTTP headers).

Multiline is allowed, if indented with 2 spaces. The order of the fields is not relevant.

The syntax of the Dublin Core fields is:  DC-<Dublin core field>, with the field being camelcase. for example:  DC-Title. Each asset has one bag-info.txt. So for example:
```
DC-AccessRights: open
DC-Creator: Caine, Hall,
DC-Creator: Teding van Berkhout, Frans,
DC-DateAccepted: 2012-09-14
DC-Description: Het werk der vrouwen in Groot Brittannië / door Hall
  Caine ; vertaling van Frans Teding van Berkhout.
DC-Identifier: rug01:001647140
DC-Identifier: BIB.217P022/9
DC-Identifier: BHSL.HS.III.0024.000069
DC-Identifier: BHSL.HS.III.0024.000067
DC-Identifier: BHSL.HS.III.0024.000068
DC-Title: RUG01-001647140
DC-Type: Text
```

### Known issues
newlines in bag-info.txt


### Extra’s
extra options in bag-info.txt

### Examples

export example of an existing asset : vXgbQdVFmEFAirJoq7WrTdNv

```
drush --uri=http://myurl --root=/var/www/mediamosa mm-export-bagit vXgbQdVFmEFAirJoq7WrTdNv /tmp
```

This creates a directory in /tmp:

```bash
# ls -sal /tmp/vXgbQdVFmEFAirJoq7WrTdNv/
totalt 28
4 drwxr-xr-x  3 root root 4096 maj 20 16:09 .
4 drwxrwxrwt 14 root root 4096 maj 20 16:11 ..
4 -rw-r--r--  1 root root  309 maj 20 16:09 bag-info.txt
4 -rw-r--r--  1 root root   55 maj 20 16:09 bagit.txt
4 drwxr-xr-x  2 root root 4096 maj 20 16:09 data
0 -rw-r--r--  1 root root    0 maj 20 16:09 fetch.txt
4 -rw-r--r--  1 root root  276 maj 20 16:09 manifest-sha1.txt
4 -rw-r--r--  1 root root  215 maj 20 16:09 tagmanifest-sha1.txt
```

This BagIt can be imported again:

```
drush mm-import-bagit /tmp/vXgbQdVFmEFAirJoq7WrTdNv/ 1 
Analyse job for mf: p1ckcUkaqedSIDWKT3Wc5ufs requested
Analyse job for mf: jUbhVDXCafNLZMgJJLEyCVdt requested
Analyse job for mf: C2Yv3VTaQWPFKKb6dfNJzYli requested
Bagit file imported; asset id : XZKRXjWQtH6KPotjBjuubPbj
```
Note that a new asset is created.



# comicbookinfo
Mirrored from [code.google.com/p/comicbookinfo](https://code.google.com/archive/p/comicbookinfo/) since Google Code appears to be shutting down.
The documentation of this article will be properly transferred to GitHub over time.

# Overview
ComicBookInfo is a metadata container format to be used with the CBZ digital comic file format. It allows information such as the title, series, genre, publisher, author and other information to be stored in the file itself.

The combination of ComicBookInfo and CBZ provides a cross-platform solution for including metadata with digital comics, and thus allowing the tagging of digital comics.

# Metadata for Digital Comics
## How can we make comic book metadata available on a cross-platform basis, for existing and new digital comic files?
For the popular MP3 format, a chunk of data is added to the end (ID3v1) or inserted at the start (ID3v2) of an MP3 file. Adding data to the start or end of a CBZ or CBR digital comic would result in standard unzip and unrar tools no longer recognising the file as a compressed archive, and all existing digital comic readers would no longer be able to open the files.

Adding metadata to the CBZ or CBR digital comic, by inserting a file into the compressed ZIP / RAR archive, is suitable for new digital comic files. The EPUB format (based on ZIP) for digital books is proposing to have a rights.xml file stored in the root of the ZIP container. Doing something similar such as inserting a metadata file in the root of the comic archive would be costly for existing comics - they would need to be decompressed and recompressed in order to insert the metadata file, and upon any changes to the metadata.

The proposed solution is to add metadata to the ZIP comment of a CBZ digital comic. Updates and changes to the ZIP comment are computationally cheap O(1). Decompression and recompression of the CBZ archive is not required as the ZIP specification stores the UTF8 file comment at the end of the ZIP file. The result is that metadata can be read and updated on any computer platform which has ZIP support. The ZIP comment is currently unused for CBZ digital comics (nobody has declared an official use for it, until now).

## ComicBookInfo Metadata Format

ComicBookInfo metadata format:
* JSON (JavaScript Object Notation)
* UTF-8 text encoding

Metadata storage method:
* Stored inside the zip comment of a CBZ file

Maximum size of metadata:
* 65535 bytes
* unzip.h declares: `uLong size_file_comment; /* file comment length 2 bytes */`

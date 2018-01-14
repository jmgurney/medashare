# medashare (Meta Data Sharing)

The idea for medashare is both a standard, but also an implementation of defining and sharing metadata about files.  Some media contains the ability to embed metadata, e.g. mp3, some documents, video files, but not all files are able to convey the complete and rich information that may be desired.  This will allow you to identify files, and have external assosicated metadata with various files.

The idea is also to be able to classify parts of the metadata as private (aka TLP:Red), such that the information will not be shared, so that you can mark files w/ your own tags and/or ratings, which will not be automatically shared.

There will also be able to define derivitive works by the standard.  For example, an album may have multiple tracks, so you can note that an mp3 file is a segment of the album, or that the mp3 file obtained from a music service is equivalent to the track.  This will allow sharing metadata between mediums.

This derivation is also useful for when files are programaticly transformed.  Say an image is resized, adding a note that the smaller file is a derivative work can allow others to reproduce the file, but also allow you to not have to reenter all the metadata associated with the new version of the file.

This can be useful for things like raw files on a camera, where you associate general picture information w/ the raw image data (but none of the associated processing data that files like CR2 contains) so that the meta data is not lost.

This work is inspired by my work on STIX, a Cyber Threat Inteligence standard, that has many similar requirements as meta data sharing.

## MetaData Object

The base object will contain all the data associated w/ the file.  The base set of data is based upon the [Dublin Core] specification, as it provides a nice starting point, and will provide a good mapping to other systems out there.

## Link Object

A link object references a MetaData Object, and contains information about the file that the metadata object is associated with.

[Dublin Core]: http://dublincore.org/documents/dces/

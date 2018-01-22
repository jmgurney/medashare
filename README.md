# medashare (Meta Data Sharing)

The idea for medashare is both a standard, but also an implementation of defining and sharing metadata about files.  Some media contains the ability to embed metadata, e.g. mp3, some documents, video files, but not all files are able to convey the complete and rich information that may be desired.  This will allow you to identify files, and have external assosicated metadata with various files.

The idea is also to be able to classify parts of the metadata as private (aka TLP:Red), such that the information will not be shared, so that you can mark files w/ your own tags and/or ratings, which will not be automatically shared.

There will also be able to define derivitive works by the standard.  For example, an album may have multiple tracks, so you can note that an mp3 file is a segment of the album, or that the mp3 file obtained from a music service is equivalent to the track.  This will allow sharing metadata between mediums.

This derivation is also useful for when files are programaticly transformed.  Say an image is resized, adding a note that the smaller file is a derivative work can allow others to reproduce the file, but also allow you to not have to reenter all the metadata associated with the new version of the file.

This can be useful for things like raw files on a camera, where you associate general picture information w/ the raw image data (but none of the associated processing data that files like CR2 contains) so that the meta data is not lost.

This work is inspired by my work on STIX, a Cyber Threat Inteligence standard, that has many similar requirements as meta data sharing.

## Goals

1. Provide meta data, such as title, actors, copyright holder, for files, such as movies, photos, documents.
2. Allow look up of meta data by title, actors, etc.
3. Look up meta data belonging to a file, via file hash.
4. Support embedded files, such as within a zip file, or bittorrent, so the querier can get all the meta data for a container file, or that the file can be located for download.
5. Identify transformations of files, such as a reencoding of a movie, or a resizing of a photo.
6. Possily use of fingerprint technology, so that the database can be to query metadata based upon parts of the audio/video/image.

## MetaData Object

Properties:
uuid		UUIDv4
modified	date of last modification
dc:<prop>	A [Dublin Core] property
object_marking_refs	Imported from [STIX v2.0 Part 1]: Section 3.1
granular_markings	Imported from [STIX v2.0 Part 1]: Section 3.1

Opinion Properties:
qualityrating	On a scale from 1 (poor/terrible) to 5 (great/pristine), the subjective quality of the content

The base object will contain all the data associated w/ the file.  The base set of data is based upon the [Dublin Core] specification, as it provides a nice starting point, and will provide a good mapping to other systems out there.

There may be a link to another MetaData object from which this one is derived.  If there is, all the meta data from the derived object (and the ones it derives from) must be included, except for the ones that have been marked deleted, or were overridden.  When a property is marked as opinion, it should not be inherited.  If the new author agrees with the opinion, then they have to restate the opinion in their object.

Custom properties must be preceeded w/ a namespace.  The name space is name followed by colon, as is demonstracted above w/ dc for [Dublin Core].

The link to the metadata object must include the version referenced, as the referenced object may change.  A three way merge may be needed when updating an object where the derived object has also been updated if the new information is wished to be used.

Open Questions:  When metadata is "declassified", how do you maintain a link to the classified version?

## File Object

A link object references a MetaData Object, and contains information about the file that the metadata object is associated with.

[Dublin Core]: http://dublincore.org/documents/dces/
[STIX v2.0 Part 1]: http://docs.oasis-open.org/cti/stix/v2.0/cs01/part1-stix-core/stix-v2.0-cs01-part1-stix-core.html

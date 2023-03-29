## Initial scripts
For the specific use case, 3 Python scripts have been made to:
- extract the song download links from a plain HTML page saved from a song listing site (e.g. https://freemusicarchive.org/genre/Ambient_Electronic/)
- follow all download links to fetch all the songs into a dir
- extract the title and author name of all downloaded song files, and print them into a separate txt (to be used for attribution if the songs were used in publically consumed content)

## Plan for extension
- bootstrap these scripts into one Python program that accepts a Free Music Archive url of the correct format, and which points to a song listing page, and produces a file for each song on said listing, in a dir specified by the user
- port this Python script to something better, like Rust

## Fetching the listing pages ([[Pagefetch]])
The most prominent bottleneck for the previous workflow (if it can even be considered that) is that the song listing pages had to be downloaded by hand, and only then could they be handed to the scripts. We shall now implement a script to accomplish that task as well.

## Bootstrapping
With the missing core part established, we can start exporting the functions from their separate files into a full-blown CLI:
- extract url validation from `get_pages.py`
- extract validation errors
- move argparsing to `main.py`
- rework `extract_urls.py` to work with strings instead of files
	- at this point, the resulting url-s have some unexpected junk at the end `"}\'>`, but removing this is trivial
	- some of the download links are also junk through and through (e.g. leading to .bin files), but these are rare enough to be fine to ignore for now
- extract `download_songs.py`
- add output directory arg to CLI
- add silent mode to make it less loud during download
- extract metadata extraction, add arg to make it optional
	- add another arg to delete songs with no metadata
# Modifying sc2 Icons
In-game icons and textures are stored in DDS (direct-draw surface) format. This is a lossy compression format that optimizes the performance of loading it into a game.

You can open and save .dds files with gimp, and viewing icons in Windows explorer will often preview the images correctly. To export from gimp, make sure you compress with DXT5 format. Windows Explorer feedback seems to depend on the compression method and on the size metadata being reported correctly.

*Unconfirmed*: I think BC3/DXT5 compression is the way to go in gimp?

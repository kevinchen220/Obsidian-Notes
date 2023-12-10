# Files

> [!tldr] Named bytes on disk

## Abstraction
User’s view
![[Pasted image 20231209194721.png]]
* a file is a named sequence of bytes
FS’s view
* File is a collection of data blocks
FS’s job
![[Pasted image 20231209194737.png]]
* Translate name and offset to data blocks

## File operations
* Create a file
* Delete a file
* Read from a file
* Write to a file
* 
KuboFS
======

Kubo (Cube) partitions large files into small blocks and attempts to distribute them to a central repository.

Should be used for backups or with GFS2.

Writes are not complete until they have been uploaded to a central repository via SFTP and processed.

Processing involves the central repository moving the block out of the way on all other clients via SFTP (blocking as this happens).

Binary deltas are used to transfer the blocks.  These deltas are created on demand using a simple offset parameter.

Future Plans
============

I'd like to make a Python NBD server to handle this with individual config files rather than use Fuse.

Requirements
============

  - Python
  - Python-Fuse
  - PyZMQ
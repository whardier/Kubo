KuboFS
======

Star based block distribution system with a single point of failure.  Fun for some, not for all.

KuboFS partitions large files into small blocks and attempts to distribute them to a central repository.

Should be used for backups or with GFS2.

Writes are not complete until they have been uploaded to a central repository via a ZMQ Dealer socket and processed.

Processing means a ZMQ Router socket is used to inform all clients to delete a specific block from their disk and
optionally download it.  By default KuboFS will not download blocks and will download them on demand.  Once each KuboFS
peer replies nominally control is returned to the KuboFS peer that initiated the write and subsequently the filesystem
driver using the block device.

Future Plans
============

I'd like to make a Python NBD server to handle this with individual config files rather than use Fuse and get rid of
that requirement entirely.

Requirements
============

  - [Python](http://www.python.org/)
  - [FusePy](http://code.google.com/p/fusepy/)
  - [PyZMQ](http://zeromq.github.com/pyzmq/)
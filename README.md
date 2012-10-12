KuboFS
======

Star based block distribution system with a single point of failure (soon no point of failure).
Fun for some, not for all.

KuboFS partitions large files into small blocks and attempts to distribute them to a central repository.

Should be used for backups or with GFS2/OCFS2 and a DLM.

Writes are not complete until they have been uploaded to a central repository via a ZMQ Dealer socket and processed.

Processing means a ZMQ Router socket is used to inform all clients to delete a specific block from their disk and
optionally download it.  By default KuboFS will not download blocks and will download them on demand.  Once each KuboFS
peer replies nominally control is returned to the KuboFS peer that initiated the write and subsequently the filesystem
driver using the block device.

Requirements
============

  - [Python](http://www.python.org/)
  - [PyZMQ](http://zeromq.github.com/pyzmq/)
Kubo
====

Star based block distribution system with a single point of failure (soon no point of failure).
Fun for some, not for all.

KuboFS is an emulated NBD that maps blocks to a bunch of smaller files.  It can be run standalone or as a client where
it attempts to distribute the current block state to a central repository atomically, slowly, but atomically.

Standalone Mode
===============

Do whatever you want with the files.  A log file will be written to the base of the storage directory that includes a
list of all blocks that have changed.  This log file can be rotated as well as disabled.

Network Mode
============

Should be used for backups or with GFS2/OCFS2 and a DLM.

Writes are not complete until they have been uploaded to a central repository via a ZMQ Pair (over SSH if you want)
socket and processed.

Processing means a ZMQ Publish socket is used to inform all clients to delete a specific block from their disk and
optionally download it.  By default KuboFS will not download blocks and will download them on demand.  Once each KuboFS
peer replies control is returned to the KuboFS peer that initiated the write and subsequently the filesystem
driver using the block device.

Blocks are stored full and compressed initially.  Deltas are stored during writes.  Deltas are stored as deltas of
flattened blocks using the previous deltas.  This allows for much more optimized transactions.

Once a block has changed a certain amount of times previous deltas are applied and the block is flattened and the delta
log is reset.

Requirements
============

  - [Python](http://www.python.org/)
  - [PyZMQ](http://zeromq.github.com/pyzmq/)
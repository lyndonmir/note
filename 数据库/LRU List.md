#### Organization of the Database Buffer Cache

- The buffers in the cache are organized in two lists: the write list and the least recently used (LRU) list. The _write list_ holds _dirty buffers,_ which contain data that has been modified but has not yet been written to disk. The _least recently used (LRU) list_ holds free buffers, pinned buffers, and dirty buffers that have not yet been moved to the write list. _Free buffers_ do not contain any useful data and are available for use. _Pinned buffers_ are currently being accessed.

- When an Oracle process accesses a buffer, the process moves the buffer to the most recently used (MRU) end of the LRU list. As more buffers are continually moved to the MRU end of the LRU list, dirty buffers age towards the LRU end of the LRU list.

- The first time an Oracle user process requires a particular piece of data, it searches for the data in the database buffer cache. If the process finds the data already in the cache (a _cache hit_), it can read the data directly from memory. If the process cannot find the data in the cache (a _cache miss_), it must copy the data block from a datafile on disk into a buffer in the cache before accessing the data. Accessing data through a cache hit is faster than data access through a cache miss.

- Before reading a data block into the cache, the process must first find a free buffer. The process searches the LRU list, starting at the least recently used end of the list. The process searches either until it finds a free buffer or until it has searched the threshold limit of buffers.

- If the user process finds a dirty buffer as it searches the LRU list, it moves that buffer to the write list and continues to search. When the process finds a free buffer, it reads the data block from disk into the buffer and moves the buffer to the MRU end of the LRU list.

- If an Oracle user process searches the threshold limit of buffers without finding a free buffer, the process stops searching the LRU list and signals the DBW0 background process to write some of the dirty buffers to disk.
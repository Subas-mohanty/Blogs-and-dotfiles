## Disk Structure
1. Disk is divided into tracks and sectors which are logical circles.
2. The intersection of tracks and sectors is known as blocks.
															 ![[Screenshot from 2025-02-02 01-40-02.png]]
3. Block size is taken as 512 bytes but it depends on manufacturer.
4. Each block can be addressed using the track and sector number like a 2-D array.
5. Data is read from the disk as blocks, even if we want to read a single bit we have to get the full block to the main memory and then we will read the required data and send it to further use.
6. Each byte or the space till the data in the block is known as offset.
7. While performing any task, data is brought to the main memory from the disk because the data can't be processed on the disk.
8. Now when we brought the data to the main memory for any process we have to first store the data there. And there we use data structures. Ex: Array, Queue, Heap, Tree etc.
9. Organizing the data on the disk efficiently so that it can easily utilized is called DBMS(Database Management System).
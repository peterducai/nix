
# Features


## ???

* paxos vs raft

# JFS

Journal
JFS is a journaling file system. Rather than adding journaling as an add-on feature like in the ext3 file system, it was implemented from the start. The journal can be up to 128 MB. JFS journals metadata only, which means that metadata will remain consistent but user files may be corrupted after a crash or power loss. JFS's journaling is similar to XFS in that it only journals parts of the inode.[10]

B+ Tree
JFS uses a B+ tree to accelerate lookups in directories. JFS can store 8 entries of a directory in the directory's inode before moving the entries to a B+ tree. JFS also indexes extents in a B+ tree.

Dynamic Inode Allocation
JFS dynamically allocates space for disk inodes as necessary. Each inode is 512 bytes. 32 inodes are allocated on a 16 kB Extent.

Extents
JFS allocates files as an extent. An extent is a variable-length sequence of Aggregate blocks. An extent may be located in several allocation groups. To solve this the extents are indexed in a B+ tree for better performance when locating the extent locations.

Compression
Compression is supported only in JFS1 on AIX and uses a variation of the LZ algorithm. Because of high CPU usage and increased free space fragmentation, compression is not recommended for use other than on a single user workstation or off-line backup areas.[2][11]

Concurrent Input / Output (CIO)
JFS normally applies read-shared, write-exclusive locking to files, which avoids data inconsistencies but imposes write serialization at the file level. The CIO option disables this locking. Applications such as relational databases which maintain data consistency themselves can use this option to largely eliminate filesystem overheads.[12]

Allocation Groups
JFS uses Allocation groups. Allocation groups divide the aggregate space into chunks. This allows JFS to use resource allocation policies to achieve great I/O performance. The first policy is to try to cluster disk blocks and disk inodes for related data in the same AG in order to achieve good locality for the disk. The second policy is to distribute unrelated data throughout the file system in an attempt to minimize free-space fragmentation. When there is an open file JFS will lock the AG the file resides in and only allow the open file to grow. This reduces fragmentation as only the open file can write to the AG.

JFS Superblocks
The superblock maintains information about the entire file system and includes the following fields:

Size of the file system
Number of data blocks in the file system
A flag indicating the state of the file system
Allocation group sizes
File system block size


# Hadoop

The Hadoop distributed file system (HDFS) is a distributed, scalable, and portable file system written in Java for the Hadoop framework. Some consider it to instead be a data store due to its lack of POSIX compliance,[28] but it does provide shell commands and Java application programming interface (API) methods that are similar to other file systems.[29] A Hadoop is divided into HDFS and MapReduce. HDFS is used for storing the data and MapReduce is used for the Processing the Data. HDFS has five services as follows:

1. Name Node

2. Secondary Name Node

3. Job tracker

4. Data Node

5. Task Tracker

Top three are Master Services/Daemons/Nodes and bottom two are Slave Services. Master Services can communicate with each other and in the same way Slave services can communicate with each other. Name Node is a master node and Data node is its corresponding Slave node and can talk with each other.

Name Node: HDFS consists of only one Name Node we call it as Master Node which can track the files, manage the file system and has the meta data and the whole data in it. To be particular Name node contains the details of the No. of blocks, Locations at what data node the data is stored and where the replications are stored and other details. As we have only one Name Node we call it as Single Point Failure. It has Direct connect with the client.

Data Node: A Data Node stores data in it as the blocks. This is also known as the slave node and it stores the actual data into HDFS which is responsible for the client to read and write. These are slave daemons. Every Data node sends a Heartbeat message to the Name node every 3 seconds and conveys that it is alive. In this way when Name Node does not receive a heartbeat from a data node for 2 minutes, it will take that data node as dead and starts the process of block replications on some other Data node.

Secondary Name Node: This is only to take care of the checkpoints of the file system metadata which is in the Name Node. This is also known as the checkpoint Node. It is helper Node for the Name Node.

Job Tracker: Basically Job Tracker will be useful in the Processing the data. Job Tracker receives the requests for Map Reduce execution from the client. Job tracker talks to the Name node to know about the location of the data like Job Tracker will request the Name Node for the processing the data. Name node in response gives the Meta data to job tracker.

Task Tracker: It is the Slave Node for the Job Tracker and it will take the task from the Job Tracker. And also it receives code from the Job Tracker. Task Tracker will take the code and apply on the file. The process of applying that code on the file is known as Mapper.[30]

Hadoop cluster has nominally a single namenode plus a cluster of datanodes, although redundancy options are available for the namenode due to its criticality. Each datanode serves up blocks of data over the network using a block protocol specific to HDFS. The file system uses TCP/IP sockets for communication. Clients use remote procedure calls (RPC) to communicate with each other.

HDFS stores large files (typically in the range of gigabytes to terabytes[31]) across multiple machines. It achieves reliability by replicating the data across multiple hosts, and hence theoretically does not require redundant array of independent disks (RAID) storage on hosts (but to increase input-output (I/O) performance some RAID configurations are still useful). With the default replication value, 3, data is stored on three nodes: two on the same rack, and one on a different rack. Data nodes can talk to each other to rebalance data, to move copies around, and to keep the replication of data high. HDFS is not fully POSIX-compliant, because the requirements for a POSIX file-system differ from the target goals of a Hadoop application. The trade-off of not having a fully POSIX-compliant file-system is increased performance for data throughput and support for non-POSIX operations such as Append.[32]

In May 2012, high-availability capabilities were added to HDFS,[33] letting the main metadata server called the NameNode manually fail-over onto a backup. The project has also started developing automatic fail-overs.

The HDFS file system includes a so-called secondary namenode, a misleading term that some might incorrectly interpret as a backup namenode when the primary namenode goes offline. In fact, the secondary namenode regularly connects with the primary namenode and builds snapshots of the primary namenode's directory information, which the system then saves to local or remote directories. These checkpointed images can be used to restart a failed primary namenode without having to replay the entire journal of file-system actions, then to edit the log to create an up-to-date directory structure. Because the namenode is the single point for storage and management of metadata, it can become a bottleneck for supporting a huge number of files, especially a large number of small files. HDFS Federation, a new addition, aims to tackle this problem to a certain extent by allowing multiple namespaces served by separate namenodes. Moreover, there are some issues in HDFS such as small file issues, scalability problems, Single Point of Failure (SPoF), and bottlenecks in huge metadata requests. One advantage of using HDFS is data awareness between the job tracker and task tracker. The job tracker schedules map or reduce jobs to task trackers with an awareness of the data location. For example: if node A contains data (a, b, c) and node X contains data (x, y, z), the job tracker schedules node A to perform map or reduce tasks on (a, b, c) and node X would be scheduled to perform map or reduce tasks on (x, y, z). This reduces the amount of traffic that goes over the network and prevents unnecessary data transfer. When Hadoop is used with other file systems, this advantage is not always available. This can have a significant impact on job-completion times as demonstrated with data-intensive jobs.[34]

HDFS was designed for mostly immutable files and may not be suitable for systems requiring concurrent write operations.[32]


# Other

* read only clones (anti-malware)
---
tags:
  - os
---
# Files and File Management
- **Files** are the central element to most applications.
- **Desirable properties of files**: Long-term existence, Shareable between processes, and Structure.
- The **File Management System** consists of system utility programs that run as privileged applications.
- It is concerned with **secondary storage**.
## Typical Operations
File systems provide functions which can be performed on files, typically:
- Create, Delete, Open, Close, Read, Write.
## Terms
Common terms when discussing files:
- **Field**: Basic element of data, contains a single value, characterised by its length & data type.
- **Record**: Collection of related fields, treated as a unit.
- **File**: Collection of similar records, treated as a single entity, with a name and access control, may implement access control mechanisms.
- **Database**: Collection of related data, with relationships among elements, consisting of one or more files.
# Objectives for a File Management System
- Meet the data management needs of the user.
- Guarantee that the data in the file is valid.
- Optimise performance.
- Provide I/O support for a variety of storage device types.
- Minimise lost or destroyed data.
- Provide a standardised set of I/O interface routines to user processes.
- Provide I/O support for multiple users (if needed).
## Requirements for a General-Purpose System
1. Create, delete, read, write and modify files.
2. Controlled access to other users' files.
3. Control what type of access is allowed to users' files.
4. Restructure files in an appropriate form.
5. Move data between files.
6. Back up and recover files.
7. Access files using symbolic names (create a shortcut).
## Typical Software Organisation (Figure 12.1+2)
- **Device Drivers**: Lowest-level drivers that communicate with peripheral devices.
- **Basic File System**: Physical I/O deals with exchanging blocks of data.
- **Basic I/O Supervisor**: Responsible for file I/O initiation and termination.
- **Logical I/O**: Enables users and applications to access records.
- **Access Method**: Closest to the user, provides a standard interface between applications and the file system.
---
# File Organisation and Access

## Criteria for File Organisation
- Short access time.
- Ease of update.
- Economy of storage.
- Simple maintenance.
- Reliability.
(Priorities differ depending on use case, e.g., read-only CD vs. Hard Drive).
## File Organisation Types
- **The Pile**: Data collected in the order they arrive, no structure, exhaustive search.
- **The Sequential File**: Fixed format, records of same length and fields = waste storage, stored in key sequence = search faster (same as excel file).
- **Indexed Sequential File**: Sequential file with an index for random access and an overflow file.
- **Indexed File**: Uses multiple indexes for different key fields, using the pile file.
- **Direct, or Hashed File**: Directly access a block at a known address.
---
# File Directories (Danh Bạ)
- Contains information about files (attributes, location, ownership).
- The directory itself is a file owned by the OS.
- Main Purpose: **Provides a mapping between file names and the files themselves**.
## Directory Elements
- **Basic Information**: File Name, File Type, File Organisation.
- **Address Information**: Volume, Starting Address, Size Used, Size Allocated.
- **Access Control Information**: Owner, Access Information, Permitted Actions.
- **Usage Information**: Date Created, Date Last Read, Date Last Modified, etc.
## Directory Structures (Trees)
- **Simple Structure**: A single list of entries, one for each file. No help in organising files.
- **Two-Level Scheme**: One master directory and a separate directory for each user.
- **Hierarchical, or Tree-Structured Directory**: A master directory with user directories, which may have subdirectories. Allows for unique naming within a path.
- **Working Directory**: A current directory associated with a user or process to avoid using full pathnames.
---
# File Sharing
- In multiuser systems, files can be shared among users.
- **Two issues**:
    1.  **Access Rights**: Controlling who can access the file and what they can do.
    2.  **Management of simultaneous access**.
## Access Rights
- **Hierarchy of Rights**: 
	- None: The user may not even know of the file’s existence
	- Knowledge: know existence, owner
	- Execution: execute only
	- Reading: read file
	- Appending: append data
	- Updating: modify, delete, and add to the file’s data
	- Changing protection: change access file, delete
	- Deletion: delete
- **User Classes**: 
	- Owner: full rights
	- Specific users: individual
	- User groups: a set of users
	- All (everyone).
## Simultaneous Access
- Users may lock the entire file or individual records during updates.
- **Mutual exclusion** and **deadlock** are key issues for shared access.
---
# Record Blocking
- **Records** are the logical unit of access of a structured file.
- **Blocks** are the unit for I/O with secondary storage.
- **Three approaches**:
    - **Fixed Blocking**: An integral number of fixed-length records is stored in a block. Can lead to **internal fragmentation**.
    - **Variable Length Spanned Blocking**: Variable-length records packed with no unused space; *a single record may span multiple blocks* (increasing management cost).
    - **Variable-length unspanned blocking**: Wasted space if a record doesn't fit in the remaining space of a block.
---
# Secondary Storage Management
The OS is responsible for allocating blocks to files and keeping track of available space.
## File Allocation Issues
1. Is maximum space allocated at once?
2. How are portions added to a file? (Size of portion).
3. What data structure is used to track file portions?
### Preallocation vs. Dynamic Allocation
- **Preallocation**: Need maximum file size at creation, but difficult to estimate.
- **Dynamic Allocation**: Allocate space as needed.
### Portion Size
- Trade-off between allocating the whole file at once vs. one block at a time.
## File Allocation Methods
- **Contiguous Allocation**: A single set of blocks allocated at creation. Suffers from **external fragmentation**, may require compaction.
- **Chained Allocation**: Allocation on the basis of individual blocks, each block points to the next. No external fragmentation. Best for sequential files.
- **Indexed Allocation**: A separate one-level index for each file contains pointers to all allocated blocks.
## Free Space Management
- **Bit Tables**: A vector containing one bit for each block on the disk (0=free, 1=used).
- **Chained Free Portions**: Free blocks are chained together.
- **Indexing**: Treats free space as a file and uses an index.
- **Free Block List**: A list of numbers of all free blocks is maintained.
# File System Security
- **Access Control**: Users are identified upon login, and the OS enforces rules for access (using method rules-based access control).
- **Access Matrix**: A model of access control with subjects (users), objects (files), and access rights.
- **Access Control Lists (ACL)**: Decomposed by columns (for each file, list users and their rights).
- **Capability Lists**: Decomposed by rows (for each user, list files and their rights).
---
# Unix File Management
- **File Types**: Regular, Directory, Special, Named pipes, Links, Symbolic links.
- **Inodes**: A control structure containing key information for a file. Multiple filenames can point to a single inode.
	- Index node
	- A Control Structure that contains key information for a particular file.
	- Several filenames may be associated with one inode
	- Structure: data field, ...
		- Assumption: 1 data block = 1KB. We use 32bits system = 4 bytes
		- direct pointer: points to 1 data block
			- Have 9-13 direct ⇒ 9-13KB
		- Indirect pointer:
			- Pointer block size = data block size
				- How many pointers in a block? We need to have the size of a pointer
				- 1024B / 4 B = 256 pointers
			- Single indirect: points to a pointer block (only stores pointers): 256KB
			- Double indirect: 64 MB
			- Triple indirect: 16GB
		- Maximum file size: 16GB + 64MB + 256KB + 9-13KB
		- Put data sequential: direct → single indirect  → double indirect → triple indirect
- **File Allocation**: Done on a block basis, using an index method with direct and indirect pointers stored in the inode.
---
# Linux Virtual File System (VFS)
- Uniform file-system interface for user processes.
- Represents any conceivable file system's general features and behaviour.
- Assumes files are objects with shared basic properties.
- **Primary Objects**: Superblock, Inode, Dentry, and File objects.
---
# Windows File System (NTFS)
- **Key features**: Recoverability, Security, Large disks and files, Multiple data streams, Journaling, Compression, and Encryption.
- **Structure**:
    - **Sector**: Smallest physical storage unit (usually 512 bytes).
    - **Cluster**: One or more contiguous sectors.
    - **Volume**: A logical partition on a disk.
- **NTFS Volume Layout**: Every element is a file, and every file consists of a collection of attributes.
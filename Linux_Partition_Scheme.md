## <span style="font-size: 20px;"><strong><em>Linux Partition Scheme:</em></strong></span>
A Linux partition scheme is a way of dividing a physical storage device (like a hard drive or SSD) into multiple logical sections called partitions. Each partition can then be formatted with a specific file system and used for different purposes. 

***Types of Partitions -***
  - Primary Partitions: Traditional partitioning allows for up to four primary partitions.
  - Extended Partition: An extended partition acts as a container for multiple logical partitions, overcoming the four-partition limit.
  - Logical Partitions: Subdivisions within an extended partition.

***Key Partitions in a Typical Linux Setup -***
  - / (Root): The top-level directory of the file system. Contains the operating system's core files, applications, and system configurations.
  - /home: Stores user data, including documents, pictures, and settings. Separating /home allows you to reinstall the operating system 
  - without losing user data.
  - swap: Used as virtual memory to extend the system's RAM. When physical RAM is full, the system uses swap space on the hard drive.
  - /boot: Contains the boot loader and kernel, which are necessary to start the operating system.

***Partition Tables -***
  - MBR (Master Boot Record): A legacy partitioning scheme with limitations on partition size (2TB) and the number of primary partitions (4).
  - GPT (GUID Partition Table): A modern standard that supports larger disks, more partitions, and improved data integrity.

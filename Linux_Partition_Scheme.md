## <span style="font-size: 20px;"><strong><em>Linux Partition Scheme:</em></strong></span>
A Linux partition scheme is a way of dividing a physical storage device (like a hard drive or SSD) into multiple logical sections called partitions. Each partition can then be formatted with a specific file system and used for different purposes. 

***Types of Partitions -***
There are several types of partitions that you can create to organize and manage your data. Here are the main types
  - Primary Partitions: 
    - Description: A primary partition is a type of partition that can host an operating system or other essential files.
    - Limitations: On MBR disks, you can have up to four primary partitions. On GPT disks, you can have many more.
    - Use Case: Typically used for operating system installation and bootable partitions.
  - Extended Partition:
    - Description: An extended partition is a type of partition that acts as a container for logical partitions. It's a way to bypass the limit of four primary partitions on MBR disks.
    - Limitations: Only one extended partition can exist on an MBR disk, but it can contain multiple logical partitions.
    - Use Case: Used when more than four partitions are needed on an MBR disk.
  - Logical Partitions:
    - Description: Logical partitions are created within an extended partition and can be used for various purposes such as data storage, additional operating systems, and more.
    - Limitations: Only available within an extended partition on MBR disks.
    - Use Case: Ideal for additional data storage and multi-boot setups.
  - Swap Partitions
    - Description: A swap partition is used by the operating system to provide additional virtual memory, extending the system's physical RAM.
    - Use Case: Used for virtual memory and system hibernation.
  - EFI System Partition (ESP)
    - Description: The EFI System Partition is a small partition on GPT disks used by UEFI firmware to store bootloader and related files.
    - Use Case: Required for UEFI systems to boot.

Summary of Partition Types  

| Header 1    | Header 2    | Header 3    | Header 4    |
|-------------|-------------|-------------|-------------|
| Row 1 Col 1 | Row 1 Col 2 | Row 1 Col 3 | Row 1 Col 4 |
| Row 2 Col 1 | Row 2 Col 2 | Row 2 Col 3 | Row 2 Col 4 |
| Row 3 Col 1 | Row 3 Col 2 | Row 3 Col 3 | Row 3 Col 4 |
| Row 4 Col 1 | Row 4 Col 2 | Row 4 Col 3 | Row 4 Col 4 |
| Row 5 Col 1 | Row 5 Col 2 | Row 5 Col 3 | Row 5 Col 4 |
| Row 6 Col 1 | Row 6 Col 2 | Row 6 Col 3 | Row 6 Col 4 |




***Partition Tables -***
There are two primary partitioning schemes in use today:
* MBR (Master Boot Record):
  - Legacy Standard: An older standard that has been around for a long time.
  - Location: The partition table is stored in the first sector of the drive (the MBR).
  - Limitations:
    - Maximum of four primary partitions.
    - Maximum disk size of 2 terabytes (TB).
    - Does not support UEFI booting directly (requires Compatibility Support Module - CSM).
  - Extended and Logical Partitions: To overcome the four-partition limit, MBR introduced the concept of an extended partition, which acts as a container for multiple logical partitions.
  - Boot Process: The BIOS firmware reads the MBR to find the boot loader, which then loads the operating system.

* GPT (GUID Partition Table):
  - Modern Standard: The current standard, designed to overcome the limitations of MBR.
  - Location: The partition table is stored in multiple locations on the drive for redundancy and error recovery.
  - Advantages:
    - Supports very large disks (up to 8 ZiB).
    - Supports a vast number of partitions (theoretically almost unlimited).
    - Required for UEFI booting.
    - Improved data integrity with CRC checksums.
  - Partition Types: GPT uses only primary partitions. There are no extended or logical partitions.
  - Boot Process: The UEFI firmware reads the GPT to find the EFI System Partition (ESP), which contains the boot loaders.
 
***Key Differences Summarized:***
| Feature | MBR | GPT |
|-----------------|-----------------|-----------------|
| Maximum Disk Size | 2TB | Very large (8 ZiB) |
| Maximum Partitions | 4 primary or 3 primary + 1 extended (with many logical inside)  | Vast number (practically unlimited)  |
| Boot Mode | BIOS (with CSM for UEFI sometimes) | UEFI |
| Partition Types | Primary, Extended, Logical | Primary only |
| Data Integrity | Less robust | More robust (CRC checksums) |
| Compatibility | Older systems, some embedded devices | Modern systems, servers |

***Key Partitions in a Typical Linux Setup -***
  - / (Root): The top-level directory of the file system. Contains the operating system's core files, applications, and system configurations.
  - /home: Stores user data, including documents, pictures, and settings. Separating /home allows you to reinstall the operating system 
  - without losing user data.
  - swap: Used as virtual memory to extend the system's RAM. When physical RAM is full, the system uses swap space on the hard drive.
  - /boot: Contains the boot loader and kernel, which are necessary to start the operating system.



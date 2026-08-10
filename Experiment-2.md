# Experiment 2: Recover Deleted or Damaged Files from a Storage Device Using TestDisk

**Date:**

## Aim

To recover deleted or damaged partitions and restore access to files stored on a storage device using TestDisk in Kali Linux.

## Description

TestDisk is an open-source data recovery utility available in Kali Linux. It is used to recover lost partitions, repair damaged partition tables, recover corrupted file systems, and restore access to files stored on damaged or deleted partitions.

In this experiment, TestDisk is used to analyse a storage device or disk image, search for a missing partition, verify the recovered files, restore the partition structure, and repair a damaged file system when a valid backup boot sector is available.

A forensic disk image or working copy should be used whenever possible so that the original storage device is not modified during the recovery process.

## Software and Tools Required

- Kali Linux
- TestDisk
- Linux Terminal
- `fdisk`
- `lsblk`
- `mount`
- `sha256sum`
- ext4 / NTFS file system
- Storage device or forensic disk image

## Procedure

### Step 1: Update Kali Linux

Open the Kali Linux Terminal and update the package repository:

```bash
sudo apt update
```

### Step 2: Install TestDisk

Install TestDisk using:

```bash
sudo apt install testdisk -y
```

Verify the installation:

```bash
testdisk --version
```

### Step 3: Identify the Storage Device

Before starting TestDisk, identify the storage devices connected to Kali Linux.

Run:

```bash
lsblk
```

You can also use:

```bash
sudo fdisk -l
```

Identify the storage device containing the lost or damaged partition.

Example:

```text
/dev/sda
/dev/sdb
/dev/nvme0n1
```

> **Warning:** Make sure the correct storage device is selected. Do not perform recovery operations on the wrong disk.

### Step 4: Start TestDisk

Start TestDisk from the Kali Linux Terminal:

```bash
sudo testdisk
```

TestDisk displays:

```text
[ Create ]
[ Append ]
[ No Log ]
```

Select **Create** and press **Enter**.

This creates a log file containing technical information and messages generated during the recovery process.

### Step 5: Select the Disk

TestDisk displays the available storage devices.

Use the **Up/Down arrow keys** to select the required storage device.

For example:

```text
Disk /dev/sdb - 32 GB
```

Press **Enter** to proceed.

### Step 6: Select the Partition Table Type

TestDisk displays the available partition table types.

For example:

```text
[Intel]
[EFI GPT]
[Mac]
[Sun]
[XBox]
[None]
```

TestDisk normally detects the partition table automatically.

Select the detected/default option.

For an MBR partition table:

```text
[Intel]
```

For a GPT partition table:

```text
[EFI GPT]
```

Press **Enter**.

### Step 7: Analyse the Partition Structure

TestDisk displays the main menu.

Select:

```text
[ Analyse ]
```

Press **Enter**.

TestDisk displays the current partition structure.

Examine the partition table for:

- Missing partitions
- Incorrect partition entries
- Damaged partitions
- Overlapping partitions
- Invalid partition structures
- Incorrect file-system information

### Step 8: Perform Quick Search

Select:

```text
[ Quick Search ]
```

Press **Enter**.

TestDisk searches for lost partitions.

The detected partitions are displayed as the search progresses.

Highlight a suspected partition using the arrow keys.

### Step 9: List the Files

Press:

```text
P
```

to list the files stored in the selected partition.

Check whether the expected directories and files are displayed.

For example:

```text
Evidence/
Documents/
report.txt
evidence.txt
```

Use the arrow keys to navigate through directories.

Press:

```text
Q
```

to return to the previous screen.

### Step 10: Perform Deeper Search

If the required partition is not found using Quick Search, select:

```text
[ Deeper Search ]
```

Press **Enter**.

Deeper Search performs a more comprehensive search for lost partitions.

Wait for the search to complete.

After the search, examine the detected partitions.

### Step 11: Verify the Detected Partitions

Select each suspected partition and press:

```text
P
```

to list its files.

Compare:

- Partition size
- File-system type
- Directory structure
- File names
- Stored evidence

Identify the partition containing the required data.

### Step 12: Identify the Correct Partition Status

TestDisk may display the following partition statuses:

```text
P - Primary
L - Logical
* - Bootable
D - Deleted
```

If the correct partition is marked as:

```text
D
```

use the **Left/Right arrow keys** to change it to the appropriate status.

For example:

```text
D → L
```

for a logical partition.

Or:

```text
D → P
```

for a primary partition.

Press **Enter** to proceed.

### Step 13: Write the Recovered Partition Table

After verifying that the correct partition has been identified, select:

```text
[ Write ]
```

Press **Enter**.

TestDisk asks for confirmation.

Select **Yes** or enter:

```text
Y
```

Press **Enter**.

The recovered partition structure is written to the partition table.

> **Important:** The `Write` operation modifies the partition structure. For real forensic investigations, perform this operation only on a forensic image or working copy, not the original evidence.

### Step 14: Exit TestDisk

After successfully writing the partition table, select **Quit** to exit TestDisk.

Return to the Kali Linux Terminal.

### Step 15: Verify the Recovered Partition

Run:

```bash
lsblk
```

You can also run:

```bash
sudo fdisk -l
```

The recovered partition should now be displayed.

For example:

```text
/dev/sdb
└─/dev/sdb1
```

### Step 16: Create a Mount Point

Create a directory for mounting the recovered partition:

```bash
sudo mkdir -p /mnt/recovered
```

### Step 17: Mount the Recovered Partition

Mount the recovered partition:

```bash
sudo mount /dev/sdb1 /mnt/recovered
```

Replace `/dev/sdb1` with the actual recovered partition shown by `lsblk`.

Verify the mount:

```bash
df -h /mnt/recovered
```

### Step 18: Verify the Recovered Files

List all files from the recovered partition:

```bash
sudo find /mnt/recovered -type f
```

View the directory contents:

```bash
sudo ls -lah /mnt/recovered
```

If the required files are accessible, the partition recovery was successful.

A recovered text file can be viewed using:

```bash
sudo cat /mnt/recovered/Evidence/evidence.txt
```

### Step 19: Calculate SHA-256 Hashes

For forensic verification, calculate SHA-256 hashes of the recovered files:

```bash
sudo sha256sum /mnt/recovered/Evidence/*
```

Record the generated hash values.

If hashes were calculated before the recovery process, compare the original and recovered hash values.

Matching hashes confirm that the file contents have remained unchanged.

### Step 20: NTFS Boot Sector Recovery

If the storage device contains an NTFS partition and TestDisk reports that the primary NTFS boot sector is damaged while the backup boot sector is valid, the boot sector can be repaired.

From the TestDisk main menu, select:

```text
[ Advanced ]
```

Select the affected NTFS partition.

If TestDisk displays:

```text
Boot sector
Bad

Backup boot sector
OK
```

select:

```text
[ Backup BS ]
```

Press **Enter**.

Confirm the operation by pressing:

```text
Y
```

TestDisk copies the valid backup boot sector to the damaged primary boot sector.

After successful recovery, TestDisk should indicate that the boot sector and backup boot sector are consistent.

Press **Enter** to continue.

> **Note:** This step is specifically applicable to NTFS partitions. It is not required for an ext4 partition.

### Step 21: Verify the Repaired NTFS Partition

After repairing the boot sector, exit TestDisk and check the partition:

```bash
lsblk
```

Mount the partition:

```bash
sudo mount /dev/sdb1 /mnt/recovered
```

Verify the files:

```bash
sudo find /mnt/recovered -type f
```

### Step 22: Unmount the Recovered Partition

After completing the examination, unmount the recovered partition:

```bash
sudo umount /mnt/recovered
```

Verify the device status:

```bash
lsblk
```

## Result

The deleted or lost partition was successfully identified and recovered using TestDisk in Kali Linux.

The partition was analysed using **Quick Search** and, when necessary, **Deeper Search**. The contents of the detected partitions were verified using the `P` option.

After identifying the correct partition, its status was changed from **Deleted (D)** to the appropriate partition type, and the recovered partition structure was written using the **Write** option.

The recovered partition was successfully accessed from Kali Linux, and the stored files were verified.

For NTFS partitions with a damaged primary boot sector and a valid backup boot sector, the **Backup BS** option was used to restore the damaged boot sector.

## Conclusion

TestDisk was successfully used in Kali Linux to analyse a storage device, identify a lost or deleted partition, verify its contents, recover the partition structure, and restore access to the stored data.

The experiment demonstrated the practical application of TestDisk in digital forensics for recovering lost partitions, analysing damaged file systems, and restoring access to recovered data.

The use of a forensic image or working copy is recommended when analysing real digital evidence to prevent accidental modification of the original storage device.

<img width="847" height="285" alt="Screenshot From 2026-08-10 23-12-22" src="https://github.com/user-attachments/assets/aa222391-76a4-4a19-a720-0b96ee0b638c" />
<img width="802" height="199" alt="Screenshot From 2026-08-10 23-13-01" src="https://github.com/user-attachments/assets/5a94cd3a-847f-4176-8430-57047eaa1ad5" />
<img width="766" height="964" alt="Screenshot From 2026-08-10 23-13-43" src="https://github.com/user-attachments/assets/a01e9f1d-eb39-4aba-8b3a-94d24f771bd3" />
<img width="762" height="294" alt="Screenshot From 2026-08-10 23-14-35" src="https://github.com/user-attachments/assets/8379e2b6-d14a-49eb-bf7e-18ff78b31f16" />
<img width="762" height="233" alt="Screenshot From 2026-08-10 23-15-25" src="https://github.com/user-attachments/assets/494158fc-4690-4e09-afff-28ccd131cc60" />
<img width="937" height="417" alt="Screenshot From 2026-08-10 23-16-32" src="https://github.com/user-attachments/assets/b1aff4f8-bb6a-4d96-8ea8-2643e45e18e2" />
<img width="926" height="1065" alt="Screenshot From 2026-08-10 23-16-57" src="https://github.com/user-attachments/assets/4e2ee8ea-4912-401a-85c5-6beea67bb63b" />
<img width="866" height="484" alt="Screenshot From 2026-08-10 23-17-22" src="https://github.com/user-attachments/assets/f6cff1ba-7267-4d65-acfd-cf38fe452c4c" />
<img width="925" height="370" alt="Screenshot From 2026-08-10 23-21-54" src="https://github.com/user-attachments/assets/43e1b3a1-01b1-48d5-afb3-3a80e1ccc6a1" />









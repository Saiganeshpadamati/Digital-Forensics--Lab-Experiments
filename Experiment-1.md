 # Experiment 1: Evidence Acquisition Using AccessData FTK Imager

## Aim

To acquire a forensic disk image from a physical storage device using AccessData FTK Imager and verify the integrity of the acquired image using MD5 and SHA1 hash values.

## Software Used

- AccessData FTK Imager 4.7.1.2
- Windows

## Introduction

FTK Imager is a computer forensic tool developed by AccessData. It is used for acquiring and analyzing digital forensic evidence.

FTK Imager can acquire:

- Volatile memory (RAM)
- Non-volatile memory such as hard disks and USB drives
- Physical drives
- Logical drives
- Image files
- Contents of folders
- CDs/DVDs

In this experiment, a physical USB storage device was acquired and converted into a forensic disk image.

## Procedure

### Step 1: Open FTK Imager

Open **AccessData FTK Imager 4.7.1.2**.

Navigate to the option for creating a disk image.

### Step 2: Select Evidence Source

Select **Physical Drive** and click **Next**.

### Step 3: Select Physical Drive

Select the physical drive that needs to be acquired.

The device used in this experiment was:

**SanDisk Cruzer Blade USB Device**

Click **Finish**.

### Step 4: Select Image Type

Select **Raw (dd)** and click **Next**.

### Step 5: Enter Evidence Information

The following evidence information was entered:

- Case Number: 1
- Evidence Number: 1
- Unique Description: DF
- Examiner: SAI GANESH
- Notes: EXP 1

Click **Next**.

### Step 6: Select Image Destination

The image was saved in the following destination:

`D:\3-1\Digital Forensics`

Image Filename:

`diskimage`

Image Fragment Size:

`0 MB`

### Step 7: Create Image

The source and destination information were displayed.

The option **Verify images after they are created** was selected.

Click **Start** to begin the acquisition.

### Step 8: Image Acquisition

FTK Imager started creating the forensic image from the physical drive.

### Step 9: Image Verification

After acquisition, FTK Imager verified the created forensic image.

The verification process checks the integrity of the acquired image using hash values.

### Step 10: Verification Result

The verification result showed:

- MD5 Verify Result: **Match**
- SHA1 Verify Result: **Match**
- Bad Blocks: **No bad blocks found in image**

### Step 11: Image Summary

The image summary provided details about the acquired physical drive.

Important information included:

- Source Type: Physical
- Drive Model: SanDisk Cruzer Blade USB Device
- Drive Interface Type: USB
- Source Data Size: 59112 MB
- Sector Count: 121061376
- Bytes per Sector: 512
- 
### Step 12: Hash Verification

The image summary showed that the computed and reported hash values matched.

**MD5:**

`9f1f7659712cde7bc536dd82f341b5ce`

**SHA1:**

`abaca319c85c310078f410c02f6b11951af63334`

Both verification results were **Match**.

## Result

The physical USB drive was successfully acquired using **AccessData FTK Imager 4.7.1.2** and converted into a **Raw (dd) forensic image**.

The acquired image was successfully verified using MD5 and SHA1 hash values.

## Verification Results

| Parameter | Result |
|---|---|
| Image Type | Raw (dd) |
| Source | Physical Drive |
| Device | SanDisk Cruzer Blade USB Device |
| Source Size | 59112 MB |
| MD5 Verification | Match |
| SHA1 Verification | Match |
| Bad Blocks | No bad blocks found |

**Therefore, the forensic image was successfully created and its integrity was verified using MD5 and SHA1 hash values.**

<img width="342" height="241" alt="image" src="https://github.com/user-attachments/assets/a3b867db-be1c-4663-b8b0-2213f36dd29d" />
<img width="679" height="550" alt="image" src="https://github.com/user-attachments/assets/97549e14-f644-41bd-9334-60f45ee72e09" />
<img width="679" height="543" alt="image" src="https://github.com/user-attachments/assets/0dbc1dde-5128-43a6-848c-31d17b75a783" />
<img width="1463" height="1075" alt="image" src="https://github.com/user-attachments/assets/c1fe2a1b-4f12-44a7-bba2-809d6330ef60" />
<img width="694" height="493" alt="image" src="https://github.com/user-attachments/assets/b774a3b0-df7c-473e-9b24-ae49ac76efcb" />
<img width="702" height="598" alt="image" src="https://github.com/user-attachments/assets/eb0bb54b-166b-405d-a5dd-98ed96d00211" />
<img width="702" height="598" alt="image" src="https://github.com/user-attachments/assets/107e5174-6b39-44a9-92d2-e59dfaf1ff8d" />
<img width="651" height="387" alt="image" src="https://github.com/user-attachments/assets/a10b49ec-c301-4944-b5f0-c4d246d6485f" />
<img width="618" height="442" alt="image" src="https://github.com/user-attachments/assets/e26c8d7c-9e0c-4143-a08e-73f98241ee49" />
<img width="1600" height="453" alt="image" src="https://github.com/user-attachments/assets/3993a447-7a8b-442e-9bdb-4f49c79d2604" />
<img width="619" height="643" alt="image" src="https://github.com/user-attachments/assets/6656c342-fce2-4440-8492-ac713eb4e960" />









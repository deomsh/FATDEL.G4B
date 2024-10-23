## FATDEL.G4B v0.3.1 (20241018)

<pre><code>Function: frontend for Grubutil 'FAT', function 'del'
FATDEL.G4B [--mdbase=sector] DEVICE[/PATH][/FILENAME[.EXT]] switches
FATDEL.G4B /? (this text)
--mdbase=sector => changes (md)-startsector in use (default=0x3000-0x3FFF)*
* Except: <0x3000, 0x3001-0xD460, 0x12000-0x12FFF
DEVICE = (fd#) & (hd#,#) & (0x#) & (#); FAT only!
/PATH/ = starting directory => without PATH => on ROOT
Last DIR in PATH accepts wildcard: '*' in Name and Extension both (NOT: '?' )
FILENAME[.EXT] = del specified file => on ROOT without /PATH/
FILENAME[.EXT] accepts wildcard: '*' in Name and Extension (NOT: '?' )
Without FILENAME[.EXT] full directory will be deleted (*.* is NOT needed)*

General Switches: /s /p /q /t /[-]x:~ /[-]y:~ /[-]r /z /lfn
/s = delete subdirectories (LFN as SFN) too *
/p = pause after each screen
/q = quiet del: error messages & last file-count message only **
/t = trial del, does not detect read-only files
/[-]x:~ = only SFN-file of LFN/real shortened LFN will [not] be deleted 3*
/[-]y:~ = only SFN-directory of LFN/real shortened LFN will [not] be deleted 3*
/[-]r = [not] delete read-only files without asking
/z = delete zero byte files only
/lfn = delete Long File Names or use Long File Names on command-line 4*
* Without FILENAME.EXT empty start-directory will be deleted (like DELTREE)
* With /s and *.* as FILENAME.EXT, empty start-directory will not be deleted!
**  Default verbose del: del and output messages too
3* Instead of '~' other chars: max full 8.3 filename (with /lfn max 16 chars)
    /[-]y:~ can NOT filter PATH, if wildcard(s) are in last directory of PATH
4* If spaces or '=' on command-line use double quotes or escaped '\ ' or '\='

FAT Directory Parser Switches*: /a:[-]darsh
/a:[-]d[-]a[-]r[-]s[-]h = [not] delete files/directories with attribute(s) *
*  About max 35 000 files and 3 000 subdirectories in one directory
** Attributes are not shown by FAT
** FAT cannot delete read-only files and read-only directories: dialog or if /r is set
** With /a:d only empty directories will be deleted (but all faked with /s /t)

Remarks:
Delete files on DEVICE; DEVICE is mandatory for safety reasons!
Delete on hidden partitions too!
Without /lfn: 8+3 file-names only, SFN of Long File Names deleted, LFN not!
Arguments space-separated! Switches: lower/uppercase free
FAT needed, searched: %~dp0, (bd), ROOT, or in /, /boot/grub/, /grub/, /g4dll/
File versions: Grubutil FAT >=15/02/2015, Grub4Dos 0.4.6a
 On FAT32 partition >= 4GB use Grubutil FAT from 2023, april or later
Switch /lfn: Loosely Linked Library ATTRIBFT.LLL needed, in same folder as FATDEL.G4B
Grub4dos for UEFI: compatible, but soon 'Out of malloc memory' errors
Found not compatible with Grub4Dos 0.4.5b / Grub4Dos 0.4.5c
Deleting can be stopped by pressing Escape (not on Grub4dos for UEFI)
More convenient => insmod DEVICE/PATH/FATDEL.G4B DEL (watch loading FAT!)

Example FATDEL.G4B (fd0)/SOMEDIR/
Example FATDEL.G4B (hd0,0)/SUBDIR/ /s
Example FATDEL.G4B (hd0,0)/SUBDIR/*.* /s /t
Example FATDEL.G4B (rd)/SOMEDIR/FILENAME.EXT
Example FATDEL.G4B (fd0)/SOMEDIR/FILE*.EX* /s
Example FATDEL.G4B (fd0)/IO.SYS
Example FATDEL.G4B (fd0)/IO.SYS /r
Example FATDEL.G4B (fd0)/SOMEDIR/ /a:-drsh /s
Example FATDEL.G4B "(hd0,0)/Long Directory/" /lfn
Example FATDEL.G4B (hd0,0)/Long\ Directory\ with\ \=/ /lfn /s /t</code></pre>    

#### ATTRIBFT.LLL

Concept of 'Loosely Linked Library' is courtesy of Wonko the Sane (Jaclaz)  
More information and download: https://github.com/deomsh/ATTRIBFT.LLL  

### HISTORY
Version 0.3.1  
NEW: deleting read-only files compatible with one File Allocation Table (number of FAT's = 1)  

Version 0.3  
First published version

### SCREENSHOTS

Example of trial-deleting all files in a directory with switch /t. Also use of asterisk-wildcard. And confirm-dialog if really deleting all files in a directory  

![FATDEL G4B example of trial deleting directory with switch -t AND use of asterisk-wildcard AND confirm-dialog if really deleting all files in a directory I](https://github.com/user-attachments/assets/a1bd8a7f-9619-4221-8f95-f5268482f9a1)

Example with switch /s to delete all files, in subdirectories too. Showed without and with asterisk wildcards for Name and Extension - with asterisk wildcards target directory remains (trial delete with switch /t)

![FATDEL G4B trial del with -s, without and with wildcards for name and extension - with target directory remains II](https://github.com/user-attachments/assets/1133f6c2-0352-4e58-a316-eeed692b8f86)

Example of trial del with asterisk wildcard in PATH and use of switch /y:CHARS, without and with switch /s

![FATDEL G4B trial del with asterisk wildcards in PATH and use of switch -y and without and with switch -s](https://github.com/user-attachments/assets/96714f94-107f-4822-abe4-c856d15d110b)

Examples of deleting read-only files with dialog or with switch /r. Als showed with attributes in switch /a:sh and /a:r

![FATDEL G4B examples of deleting read-only files with dialog or with switch -r AND with attributes in switch -a=sh and -a=r III](https://github.com/user-attachments/assets/9ea7c3f7-10f5-4567-aae3-b49ef1d6df83)

Example of use of switch /lfn, with trial del /s and /y:sys

![FATDEL G4B trial del with switch -lfn and -s and -y=sys](https://github.com/user-attachments/assets/fd193f3d-e4f9-4f9c-b249-89fe06da5487)

Example of use of switch /lfn with spaces or '=' on command-line (trial del). Watch case of missing extension wildcard in the middle of the print-screen (filesize 0!)

![FATDEL G4B use of switch -lfn with spaces or '=' on command-line](https://github.com/user-attachments/assets/7fea6c7c-968b-4b4c-95b4-dec9d063337e)

Speed of del: looptest of deleting 1459 files, without and with switch /lfn (in Windows 10 about 5 seconds)

![FATDEL G4B looptest of deleting 1459 files, without and with switch -lfn (in Windows 10 5 seconds)](https://github.com/user-attachments/assets/da1c00a3-bbb7-4183-a174-6ca28ef6af3d)

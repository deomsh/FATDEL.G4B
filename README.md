## FATDEL.G4B v0.3 (20241009)

<pre><code>Function: frontend for Grubutil 'FAT', function 'del'
FATDEL.G4B [--mdbase=sector] DEVICE[/PATH][/FILENAME[.EXT]] switches
FATDEL.G4B /? (this text)
--mdbase=sector => changes (md)-startsector in use (default=0x3000-0x3FFF)*
* Except: <0x3000, 0x3001-0xD460, 0x12000-0x12FFF
DEVICE = (fd#) & (hd#,#) & (0x#) & (#); FAT only!
/PATH/ = starting directory => without PATH => on ROOT
Last DIR in PATH accepts wildcard: '*' in Name and Extension (NOT: '?' )
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
3* Instead of '~' max full 8.3 filename: other chars can be used
4* If spaces or '=' on command-line use double quotes or escaped '\ ' or '\='

FAT Directory Parser Switches*: /a:[-]darsh
/a:[-]d[-]a[-]r[-]s[-]h = [not] delete files/directories with attribute(s) *
*  About max 35 000 files and 3 000 subdirectories in one directory
** Attributes are not shown by FAT
** FAT cannot delete read-only files and read-only directories: dialog or if /r is set
** With /a:d only empty directories will be deleted (fake all with /s /t)

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
More convenient => insmod DEVICE/PATH/FATDEL.G4B DEL (watch laoding FAT!)

Example FATDEL.G4B (fd0)/SOMEDIR/
Example FATDEL.G4B (hd0,0)/SUBDIR/ /s
Example FATDEL.G4B (hd0,0)/SUBDIR/*.* /s /t
Example FATDEL.G4B (rd)/SOMEDIR/FILENAME.EXT
Example FATDEL.G4B (fd0)/SOMEDIR/FILE*.EX* /s
Example FATDEL.G4B (fd0)/SOMEDIR/ /a:-drsh /s /r
Example FATDEL.G4B "(hd0,0)/Long Directory/" /lfn
Example FATDEL.G4B (hd0,0)/Long\ Directory\ with\ \=/ /lfn /s /t</code></pre>    

#### ATTRIBFT.LLL

Concept of 'Loosely Linked Library' is courtesy of Wonko the Sane (Jaclaz)  
More information and download: https://github.com/deomsh/ATTRIBFT.LLL  

### HISTORY
Version 0.3  
First published version

### SCREENSHOTS

Example of trial-deleting all files in a directory with switch /t. Also use of asterisk-wildcard. And confirm-dialog if really deleting all files in a directory

![FATDEL G4B example of trial deleting directory with switch -t AND use of asterisk-wildcard AND confirm-dialog if really deleting all files in a directory I](https://github.com/user-attachments/assets/a1bd8a7f-9619-4221-8f95-f5268482f9a1)




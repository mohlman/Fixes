The majority of this document is knowledge from my head. Any corrections or attributions are welcome. 



# Fixes

## Computer not booting:

EUFI System:

    bcdboot c:\windows
    
BIOS System:

    bootrec /fixmbr
    bootrec /fixboot
    bootrec /rebuildbcd

Note: If `bootrec /rebuildbcd` says that no operating systems are found, it means no new, unlisted OS is present, i.e. Windows is already in the BCD, and the command was successful.

## User Account is Corrupt

This can manifest as issues with Microsoft Store Apps, Edge, the Start Menu or Taskbar, etc.

The following example CMD code will create a new administrative user.
    
    net user /add admin
    net localgroup Administrators /add admin
    
You may then use explorer or the file manager of your choice to copy the original user accounts Documents, Desktop, etc. folders to the new account.

**Do not merge the entire AppData folder to the new user:** AppData is not designed to be moved between computers or accounts whole hog, but there may be something valuable in AppData all the same. For example:

* Google Chrome, Mozilla Firefox, and Microsoft Edge all store favorites and preferences in `AppData\Local`
* Certain Microsoft mail applications store email in `AppData\Local`
* iTunes stores iPhone/iPad backups in `AppData\Roaming`

Instead of merging EVERYTHING, a better approach would be to copy the previous account AppData folder to `C:\` or `C:\Users\admin\` as `AppData.old` before erasing the old account.
* This led to disappointment on May 20, 2018, when we were not able to retrieve the customer's Edge favorites because another technician did not make a copy of the original AppData folder.

# Examples
BCDEDIT Examples:


    bcdedit /set {default} safeboot minimal
    bcdedit /set {default} safebootalternateshell yes

The following disables automatic repair, which can be helpful. On more than one occasion a syskey password has reinstalled itself due to the repair operations performed by automatic repair. There are also situations where PC will BSOD and describe the driver/AV file that is at fault, **instead of** the unhelpful "PC Did Not Start Correctly" message following a failed Automatic Repair

    bcdedit /set {default} recoveryenabled no


Enable the handy "F8 for boot options" mode
    
    bcdedit /set {default} bootmenupolicy legacy

Get back to normal mode (from safe mode):

    bcdedit /deletevalue {default} safeboot

DISM Examples:

`dism /image:C:\ /get-packages`

`dism /online /cleanup-image /scanhealth`

SFC Examples:

`sfc /verifyonly`

`sfc /scanhealth /offbootdir=c: /offwindir=c:\windows`

Read SFC Results:

`findstr /c:"[SR] Ca" %windir%\logs\cbs\cbs.log > c:\sfc.txt`

The Run box is your friend:
    
    inetcpl.cpl

Help! The Recovery partition is visible!

    diskpart
    list vol
    select volume <number>
    remove letter=<letter>
    exit
    
The recovery partition seems to pretty regularly be volume 2 and assigned letter D. So the following often works:

    diskpart
    list vol
    sel vol 2
    remove letter=d
    exit


Windows Network Troubleshooting:

Google DNS:

    8.8.8.8
    8.8.4.4

Alternative DNS Providers:

https://www.lifewire.com/free-and-public-dns-servers-2626062


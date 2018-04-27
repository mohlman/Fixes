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


# Examples
BCDEDIT Examples:

    bcdedit /set {default} safeboot minimal
    bcdedit /set {default} safebootalternateshell yes


`bcdedit /set {default} recoveryenabled no`


Enable the handy "F8 for boot options" mode
`bcdedit /set {default} bootmenupolicy legacy`

Get back to normal mode (from safe mode):
`bcdedit /deletevalue {default} safeboot`

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


The majority of this document is knowledge from my head. Any corrections or attributions are welcome. 



# Fixes


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

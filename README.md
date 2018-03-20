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


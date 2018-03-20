# Fixes


BCDEDIT Examples:

    bcdedit /set {default} safeboot minimal
    bcdedit /set {default} safebootalternateshell yes


`bcdedit /set {default} recoveryenabled no`

`bcdedit /set {default} bootmenupolicy legacy`

`bcdedit /deletevalue {default} safeboot`

DISM Examples:

`dism /image:C:\ /get-packages`

`dism /online /cleanup-image /scanhealth`

SFC Examples:

`sfc /verifyonly`


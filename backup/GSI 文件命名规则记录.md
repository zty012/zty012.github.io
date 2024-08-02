```
{arm|a64|arm64}_{a|b}{v|g}{N|S}-{signed|vndklite|secure|personal}
|               |    |    |     |
|               |    |    |     signed: Signed with maintainer's keys
|               |    |    |     vndklite: For VNDKLite devices,
|               |    |    |               or for read-writeable /system on regular devices
|               |    |    |     personal: With personal mods, for reference
|               |    |    |     secure: Superuser removed and system props spoofed
|               |    |    |
|               |    |    N: No Superuser
|               |    |    S: *Built* with PHH Superuser (app needed)
|               |    |    (Z): *Built* with eremitein's Dynamic Superuser (not offered here)
|               |    |
|               |    v: Vanilla, i.e. no GAPPS
|               |    g: With regular GAPPS
|               |    o: With Android Go GAPPS
|               |    (f): With built-in MicroG and FLOSS replacements of GAPPS (not offered here)
|               |
|               a: "A-only", i.e. system-as-system (deprecated since Android 12)
|               b: "AB", i.e. system-as-root
|
arm: ARM 32-bit (deprecated since Android 12)
a64: ARM 32-bit with 64-bit binder
arm64: ARM 64-bit
```
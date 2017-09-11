This is a fork of zenden2k's [context-menu-launcher](https://github.com/zenden2k/context-menu-launcher) that adds support for minimum and maximum file counts.
   A minimum file count can be used to prevent the launcher from executing the command if a minimal number of files have not been selected.
   A maximum file count can be used to execute the command as soon as the maximum number of files have been selected. This is particularly helpful when selecting files individually (e.g. selecting files from separate Windows Explorer instances).

[Download executable](https://github.com/TrevorKarjanis/context-menu-launcher/releases/tag/2.0)

The original context-menu-launcher defines an executable that can be used in the Windows Explorer context menu to execute a single arbitrary command on multiple files. It does not require shell extensions and, unlike diff-ext, it works with mapped network paths.

```
Usage: singleinstance.exe "%1" {command} $files [arguments]

Optional arguments for singleinstance (not passed to command):

--si-timeout {time to wait in msecs}
--si-maxfilecount {maximum file count}
--si-minfilecount {minimum file count}
```

Sample registry file for Perforce:
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\SystemFileAssociations\.txt\Shell\p4merge]
"MultiSelectModel"="Player"

[HKEY_CLASSES_ROOT\SystemFileAssociations\.txt\Shell\p4merge\Command]
@="\"C:\\singleinstance.exe\" \"%1\" \"C:\\Program Files\\Perforce\\p4merge.exe\" $files --si-timeout 400"
```

Sample registry file for Compare It!:
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\CompareItFiles]
@="Compare it!"

[HKEY_CLASSES_ROOT\*\shell\CompareItFiles\command]
@="\"C:\\singleinstance.exe\" \"%1\" \"C:\\Program Files (x86)\\Compare It!\\wincmp3.exe\" $files --si-timeout 5000 --si-maxfilecount 2 --si-minfilecount 2"

[HKEY_CLASSES_ROOT\Folder\shell\CompareItFolders]
@="Compare It!"

[HKEY_CLASSES_ROOT\Folder\shell\CompareItFolders\command]
@="\"C:\\singleinstance.exe\" \"%1\" \"C:\\Program Files (x86)\\Compare It!\\wincmp3.exe\" $files --si-timeout 5000 --si-maxfilecount 2 --si-minfilecount 2"
```
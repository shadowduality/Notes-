Create New Virtual Environment
```
python -m venv /path/to/new/virtual/environment
```

Windows -> Same as long as PATH configured:

```
c:\>python -m venv c:\path\to\myenv
```

_____
ACTIVATE VENV :

__replace `_<venv>_` with path to directory containing virtual environment.__

Bash/ZSH:
```
source _<venv>_/bin/activate
```

PowerShell : 
```
C:\ _<venv>_\Scripts\Activate.ps1
```

cmd.exe ;
```
C:\ _<venv>_\Scripts\activate.bat
```



Documentation : https://docs.python.org/3/library/venv.html
## MORE

A virtual environment may be “activated” using a script in its binary directory (<span style="color:rgb(212, 95, 17)">`bin` on POSIX</span>; <span style="color:rgb(255, 0, 0)">`Scripts` on Windows)</span>. This will prepend that directory to your `PATH`, so that running **python** will invoke the environment’s Python interpreter and you can run installed scripts without having to use their full path. 

__The invocation of the activation script is platform-specific (`_<venv>_` must be replaced by the path to the directory containing the virtual environment):__

| Platform | Shell      | Command to activate virtual environment |
| -------- | ---------- | --------------------------------------- |
| POSIX    | bash/zsh   | `$ source _<venv>_/bin/activate`        |
|          | fish       | `$ source _<venv>_/bin/activate.fish`   |
|          | csh/tcsh   | `$ source _<venv>_/bin/activate.csh`    |
|          | PowerShell | `$ _<venv>_/bin/Activate.ps1`           |
| Windows  | cmd.exe    | `C:\> _<venv>_\Scripts\activate.bat`    |
|          | PowerShell | `PS C:\> _<venv>_\Scripts\Activate.ps1` |

From : **https://docs.python.org/3/library/venv.html**







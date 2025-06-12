## Oh-My-Posh Installation on Windows PowerShell v5.1
---

### 1. Installation
There are number of ways you can install Oh-My-Posh. But commonly you install Oh-My-Posh either from _PSGallery_ by using PowerShell's ***'Install-Module'*** command or with Oh-My-Posh supplied platform-specific install instructions like ***'Winget'*** on their website. Hence you can choose to run any one of the following.

#### If you want to use 'winget', run following:

```pwsh
winget install JanDeDobbeleer.OhMyPosh -s winget
```

#### If you want to use PSGallery 'Install-Module', run the following:

```pwsh
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```

_<sub>For the PATH to be reloaded, a restart of your terminal is advised<sub>_

 </br>

####  _Note: Path to oh-my-posh module directory ($Env:PSModulePath)_

The path of the module installation depends upon the '-Scope' used in the module installation command above.
_The acceptable values for this parameter are _'AllUsers'_ and _'CurrentUser'_._
>
> The **AllUsers** scope installs modules in a location that's accessible to all users of the computer:
>
> _$env:ProgramFiles\WindowsPowerShell\Modules_
>
> The **CurrentUser** installs modules in a location that's accessible only to the current user of the computer. For example:
>
> _$HOME\Documents\WindowsPowerShell\Modules_
>
_<sub> When no Scope is defined, the default is set based on the PowerShellGet version. </sub>_
_<sub> In PowerShellGet versions 2.0.0 and above, the default is CurrentUser, which doesn't require elevation for install. </sub>_
_<sub> In PowerShellGet 1.x versions, the default is AllUsers, which requires elevation for install. </sub>_

 </br>

####  _Note: Path to PowerShell Home Directory ($PSHOME)_
```pwsh
C:\Windows\System32\WindowsPowerShell
```

</br>

### 2. List Default Available Themes

To display every available theme in the current directory, use the following cmdlet.
```pwsh
Get-PoshThemes
```
The module installs all themes in the module folder. To find the actual files, you can use the following command:
```pwsh
Get-PoshThemes -list
```

</br>

### 3. Edit Profile to Replace Existing Prompt

Edit your PowerShell $PROFILE and add the following lines to load Oh-My-Posh module and theme of your choice at startup. Autocompletion is available so it will loop through all available themes. Refer the [last section](https://gist.github.com/adojos/d7904b76af760430ad086473da759d97#point_right-powershell-profile-path) of this gist to know the location of your PowerShell profile.

```pwsh
Import-Module oh-my-posh
Set-PoshPrompt -Theme jandedobbeleer
```

</br>

### 4. Update Oh-My-Posh Module
In order to update oh-my-posh module to latest available version, run one of the following:


#### If using 'winget', run the following:

```pwsh
winget upgrade JanDeDobbeleer.OhMyPosh -s winget
```

#### If using PSGallery, 'Update-Module', run the following:

```pwsh
Update-Module oh-my-posh
```

</br>

### 5. Install Dev Fonts (Glyph)

Oh My Posh was designed to use Nerd Fonts. Nerd Fonts are popular fonts that are patched to include icons. We recommend ***Meslo LGS NF***, but any Nerd Font should be compatible with the standard themes.

To see the icons displayed in Oh My Posh, install a Nerd Font, and configure your terminal to use it.

</br>

####  _Note: PowerShell Profile Path_

* Find out where the configuration file is

    ```pwsh
    AllUsersAllHosts -       C:\Windows\System32\WindowsPowerShell\v1.0\profile.ps1

    AllUsersCurrentHost -    C:\Windows\System32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1

    CurrentUserAllHosts -    C:\Users\UserName\Documents\WindowsPowerShell\profile.ps1

    CurrentUserCurrentHost - C:\Users\UserName\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
    ```
* You can check the execution policy first

    ```pwsh
    Get-ExecutionPolicy -List
    ```
* The result should be as the following output
    ```pwsh
            Scope ExecutionPolicy
            ----- ---------------
        MachinePolicy       Undefined
           UserPolicy       Undefined
              Process       Undefined
          CurrentUser       Restricted
         LocalMachine       Restricted
    ```
* For above last command work for WindowsPowerShell-5

    ```pwsh
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

* To disable logo go to setting and edit Command Line to

    ```pwsh
    %SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -NoLogo
    ```

* To have autocompletion work, install the following module in WindowsPowerShell

    ```pwsh
    Install-Module -Name PSReadLine -Force -SkipPublisherCheck
    ```

* Set the following commands

    ```pwsh
    Set-PSReadlineOption -HistoryNoDuplicates
    Set-PSReadlineOption -HistorySaveStyle SaveIncrementally
    ```

</br>

#### Git Bash

* Add the following line

    ```bash
    eval "$(oh-my-posh --init --shell bash --config c:/Users/say_o/AppData/Local/Programs/oh-my-posh/themes/rabbit.omp.json)"
    ```

* to the file

    ```bash
    C:\Users\<UserName>\.bashrc
    ```

####  _Note: PowerShell Modules Path ($ENV: PSModulePath)_
```pwsh
CurrentUser -       C:\Users\UserName\Documents\WindowsPowerShell\Modules

AllUsersCurrentHost -    C:\Program Files\WindowsPowerShell\Modules

BuiltInModules (AllUsers) -    C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\


```
# WSL

```pwsh
\\wsl.localhost\Ubuntu-20.04\home\michael\.local\bin
\\wsl.localhost\Ubuntu-20.04\home\michael\.cache\oh-my-posh\themes\rabbit.omp.json
\\wsl.localhost\Ubuntu-20.04\home\michael\.profile
eval "$(oh-my-posh init bash --config '~/.cache/oh-my-posh/themes/rabbit.omp.json')"
```

# CMD

1. Install `clink` from [https://mridgers.github.io/clink/](https://mridgers.github.io/clink/)

1. To disable startup prompt message, execute the following command in cmd `clink autorun install -- --quiet`
1. In Windows Terminal settings, add `/k` flag to the `%SystemRoot%\System32\cmd.exe`. So, it would be `%SystemRoot%\System32\cmd.exe /k` 
1. Execute the `clink info` to see the installation directory of `scripts`
1. In my case, `C:\Users\Dell\AppData\Local\clink\`
1. Create a file called `oh-my-posh.lua` and add `load(io.popen('oh-my-posh init cmd --config "C:\\Users\\Dell\\AppData\\Local\\Programs\\oh-my-posh\\themes\\rabbit.omp.json"'):read("*a"))()`


# References

* [Oh-My-Posh](https://ohmyposh.dev/docs/installation/customize)
* [Terminal-Icon](https://github.com/devblackops/Terminal-Icons/tree/main)
* [Git Bash](https://github.com/JanDeDobbeleer/oh-my-posh/issues/566)
* [Windows PowerShell v5.1](https://gist.github.com/adojos/d7904b76af760430ad086473da759d97#file-oh-my-posh_winps_install-md)
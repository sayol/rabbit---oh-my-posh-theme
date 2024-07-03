## Oh-My-Posh Installation on Windows PowerShell v5.1
---

### 1. Installation
There are number of ways you can install Oh-My-Posh. But commonly you install Oh-My-Posh either from _PSGallery_ by using PowerShell's ***'Install-Module'*** command or with Oh-My-Posh supplied platform-specific install instructions like ***'Winget'*** on their website. Hence you can choose to run any one of the following.

#### If you want to use 'winget', run following:

```
winget install JanDeDobbeleer.OhMyPosh -s winget
```

#### If you want to use PSGallery 'Install-Module', run the following:

```
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
```
C:\Windows\System32\WindowsPowerShell
```

</br>

### 2. List Default Available Themes

To display every available theme in the current directory, use the following cmdlet.
```
Get-PoshThemes
```
The module installs all themes in the module folder. To find the actual files, you can use the following command:
```
Get-PoshThemes -list
```

</br>

### 3. Edit Profile to Replace Existing Prompt

Edit your PowerShell $PROFILE and add the following lines to load Oh-My-Posh module and theme of your choice at startup. Autocompletion is available so it will loop through all available themes. Refer the [last section](https://gist.github.com/adojos/d7904b76af760430ad086473da759d97#point_right-powershell-profile-path) of this gist to know the location of your PowerShell profile.

```
Import-Module oh-my-posh
Set-PoshPrompt -Theme jandedobbeleer
```

</br>

### 4. Update Oh-My-Posh Module
In order to update oh-my-posh module to latest available version, run one of the following:


#### If using 'winget', run the following:

```
winget upgrade JanDeDobbeleer.OhMyPosh -s winget
```

#### If using PSGallery, 'Update-Module', run the following:

```
Update-Module oh-my-posh
```

</br>

### 5. Install Dev Fonts (Glyph)

Oh My Posh was designed to use Nerd Fonts. Nerd Fonts are popular fonts that are patched to include icons. We recommend ***Meslo LGS NF***, but any Nerd Font should be compatible with the standard themes.

To see the icons displayed in Oh My Posh, install a Nerd Font, and configure your terminal to use it.

</br>

####  _Note: PowerShell Profile Path_
```
AllUsersAllHosts -       C:\Windows\System32\WindowsPowerShell\v1.0\profile.ps1

AllUsersCurrentHost -    C:\Windows\System32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1

CurrentUserAllHosts -    C:\Users\UserName\Documents\WindowsPowerShell\profile.ps1

CurrentUserCurrentHost - C:\Users\UserName\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
```

* For above last command work for WindowsPowerShell-5

```Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser```

* To disable logo go to setting and edit Command Line to

```%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -NoLogo```

</br>

#### Git Bash

* Add the following line

```eval "$(oh-my-posh --init --shell bash --config c:/Users/say_o/AppData/Local/Programs/oh-my-posh/themes/rabbit.omp.json)"```

* to the file

```C:\Users\<UserName>\.bashrc```

####  _Note: PowerShell Modules Path ($ENV: PSModulePath)_
```
CurrentUser -       C:\Users\UserName\Documents\WindowsPowerShell\Modules

AllUsersCurrentHost -    C:\Program Files\WindowsPowerShell\Modules

BuiltInModules (AllUsers) -    C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\

```
# References

* [Oh-My-Posh](https://ohmyposh.dev/docs/installation/customize)
* [Terminal-Icon](https://github.com/devblackops/Terminal-Icons/tree/main)
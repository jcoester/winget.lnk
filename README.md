# Winget.lnk

A simple shortcut to quickly upgrade your apps using [**winget**](https://learn.microsoft.com/windows/package-manager/winget/). *No nonsense. Just 4 KB.*

## Why use Winget.lnk?

> **Alice:** "winget upgrade" is two words! I don't need a shortcut for that!

> **Bob:** The shortcut is a visual reminder, a nudge, to occasionally check for updates. Beginners don’t need to remember any command prompts. Power users conveniently switch to custom prompts.

**Perfect for:**  
- Minimalists who believe less is more 🔧
- Friends who fear the command line 😱  
- Parents who forget updates exist 🧓  

## Features 

- **For Everyone:** Not everyone is tech-savvy. It helps you, family, and friends stay updated.
- **Shareable:** Create once, share anywhere. Copy it to a flash drive or send it via Email or a messenger.
- **Safe and Secure:** No explicit admin rights required, no execution policy changes, no browser interaction.
- **Full Control:** No autostart, no scheduling, no interruptions — you decide when to run.
- **Zero Nonsense:** No third-party tools, no background processes, no notifications.

![Basic Demo](images/Demo-Yes.gif)

## Create Winget.lnk in Under 30 Seconds

> The **creation script** creates a **winget.lnk** shortcut on the **Desktop**. It assigns **PowerShell as the target**, and icon 46 from **shell32.dll**. 

1. **Copy** the following script
   ```powershell
   New-Object -ComObject WScript.Shell | ForEach-Object {
       $shortcut = $_.CreateShortcut([System.Environment]::GetFolderPath('Desktop') + '\winget.lnk')
       $shortcut.TargetPath = 'C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe'
       $shortcut.Arguments = '-NoExit -Command "winget upgrade; Write-Host ''''; $i = Read-Host ''Upgrade all packages? (Y/N)''; if ($i -match ''^[Yy]$'') { winget upgrade --all } else { Write-Host '''' }"'
       $shortcut.IconLocation = '%SystemRoot%\System32\shell32.dll,46'
       $shortcut.Save()
   }

2. Press `Win + X`, then select **Windows PowerShell** or **Terminal** from the menu. 

3. **Paste (Right-Click)** the copied script into your **PowerShell** window. **Confirm** the multi-line warning. **Close** the window afterwards.
   
4. Once the shortcut is created, you can optionally pin it to your **Taskbar or Start Menu** for easy access. Run it **on Demand**.

## Technical info


The shortcut itself runs the following command in PowerShell:

```powershell
-NoExit -Command "
    winget upgrade; Write-Host '';                  # Lists available upgrades
    $i = Read-Host 'Upgrade all packages? (Y/N)';   # Asks user how to proceed
    if ($i -match '^[Yy]$') {                       
        winget upgrade --all                        # Y ✅ : Upgrades apps automatically. Prompts UAC only when needed.
    } else {
        Write-Host ''                               # N ❌ : Lets user run custom prompts. Convenient for power users.
    }"
```

![Custom Demo](images/Demo-No.gif)

Made with ❤️ for simplicity.

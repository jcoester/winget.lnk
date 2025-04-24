# Winget.lnk

A simple shortcut to quickly upgrade your apps using [**winget**](https://learn.microsoft.com/windows/package-manager/winget/). No installation, no nonsense.

**Easy for beginners, family and friends. Convenient for power users. Just 4 KB in size.**

## Why Winget.lnk?

- **Zero Nonsense:** No installation, no background processes, no notifications, no third-party tools.
- **Full Control:** No autostart, no scheduling, no interruptions — run it when you want.
- **Secure and Fast:** No explicit admin rights required, no execution policy changes, no browser interaction.

## Thought Process

**Q: _"winget upgrade" is two words! I don't need a shortcut for that!_**  
**A:** The shortcut is a visual reminder to occasionally check for updates. Beginners don’t need to remember any command prompts, and power users get a convenient custom prompt option.

## How to Use

Simply **[download Winget.lnk](https://raw.githubusercontent.com/jcoester/winget.lnk/main/winget.lnk)**. Pin it to your **Desktop, Taskbar, or Start menu**. Run it **on demand**.

![Basic Demo](images/Demo-Yes.gif)

## How It Works

*The shortcut runs the following command in PowerShell:*

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

Made for all no-nonsense lovers ❤️

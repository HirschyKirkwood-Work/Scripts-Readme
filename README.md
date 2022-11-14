If there is a script in the Google Drive that isn't here, it's probably not finished or not important for anyone besides me.

# Important
## Multi Office Installer
Presents  you with a few options for version of Office to install. Select one and press "OK."
## Oracle12CInstall
Run and go. It installs everything correctly. So simple, even a caveman could do it.
Now also copies the required .ora files after waiting for the installation to finish.
You just have to dismiss the java install window when it finishes.
## Oracle19install
Not as polished as 12c, but it's also a slightly different process. Will finish it at some point.
## Reinstall SCCM
Uninstalls and reinstalls SCCM. Should be in a fully operational state now. Sometimes it'll through false errors when deleting the CCM folders. Should be fine to ignore.
## Remoteupdates
Installs Windows and DCU updates (if DCU is already present on machine) remotely. Just feed it a machine name.
## Updates
This is for when you're updating a freshly imaged computer (Some of you don't do this, I'm looking at you. You know who you are.)

Monitor the script to say yes,no,etc to prompts. By default it will ask you if you have to install another version of office (does not uninstall for you) and Oracle.

It will detect model and run updates and install apps based on the brand. It will also give you machine name and MAC depending on the user running the script. Update lines 23 and 26 to match your username and computer name and it will output them to your C:\
```
function getMAC {
    Write-Host "Getting PTAG Passthrough MAC"
    Copy-Item -Recurse -Force '\\andrew.ad.cmu.edu\depts\acs\dsp\New Machine update flashdrive contents\ptag' C:\
    $PTAG =  & '\\andrew.ad.cmu.edu\depts\acs\dsp\New Machine update flashdrive contents\ptag\ptags.bat'| Select-String -Pattern  "Aux"
    $MAC = $PTAG -split('Aux Mac Value .... ')
    $hostname = $env:COMPUTERNAME
    $runner = $env:UserName
    if ( $runner -eq 'hkirkwoo') 
    {
        Write-Host "$MAC"
        echo "$MAC $hostname" | Out-File -FilePath "\\DSP-HIRSCHY-L\C$\MAC.txt"
    }
    else
    {
        #Do nothing
    }
}
```


# Process-Related scripts
## CopyFiles.ps1
No longer needed. Put it copies the Oracle .ora files.
## CurrentOU Run As admin
Runs gpupdate and prints out the current OU of machine it is run on. Must be run as admin
## FileMakerProFirewall
Sets firewall rues for FMP
## Gpresult.ps1
Just runs and opens a gpresult.
## RestartRemoteComputer (bat and ps1)
Just feed it the name and it will reboot
## GetRemovePassthroughMAC
Feed it a name and it will get you the MAC address. Dell only. (for some reason ptags doesn't work on non-laptops. This is a dell issue)
## Remote-Serial
Feed it a name and it will get the serial.
## RemoteAudioUpdates
Feed it a name and it will update the REaltek audio driver. This is only useful for the random audio issues we've been having as of November 2022. Wouldn't recommend using in the future.


# Other
## Edge Uninstall
Something I was testing a while back. 
## laps
Change account to your admin account. It will open Laps for you without jumping through hoops.
## Macgetter
Something I was playing around with. Should work, but not all that useful since we have Dell machines/
##Message
Sent a pop-up message to a computer. It shows your account name, so don't be too funny. (Internal pranks only)

# Unix
## grouperdecoder
Changes formating of grouper group to it's AD group form.
## MacFileSizeFinder
Shows an ordered list of subdirectories based on their size

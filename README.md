# NWN-Log-Rotator
The Neverwinter Nights Log Rotator is designed to parse, format, and colorize logs so that they may be shared and re-read. The log rotator can also optionally upload remotely to sftp. With the batch file below along with this, it is easy to fully automate logging in NWN in a colorful way! A very basic example of this in action is <a href="http://htmlpreview.github.io/?https://github.com/ravenmyst/NWN-Log-Rotator/blob/master/latest/advanced/NWNLog_2016_08_26_001006.html" target="_blank">here</a>.
<br />
<br />
**Required Files / Frameworks:**

- This script requires <a href="https://nodejs.org/en/">Node.js</a> to be installed. It is a Javascript VM that helps this script run.<br />
- Retrieve the latest [RavenLogRotator.js](../master/latest/RavenLogRotator.js) here on this repository and place it in **your** NWN Base directory.

**Enabling NWN Logging:**

1) Go to C:\Program Files (x86)\GOG\Neverwinter Nights Diamond Edition\ or **your** NWN Base directory. 

2) Open nwnplayer.ini and ensure that ClientEntireChatWindowLogging = 1 under "[Game Options]".

3) Start NWN, join a server, and spam a few chat lines through chat for the logger.  Close NWN.

4) Then in your NWN base directory go to /Logs and ensure nwclientLog1.txt exists and looks correct.

**Testing RavenLogRotator:**

1) Open a command prompt (Open the Start Menu, then click "Run...". In the dialog box, type "cmd" then hit enter).

2) Navigate to the path of **your** NWN install in the command prompt (cmd.exe):
```batch
cd C:\Program Files (x86)\GOG\Neverwinter Nights Diamond Edition\
```
3) Try calling RavenLogRotator in node.
```batch
node RavenLogRotator 
```

The following flags are all optional, but may be changed to specify your configuration:

| Flag  | Description | Default | Usage |
| ------------- | ------------- | ------------- | ------------- |
| -s | nwn server name | "" | -s sinfar |
| -u | upload to sftp | false | -u true |
| -p | path to log | "/Logs/nwclientLog1.txt" | -p "C:/nwnlogs/nwClientLog1.txt" |
| -d | log destination | "/Logs" | -p "C:/nwnlogs/" |
| -h | sftp hostname | "" | -h host.sftphostname.com |
| -l | sftp username | "" | -l mysftpusername |
| -k | sftp password | "" | -k mysftppassword |
| -g | sftp port | "" | -g 22 |
| -z | sftp directory| "" | -z "/nwnlogs" |
| -t | test only | false | -t true |
| -c | server name color | "FFFFFF" | -c 03FFFF |
| -m | minimum rows to log | "10" | -m 25 |

**Important:** Only if you ***are*** using using sftp enter this line to install ssh-sftp-client from the node package manager (npm).
```batch
npm install ssh2-sftp-client
```
If this command fails, try opening the command prompt as administrator and trying again. To accomplish this, right click the cmd.exe shortcut in the start menu and select *Run As Administrator*.

**Advanced Flag Usage Example:**

To test the usage of RavenLogRotator with advanced parameters, you can copy and paste this into the Command Prompt by right clicking in the black window and hitting paste (cmd.exe).
```
node RavenLogRotator -s servername -u true -p "C:/Source/nwClientLog.txt" -d "C:/DestinationWithNoSlashAtTheEnd" -h "mysftphostname" -l mysftpusername -k mysftppassword -g 22 -z "/mysftppath"
```

Repeat running it, changing flags and their values until you reach the desired operation. If was successful, it will create a .html file both in the destination (-d) and if you chose to upload in the sftp zone (-z).

**Automate Logging when playing NWN:**

**[NWN_Launcher.bat](../master/latest/NWN_Launcher.bat):** Basic Launcher Example.

If you play on a server with custom launchers (i.e. sinfarx.exe), you will need to do something a little different. 

**[NWN_Launcher_Sinfar.bat](../master/latest/NWN_Launcher_Sinfar.bat):** Server with Launcher Example (Requires to be *Run as Administrator*).

**Tips:** 

- If you play on multiple servers, it's easier to make a launcher for each, and then a shortcut on the desktop. Make sure the shortcuts are configured to *Run as Administrator*.

- Want to *hide* the command prompt in your shortcut? Easy! Download <a href="http://www.ntwind.com/blog/hstart-x64.html">hstart or hstart64</a> and unzip the exe in your NWN Base Directory. Once it's there, create a starter batch file.. that calls the Sample_NWN_Launcher.bat from above using the hstart to make it hidden. 
```batch
start /w /d "C:\Program Files (x86)\GOG.com\Neverwinter Nights Diamond Edition\" hstart64.exe /noconsole "Sample_NWN_Launcher.bat"
```
If you added hstart64.exe to your Windows\system32 folder you can call it from cmd like this;
```batch
start hstart64.exe /noconsole "C:\Program Files (x86)\GOG.com\Neverwinter Nights Diamond Edition\Sample_NWN_Launcher.bat" 
```
Once it works, you can make a shortcut to that batch file. Make sure the shortcuts are configured to *Run as Administrator*.
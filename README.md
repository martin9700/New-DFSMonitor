Version 2.6 - Now saves historical data in XML format instead of CSV, which will better preserve the [datetime] variable type. If you are running an older version and want to keep your historical data you must run Convert-DFSDataToXML once: http://community.spiceworks.com/scripts/show/1723-convert-dfsdatatoxml

DFS is a fantastic technology that Microsoft put together for sharing and replicating files. Unfortunately the tools for monitoring the replication leave a lot to be desired. What I wanted to do with this script is create a graph that would tell me how replication is going, something I could see and comprehend at a glance. This script not only gives you that, but it also keeps the detailed information from every time it's run, something you can review at the click of a button.

Setup: 

1. Create a directory 
2. Download the script and call it DFSMonitorWithHistory.PS1 and save it into that directory. 
3. Make sure you have a working web server. Figure out the path to the web directory. On IIS that would be: c:\inetpub\wwwroot (your path will vary depending on your installation). 
4. Edit the script, scroll down to the PARAM section and edit: 
4a. $DFSServers: This should be changed to your DFS servers. You should include every one in your DFS replication tree. They should be seperated by comma's and surrounded by quotes. IE: "server1,server2,server3" 
4b. $DaysToSaveData: this is how many days you want to keep data in history. I recommend no more then 7 days as any more will cause the script to run slower. 
4c. $DataLocation: Where you want to save your data. This includes the debug log and the raw data (in the form of a CSV). I recommend using the directory you created in step #1. 
4d. $OutputLocation: This is the path to your web site that you figured out in step #3. 
4e. $MaxThreads: This script uses multi-threading and limits the # of threads to 10. I don't recommend using any more as I found my systems actually got all of the data slower once the thread count got over 10 and you could also get more WMI errors with a higher thread count. So don't change it! 
5. Create a scheduled task. Set it to run every hour. 
5a. Command to run: Powershell.exe 
5b. Argument: -ExecutionPolicy Bypass -file c:\pathfromstep1\DFSMonitorWithHistory.ps1 
5c. Make sure to use a service account with sufficient rights 
5d. To see additional information for scheduling Powershell tasks, see: http://community.spiceworks.com/how_to/show/17736-run-powershell-scripts-from-task-scheduler 
6. Copy error_event.png from your Spiceworks install: C:\Program Files\pkg\gems\spiceworks_public-\images\icons\small to the same location you set in 4d above.

To view the built in help type:

Get-Help pathtoscript\DFSMonitorWithHistory.ps1 -Full

See the examples for running the script with custom parameters--you can now run different scans without editing code!

To see your results, navigate to your web server and use this file name: DFSMonitorGrid.html 
All past history is saved (link's are in the html page listed).

Rate and comment! Enjoy

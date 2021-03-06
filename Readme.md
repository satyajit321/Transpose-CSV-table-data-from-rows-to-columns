<div><strong>.Synopsis</strong><br /> &nbsp;&nbsp; This script is to Transpose csv table data from rows to columns.<br /> <strong>.DESCRIPTION</strong><br /> &nbsp;&nbsp; This script allows you to import a csv file and transpose the data inside just like you do it in Excel, with some limitations.<br /> &nbsp;&nbsp; Its irrespective of the length and size of the table. It automatically calculates and switches the rows to columns.<br /> &nbsp;&nbsp; Output is PSCustomObject that can be manipulated just like any other PSObject, Export-CSV or ft, fl etc.<br /> &nbsp;&nbsp; The view would not make much sense in console output, but when checked in Excel it would make lots of sense.<br /> &nbsp;&nbsp; <br /> &nbsp;&nbsp; Mainly on data that has less objects\rows and more columins\parameters. Transpose would make it look cleaner.</div>
<div>&nbsp;&nbsp; #The logic behind is slightly tricky, if you still want to know read through:<br /> &nbsp;&nbsp; 1.Csv file is imported and current headers extracted.<br /> &nbsp;&nbsp; 2.First element of the header and all the corresponding values for that parameter is used as input for new PS Object header<br /> &nbsp;&nbsp; 3.2nd element of header and remaining old header info forms the first column\entry of the new objects<br /> &nbsp;&nbsp; 4.The other values are also similarly placed after one another<br /> &nbsp;&nbsp; 5.All the objects are collected in an array and moved out.</div>
<div><strong>.Errors\Troublshooting:</strong><br /> &nbsp;&nbsp; *This script requires you to have atleast PowerShell V3.0 onwards to run as it utilizes many features introduced in v3.<br /> &nbsp;&nbsp; *Make sure there is data in the Header and the First Column is filled, if blank it will throw error.<br /> &nbsp;&nbsp; *Make sure there is no duplicate data in the header and the first column. They must be unique.</div>
<div>&nbsp;&nbsp; @Author: Satyajit Aug 2015</div>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>PowerShell</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">powershell</span>
<pre class="hidden">.EXAMPLE
   .\Transpose.ps1 | ft

.EXAMPLE
   Example of how to use this cmdlet
   .\Transpose.ps1 -InputFile .\ProcessData.csv | ft
.EXAMPLE
   Another example of how to use this cmdlet
   .\Transpose.ps1

.EXAMPLE
This is how the original and converted data looks like.

PS Transpose&gt; Import-Csv .\ProcessData.csv

Name                                 Status                               DisplayName
----                                 ------                               -----------
p2pimsvc                             Stopped                              Peer Networking Identity Manager
p2psvc                               Stopped                              Peer Networking Grouping
PcaSvc                               Running                              Program Compatibility Assistant
PeerDistSvc                          Running                              BranchCache
PerfHost                             Stopped                              Performance Counter DLL Host
pla                                  Stopped                              Performance Logs &amp; Alerts


PS Transpose&gt; .\Transpose.ps1 -InputFile .\ProcessData.csv | ft

Name       p2pimsvc   p2psvc     PcaSvc     PeerDistSv PerfHost   pla
                                            c

----       --------   ------     ------     ---------- --------   ---
Status     Stopped    Stopped    Running    Running    Stopped    Stopped
Display... Peer Ne... Peer Ne... Program... BranchC... Perform... Perform...

PS Transpose&gt; .\Transpose.ps1 -InputFile .\ProcessData.csv | fl


Name             : Status
p2pimsvc         : Stopped
p2psvc           : Stopped
PcaSvc           : Running
PeerDistSvc      : Running
PerfHost         : Stopped
pla              : Stopped

Name             : DisplayName
p2pimsvc         : Peer Networking Identity Manager
p2psvc           : Peer Networking Grouping
PcaSvc           : Program Compatibility Assistant Service
PeerDistSvc      : BranchCache
PerfHost         : Performance Counter DLL Host
pla              : Performance Logs &amp; Alerts

.EXAMPLE
Use this example to export the transposed data back to a CSV, without type details.

.\Transpose.ps1 -InputFile .\ProcessData.csv | Export-Csv ProcessDataT2.csv  -NoTypeInformation</pre>
<div class="preview">
<pre class="powershell">.EXAMPLE&nbsp;
&nbsp;&nbsp;&nbsp;.\Transpose.ps1&nbsp;<span class="powerShell__operator">|</span>&nbsp;<span class="powerShell__alias">ft</span>&nbsp;
&nbsp;
.EXAMPLE&nbsp;
&nbsp;&nbsp;&nbsp;Example&nbsp;of&nbsp;how&nbsp;to&nbsp;use&nbsp;this&nbsp;cmdlet&nbsp;
&nbsp;&nbsp;&nbsp;.\Transpose.ps1&nbsp;<span class="powerShell__operator">-</span>InputFile&nbsp;.\ProcessData.csv&nbsp;<span class="powerShell__operator">|</span>&nbsp;<span class="powerShell__alias">ft</span>&nbsp;
.EXAMPLE&nbsp;
&nbsp;&nbsp;&nbsp;Another&nbsp;example&nbsp;of&nbsp;how&nbsp;to&nbsp;use&nbsp;this&nbsp;cmdlet&nbsp;
&nbsp;&nbsp;&nbsp;.\Transpose.ps1&nbsp;
&nbsp;
.EXAMPLE&nbsp;
This&nbsp;is&nbsp;how&nbsp;the&nbsp;original&nbsp;and&nbsp;converted&nbsp;<span class="powerShell__keyword">data</span>&nbsp;looks&nbsp;like.&nbsp;
&nbsp;
<span class="powerShell__alias">PS</span>&nbsp;Transpose&gt;&nbsp;<span class="powerShell__cmdlets">Import-Csv</span>&nbsp;.\ProcessData.csv&nbsp;
&nbsp;
Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Status&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DisplayName&nbsp;
<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;
p2pimsvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peer&nbsp;Networking&nbsp;Identity&nbsp;Manager&nbsp;
p2psvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peer&nbsp;Networking&nbsp;Grouping&nbsp;
PcaSvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Running&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Program&nbsp;Compatibility&nbsp;Assistant&nbsp;
PeerDistSvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Running&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BranchCache&nbsp;
PerfHost&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Performance&nbsp;Counter&nbsp;DLL&nbsp;Host&nbsp;
pla&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Performance&nbsp;Logs&nbsp;<span class="powerShell__operator">&amp;</span>&nbsp;Alerts&nbsp;
&nbsp;
&nbsp;
<span class="powerShell__alias">PS</span>&nbsp;Transpose&gt;&nbsp;.\Transpose.ps1&nbsp;<span class="powerShell__operator">-</span>InputFile&nbsp;.\ProcessData.csv&nbsp;<span class="powerShell__operator">|</span>&nbsp;<span class="powerShell__alias">ft</span>&nbsp;
&nbsp;
Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;p2pimsvc&nbsp;&nbsp;&nbsp;p2psvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PcaSvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PeerDistSv&nbsp;PerfHost&nbsp;&nbsp;&nbsp;pla&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c&nbsp;
&nbsp;
<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;&nbsp;&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;&nbsp;&nbsp;<span class="powerShell__operator">-</span><span class="powerShell__operator">-</span><span class="powerShell__operator">-</span>&nbsp;
Status&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;&nbsp;&nbsp;&nbsp;Running&nbsp;&nbsp;&nbsp;&nbsp;Running&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;&nbsp;&nbsp;&nbsp;Stopped&nbsp;
Display...&nbsp;Peer&nbsp;Ne...&nbsp;Peer&nbsp;Ne...&nbsp;Program...&nbsp;BranchC...&nbsp;Perform...&nbsp;Perform...&nbsp;
&nbsp;
<span class="powerShell__alias">PS</span>&nbsp;Transpose&gt;&nbsp;.\Transpose.ps1&nbsp;<span class="powerShell__operator">-</span>InputFile&nbsp;.\ProcessData.csv&nbsp;<span class="powerShell__operator">|</span>&nbsp;<span class="powerShell__alias">fl</span>&nbsp;
&nbsp;
&nbsp;
Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Status&nbsp;
p2pimsvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Stopped&nbsp;
p2psvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Stopped&nbsp;
PcaSvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Running&nbsp;
PeerDistSvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Running&nbsp;
PerfHost&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Stopped&nbsp;
pla&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Stopped&nbsp;
&nbsp;
Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;DisplayName&nbsp;
p2pimsvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Peer&nbsp;Networking&nbsp;Identity&nbsp;Manager&nbsp;
p2psvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Peer&nbsp;Networking&nbsp;Grouping&nbsp;
PcaSvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Program&nbsp;Compatibility&nbsp;Assistant&nbsp;Service&nbsp;
PeerDistSvc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;BranchCache&nbsp;
PerfHost&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Performance&nbsp;Counter&nbsp;DLL&nbsp;Host&nbsp;
pla&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Performance&nbsp;Logs&nbsp;<span class="powerShell__operator">&amp;</span>&nbsp;Alerts&nbsp;
&nbsp;
.EXAMPLE&nbsp;
Use&nbsp;this&nbsp;example&nbsp;to&nbsp;export&nbsp;the&nbsp;transposed&nbsp;<span class="powerShell__keyword">data</span>&nbsp;back&nbsp;to&nbsp;a&nbsp;CSV,&nbsp;without&nbsp;<span class="powerShell__alias">type</span>&nbsp;details.&nbsp;
&nbsp;
.\Transpose.ps1&nbsp;<span class="powerShell__operator">-</span>InputFile&nbsp;.\ProcessData.csv&nbsp;<span class="powerShell__operator">|</span>&nbsp;<span class="powerShell__cmdlets">Export-Csv</span>&nbsp;ProcessDataT2.csv&nbsp;&nbsp;<span class="powerShell__operator">-</span>NoTypeInformation</pre>
</div>
</div>
</div>
<div class="endscriptcode">Sample&nbsp;Input File&nbsp;:</div>
<div class="endscriptcode"><a id="141230" href="/scriptcenter/site/view/file/141230/1/ProcessData.csv">ProcessData.csv</a>&nbsp;</div>
<div>&nbsp;</div>
<div>Sample Output from Export-CSV:</div>
<div><a id="141231" href="/scriptcenter/site/view/file/141231/1/ProcessDataT2.csv">ProcessDataT2.csv</a></div>
<div>&nbsp;</div>

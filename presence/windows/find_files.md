<!-- Code for collapse and expand -->
<script type="text/javascript"> 
$(document).ready(function() { 
$('div.view').hide(); 
$('div.slide').click(function() {
$(this).next('div.view').slideToggle('fast'); 
return false; 
}); 
}); 
</script>

# Windows Finding File Commands

Commands that find files on the filesystem and are usually executed from the context of the `cmd.exe` or `command.exe` prompt.

## dir
### Attributes Showing
 * **Command with arguments**: `dir /a`
 * **Description**: Displays files with specified attributes. Examples: D=Directories, R=Read-only files, H=Hidden files, A=Files ready for archiving, S=System files
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>dir /a c:\<br> Volume in drive C has no label. Volume Serial Number is 1A09-5F16<br><br> Directory of c:\<br><br>01/19/2008  03:45 AM    <DIR>          $Recycle.Bin<br>09/18/2006  04:43 PM                24 autoexec.bat<br>10/08/2013  10:27 PM    <DIR>          Boot<br>04/11/2009  08:00 AM           333,257 bootmgr<br>10/08/2013  10:27 PM             8,192 BOOTSECT.BAK<br>09/18/2006  04:43 PM                10 config.sys<br>01/19/2008  06:47 AM    <JUNCTION>     Documents and Settings [C:\Users]<br>10/23/2013  07:39 PM     2,460,454,912 pagefile.sys<br>01/19/2008  04:40 AM    <DIR>          PerfLogs<br>10/08/2013  06:36 PM    <DIR>          Program Files<br>10/08/2013  06:36 PM    <DIR> <br>10/10/2013  07:59 PM    <DIR>          Users<br>10/23/2013  07:38 PM    <DIR>          Windows<br>               5 File(s)  2,460,796,395 bytes<br>              10 Dir(s)  33,311,416,320 bytes free</code></div> 

### Searching Sub-directories
 * **Command with arguments**: `dir /s *[term]*` 
 * **Description**: Searches for the word entered in the [term]  section in all sub-directories ofthe current directory.
 * **Example Terms**: `pass`, `cred`, `vnc`, `.config`, `sysprep.*`
 * **Attribution**: http://www.slideshare.net/mubix/windows-attacks-at-is-the-new-black-26665607

### Recursive
 * **Command with arguments**: `dir /b /s [directory or filename]`
 * **Description**: Displays files recursively (all subdirectories). Good for post processing with find (example: `find /I “searchstring”`) or sending to another tool.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>dir /b /s c:\temp<br>c:\Users\Default\AppData\Local\Temp<br>c:\Users\johndoe\AppData\Local\Temp<br>c:\Windows\Temp<br>c:\Windows\assembly\temp<br>c:\Windows\assembly\NativeImages_v2.0.50727_32\Temp<br>c:\Windows\System32\DriverStore\Temp<br>c:\Windows\winsxs\Temp</code></div> 
----   

## find
 * **Command with arguments**: `[somecommand] \| find /c /v ”[searchstring]”`
 * **Description**: Counts the number of times the [searchstring] is found in the output of [somecommand].
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>dir /a /s c:\  |find /c /v "svchost"
99184</code></div>
----

## tree
 * **Command with arguments**: `tree C:\ /f /a > C:\output_of_tree.txt`
 * **Description**: Prints a directory listing in tree format. The `/a` makes the tree printed with ASCII characters instead of special ones and the `/f` displays file names as well as folders.
 * **Output**:
   * <div class="slide" style="cursor: pointer;"> **Windows 2008:** Show/Hide</div><div class="view"><code>C:\Users\johndoe>tree C:\ /f /a<br>Folder PATH listing<br>Volume serial number is 1A09-5F16<br>C:\<br>|   autoexec.bat<br>|   config.sys<br>|<br>+---PerfLogs<br>+---Program Files<br>|   +---Common Files<br>|   |   +---microsoft shared<br>|   |   |   +---DAO<br>|   |   |   |       dao360.dll<br>|   |   |   |<br>|   |   |   +---ink<br>|   |   |   |   |   penchs.dll<br>|   |   |   |   |   pencht.dll<br>|   |   |   |   |   penjpn.dll<br>|   |   |   |   |   penkor.dll<br>|   |   |   |   |   penusa.dll<br>|   |   |   |   |   pipanel.dll<br>|   |   |   |   |   pipanel.exe<br>|   |   |   |   |   pipres.dll<br>|   |   |   |   |   skchobj.dll<br>|   |   |   |   |   skchui.dll<br>|   |   |   |   |<br>|   |   |   |   +---ar-SA<br>|   |   |   |   |       tipresx.dll.mui<br>|   |   |   |   |<br>[...SNIP...]</code></div> 

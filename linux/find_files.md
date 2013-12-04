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

# Linux finding files commands

Commands that finds files on the file system are usually executed from within a shell (sh/bash) or through a forking function such as system() or exec().

## ls
### Attributes showing
 * **Command with arguments**: `ls -l [directory or filename]`
 * **Description**: Displays attributes of files and directories in the specified location
 * **Output**:
 * <div class="slide" style="cursor: pointer;"> **Ubuntu:** Show/Hide</div><div class="view"><code>
    total 429820
    drwxr-xr-x   2 root root      4096 2013-08-23 02:49 bin
    drwxr-xr-x   3 root root      4096 2013-08-23 03:18 boot
    drwxr-xr-x   2 root root      4096 2011-03-05 11:41 cdrom
    drwxr-xr-x  15 root root      4600 2013-11-25 15:43 dev
    drwxr-xr-x 158 root root     12288 2013-12-04 15:54 etc
    drwxr-xr-x   4 root root      4096 2013-05-02 07:19 home
    lrwxrwxrwx   1 root root        21 2012-03-01 08:11 initrd.img -> boot/initrd.img-3.2.6
    drwxr-xr-x  25 root root     16384 2013-08-23 02:50 lib
    drwx------   2 root root     16384 2011-03-05 11:40 lost+found
    drwxr-xr-x   4 root root      4096 2013-08-04 22:31 media
    drwxr-xr-x   3 root root      4096 2012-03-04 19:14 mnt
    -rw-r--r--   1 root root      1045 2012-08-13 23:52 nis
    drwxr-xr-x  12 root root      4096 2013-08-23 03:02 opt
    drwxr-xr-x  25 root root      4096 2013-08-23 02:54 pentest
    dr-xr-xr-x 148 root root         0 2013-11-25 15:36 proc
    drwx------  77 root root      4096 2013-12-04 15:58 root
    -rw-r--r--   1 root root 440006761 2012-10-01 00:09 root.tgz
    drwxr-xr-x   2 root root     12288 2013-08-23 02:51 sbin
    drwxr-xr-x   2 root root      4096 2009-12-05 16:55 selinux
    drwxr-xr-x   4 root root      4096 2011-05-10 03:42 share
    drwxr-xr-x   4 root root      4096 2013-04-17 21:25 srv
    drwxr-xr-x  12 root root         0 2013-11-25 15:36 sys
    drwxrwxrwt  12 root root      4096 2013-12-04 01:00 tmp
    drwxr-xr-x  13 root root      4096 2013-08-23 02:52 usr
    drwxr-xr-x  16 root root      4096 2011-06-08 09:16 var
    lrwxrwxrwx   1 root root        18 2012-03-01 08:11 vmlinuz -> boot/vmlinuz-3.2.6
    </code></div>

----

## command
### Attributes showing
 * **Command with arguments**: `command --help`
 * **Description**: Displays files recursively 
 * **Output**:
 * <div class="slide" style="cursor: pointer;"> **OS:** Show/Hide</div><div class="view"><code> ... </code></div>

----

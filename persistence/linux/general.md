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

# Linux General Persistence Commands

Commands to run to maintain persistence after you have exploited it and are usually executed from the context of the bash prompt.

###Run command as a daemon
*Note this doesn't work with anything from apache. Runs like & but doesn't care if the parent process closes*
```bash
setsid *command*
```


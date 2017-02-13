# macos-userlibrary-migration

Helper for migration of macOS user settings

## Overview
Most peaple are just fine copying their data and settings from one macOS installation to another by just using the migration tool. I did this for several years now, never had a problem. Now my harddrive failed without prediction, due to some I/O errors parts of the library rendered unusable. I needed a fresh start with my user directory. This is what I found out:
As far as concerning you user data, follow the [guide which Matt Gemmel wrote](http://mattgemmell.com/manually-migrating-to-a-new-mac/).

For migration of your settings (mail accounts, signatures, adressbook, calendars), you need to migrate you "User Library" and this is what this article is about.

The process shown here has been tested on macOS `Sierra`, make sure source and target macOS installation have the same version.

## Password database migration

The KeyChain holds your passwords. I did not copy the keychain file over in this process to prevent possible account corruption.  If you’ve forgotten some passwords you can copy your old keychain to a temporary place on your new installation and use the Keychain Utility (located inside `/Applications/Utilities`) to view the contents of your old user keychain.  

The keychain file can be found on the old drive at: `~/Library/Keychains/login.keychain`.

## Export old library settings
Copying of settings to USB stick or network drive

### Preparation
Assuming you want to export your settings to `Library2` directory in your home directory, prepare an export directory structure like:

```
mkdir ~/Library2
mkdir ~/Library2/Containers
mkdir ~/Library2/Preferences
mkdir ~/Library2/SyncedPreferences
```

### Mail, calendar, addressbook and internet accounts

See [apple forum](https://discussions.apple.com/thread/7312611?tstart=0) for details, this worked for me:

```
cp -a ~/Library/Accounts ~/Library2/
cp -a ~/Library/Containers/com.apple.AddressBook ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.AddressBook..InternetAccountsBridge ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.AddressBook.ContactsAccountsService ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.AddressBook.FaceTimeService ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.CalendarAgent ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.CalendarAgent.CalNCService ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.CalendarFileHandler ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.CalendarNotification.CalNCService  ~/Library2/Containers/
cp -a ~/Library/Containers/com.apple.mail ~/Library2/Containers/
cp -a ~/Library/Mail ~/Library2/
cp -a ~/Library/Mail\ Downloads ~/Library2/
cp -a ~/Library/Preferences/com.apple.AddressBook.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.apple.MailMigratorService.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.apple.accounts.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.apple.accountsd.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.apple.mail-shared.plist ~/Library2/Preferences/
cp -a ~/Library/SyncedPreferences/com.apple.mail-com.apple.mail.vipsenders.plist ~/Library2/SyncedPreferences/
cp -a ~/Library/SyncedPreferences/com.apple.mail.plist ~/Library2/SyncedPreferences/
```

### System-wide dictionary
This is where you personal dictionaries are beeing stored, containing all accepted exceptions from standard language which you seem to need:

```
mkdir ~/Library2/Spelling
cp -a ~/Library/Dictionaries ~/Library2/
cp -a ~/Library/Spelling/LocalDictionary ~/Library2/Spelling
```

You may want to search the internet for word lists matching your hobbies or profession, there are

* [Unix/Linux](https://en.wikipedia.org/wiki/Words_(Unix)) 

word lists which you can put under `~/Library/Preferences/Dictionaries`

### Other applications

Maybe of interest: Terminal, Atom, Google, Teamviewer and XEE3 settings. Dig yourself through your `Library` and ``Library/Application Support` to get an idea what is configured for you personally
```
cp -a ~/Library/Preferences/com.apple.Terminal.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.apple.TextEdit.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.github.atom.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.google.Chrome.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.teamviewer.TeamViewer.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.teamviewer.teamviewer.preferences.Machine.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/com.teamviewer.teamviewer.preferences.plist ~/Library2/Preferences/
cp -a ~/Library/Preferences/cx.c3.Xee3.plist ~/Library2/Preferences/
```

## Import exported library contents to new installation

This can be done right after account creation, before first user login (from your administrative initial user account, which is not meant for every-day use). 
Just copy you exported library stuff from USB stick or network drive into the new library directory of the newly created user and adapt permissions:

```
mkdir <new-user-home>/Library
cp -a Library2/* <new-user-home>/Library/
chown -R <new-user> <new-user-home>/Library/
```

After login with the new account, you will be asked for some passwords and are ready to go.

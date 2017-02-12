# macos-userlibrary-migration# Migrating macOS user settings

Most peaple are just fine copying their data and settings from one macOS installation to another by just using the migration tool. I did this for 10 years now, never had a problem. By now, some failures slowly creep in, resulting in some applications to take very long time to finish their stuff.
In case you want to have a clean start, you need to run a manual migration of you data and settings.  As far as concerning you user data, follow the [guide which Matt Gemmel wrote](http://mattgemmell.com/manually-migrating-to-a-new-mac/). For migration of you settings (mail accounts, signatures, adressbook, calendars), you need to migrate you "User Library" and this is what this article is about.

## Migrating the library
Tested on macOS `Sierra`, make sure source and target os have the same version.

### Keychain
The KeyChain holds your passwords. I did not copy it over this process to prevent possible account corruption.  If you’ve forgotten some passwords you can use the Keychain Utility (located inside `/Applications/Utilities`) to view the contents of your old user keychain.  

The keychain file can be found on the old drive at: `~/Library/Keychains/login.keychain`.

### Prepare library settings transfer
Assume you want to export your settings to `Library2` directory in your home directory:
```
mkdir ~/Library2
mkdir ~/Library2/Containers
mkdir ~/Library2/Preferences
mkdir ~/Library2/SyncedPreferences
```

### mail, calendar, addressbook and internet accounts

* see [apple forum](https://discussions.apple.com/thread/7312611?tstart=0):

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



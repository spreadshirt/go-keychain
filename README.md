# Go Keychain

A library for accessing the Keychain for OSX and iOS.

Requires Mac OSX 9 or greater and iOS 7 or greater.

**WARNING**: This is still being tested and reviewed.

## Usage

```go
item := keychain.NewGenericPassword("MyService", "gabriel", []byte("toomanysecrets"), "com.corp")
item.SetSynchronizable(keychain.SynchronizableNo)
item.SetAccessible(keychain.AccessibleWhenUnlocked)
err := keychain.AddItem(item)
if err == keychain.KeychainErrorDuplicateItem {
  // Duplicate
}

accounts, err := keychain.GetAccounts("MyService")
// Should have 1 account == "gabriel"

err := keychain.DeleteGenericPasswordItem("MyService", "gabriel")
if err == keychain.KeychainErrorNotFound {
  // Not found
}
```


## Tests

Tests are in `bind`.

## iOS

Bindable package in `bind`. iOS project in `ios`. Run that project to test iOS.

```
gomobile bind -target=ios -o ios/bind.framework github.com/keybase/go-keychain/bind
```
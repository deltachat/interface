# Testing Checklist

## Preparation

**Alice** will be the tester. You need 
- an E-Mail address 
- and the release candidate build
- a Thunderbird installation with Enigmail or TB-AC.

**Bob** is the "sparring partner" of Alice. Can be a daily-use Delta Chat
Desktop account. You need
- an E-Mail address
- Delta Chat Desktop version >= 0.840.0

**Charlie** is the second account of Alice.

## Tests

- [ ] Installing the release candidate build on Alice' phone works.
- Alice sends a message to the e-mail address of Bob:
    - [ ] Does it arrive?
- Bob answers Alice with another message:
    - [ ] Does it arrive?
    - [ ] Do you get a notification?
    - [ ] Is it encrypted?
- Alice sends a file to Bob:
    - [ ] Is it encrypted?
    - [ ] Can Bob open it?
- Alice creates a group and adds Bob as a member
    - [ ] Does Bob receive the group invite?
    - [ ] Is it encrypted?
- [ ] Alice tries to search for Bob in her contact list
- [ ] Alice does a contact verification with Bob
- Bob creates a verified group
    - [ ] Alice joins the group via a QR scan
    - [ ] Can Alice send a message to the group?
    - [ ] Is it encrypted?
    - [ ] If Bob replies, does Alice receive the reply?
    - [ ] Is it encrypted?
- [ ] Alice blocks Bob
    - [ ] Bob sends Alice a message, but she doesn't receive it
- [ ] Alice unblocks Bob
    - [ ] Bob sends Alice a new message, and she receives it this time
- Autocrypt Setup Messages
    - [ ] Alice initiates an Autocrypt Setup Message in Android
    - [ ] Can Alice import it in another device?
    - [ ] Alice sends an Autocrypt Setup Message from another client: can Alice import it in Android?
- Disable: Settings -> Advanced -> Prefer end-to-end encryption
    - [ ] If you send out a mail afterwards, does it contain an "Autocrypt: prefer-encrypt=nopreference; " header?
- Backup & Restore
    - [ ] Export Backup: Settings -> Chats & Media -> Backup
    - Delete account: Phone Settings -> Apps -> DeltaChat -> Clear Data
    - Open App again, tap restore from backup
    - [ ] Is everything still there?
- [ ] Alice logs out
- [ ] Charlie logs in on Alice's device
- [ ] Bob writes a message to Charlie
    - [ ] Charlie finds the message in their Contact requests
    - [ ] Charlie clicks "Not Now" to not open a chat.
    - [ ] Bob sends another message to Charlie
    - [ ] Charlie finds the message in her Contact request and clicks "Never" this time
    - [ ] Bob sends Charlie another message, but Charlie doesn't receive it
- [ ] Alice archives her Chat with Bob; she doesn't see it anymore
- [ ] Bob writes her a mail, Alice receives it nonetheless, the chat is unarchived automatically

### Out of scope

Creating verified groups is out of scope for a community tester, until the
Desktop client can join verified groups.

Things which are already tested by automated tests, and don't have any UI,
don't need testing.


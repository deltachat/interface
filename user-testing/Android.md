# Android Checklist

### Preparation

**Alice** will be the tester. You need 
- an E-Mail address 
- and the release candidate build
- on a phone.
- a Thunderbird installation with Enigmail or TB-AC.

**Bob** is the "sparring partner" of Alice. Can be a daily-use Delta Chat
account on some other phone. You need
- an E-Mail address
- some Delta Chat version
- on a phone.

### Tests

- [ ] Installing the release candidate build on Alice' phone works.
- Alice sends a message to the e-mail address of Bob:
    - [ ] Does it arrive?
- Bob answers Alice with another message:
    - [ ] Does it arrive?
    - [ ] Do you get a notification?
    - [ ] Is it encrypted?
- Alice replies to Bob's message:
    - [ ] Is it encrypted?
- Alice creates a group and adds Bob as a member
    - [ ] Does Bob receive the group invite?
    - [ ] Is it encrypted?
- [ ] Alice does a contact verification with Bob
- Bob creates a verified group
    - [ ] Alice joins the group via a QR scan
    - [ ] Can Alice send a message to the group?
    - [ ] Is it encrypted?
    - [ ] If Bob replies, does Alice receive the reply?
    - [ ] Is it encrypted?
- Alice creates a verified group?
- Alice initiates an Autocrypt Setup Message in Android
    - [ ] Can Alice import it in another device?
    - [ ] Send an Autocrypt Setup Message from another client: can you import it in Android?
- Disable: Settings -> Advanced -> Prefer end-to-end encryption
    - [ ] If you send out a mail afterwards, does it contain an "Autocrypt: prefer-encrypt=mutual; " header?
- Backup & Restore
    - [ ] Export Backup: Settings -> Chats & Media -> Backup
    - Delete account: Phone Settings -> Apps -> DeltaChat -> Clear Data
    - Open App again, tap restore from backup
    - [ ] Is everything still there?


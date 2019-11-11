# Android Checklist

### Preparation

- create or get an existing test account ready


### Tests

- Send a message to the e-mail address of the contact
    - [ ] Does it arrive?
- The contact sends you a message
    - [ ] Does it arrive?
    - [ ] Do you get a notification?
    - [ ] Is it encrypted?
- Reply to the message of your contact
    - [ ] Is it encrypted?
- [ ] Create a group
- [ ] Invite your contact
- [ ] Do a contact verification
- Contact creates a verified group
    - [ ] Join the group via a qr scan
    - [ ] Send a message to the group: is it encrypted?
- Autocrypt Setup Message
    - [ ] Send an Autocrypt Setup Message: can you import it in another client?
    - [ ] Send an Autocrypt Setup Message from another client: can you import it in Android?
- Disable: Settings -> Advanced -> Prefer end-to-end encryption
    - [ ] If you send out a mail afterwards, does it contain an "Autocrypt: prefer-encrypt=mutual; " header?
- Backup & Restore
    - [ ] Export Backup: Settings -> Chats & Media -> Backup
    - Delete account: Phone Settings -> Apps -> DeltaChat -> Clear Data
    - Open App again, tap restore from backup
    - [ ] Is everything still there?


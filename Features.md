# This is WIP  - don't rely on it util this notice is gone

Last update: 
05/22/2019 @ 11:15pm (UTC)

## Features
What the clients have to implement to be feature complete. This can act as a checklist when implementing a new client.
*Only those which are already possible with the current core.*
  
- Searching
  - For Chats
  - For Messages by content

- Chat Managment
  - Archiving
  - Deleting
  - Mute chat notefications
  - Chat List
  - Change Name
  - New Chat
    - PM / DM chat (chat with one contact)
    - Group
    - Verified Group
  - Groups
    - Add/remove members
    - leave a group
    - Display Group Avatar
    - Change Group Avatar
  - Contact Requests

- Out-of-Band Verification
  - join verified group
  - verify an contact
  - Methode
    - QR-code + message (online)

- Contact Managment
  - Blocking Contacts
  - Adding Contacts
  - Deleting Contacts

- Messages
  - Text
    - Emoji Picker
  - Attachment
    - Video
    - Image
    - Audio
    - File
  - Location Attribute
  - Drafts
  - Star Message
  - Forward message
  - Copy message contens to Clipboard
  - mark as read
  - Show message info

- Location streaming
  - Display on Map
    - Point of interest
    - Paths from Location Streaming
    - Controls
     - Shown Timeframe
     - add new POI
  - Display a map for all chats

- Migration functionality
  - Backup
    - Import
    - Export
  - Autocrypt Key Transfer
    - Export
    - Import

- Settings
  - Watch Folders
  - Toggle moving emails to DeltaChat Folder
  - Send read notefications
  - Contact Request Settings heavyly (discussed on the forum [chat-interaction-setting])
  - Option to change mail signature
  - Login
    - change Credentials after Login
    - oAuth
  - Change Display name

- Integration with the System
  - Notifications
    - Setting Mute Chats
  - Attachments
    - (Drag 'n Drop)
    - (Share/Send with deltachat association)
  - Recording in app
    - recording voicemessages
    - (taking pictures / videos in app)
  - Location streaming
    - (Streaming own Location)
  - Contacts
    - (Accessing the systems contacts)

- Development
  - Tests
    - (Unit Tests)
    - CI for building
  - Deployment
    - Download Links to download latest stable version
    - recent Screenshot for Website/Readme
    - Explaination how to compile it (+ waht dependencies are required)

- MISC
  - Theming
    - Dark / Light theme
    - Changeable Chat Background/Wallpaper
  - Progress indicators for things like Backup and Login

Legend:
(only if that makes sense on the platform)

## Future

### Future Roadmap
What we plan to add in the Future. (This List is neiter complete nor final and will probably never be.)

- A/V Calls (probably over WebRTC) [forum topic (webRTC)](https://support.delta.chat/t/webrtc-for-communicating/410/15) [forum topic (video chat)](https://support.delta.chat/t/video-chat-integration/388)
- show Chat encryption state [forum post](https://support.delta.chat/t/show-end-to-end-encryption-state-of-chat/230)
  - Indicator wether current message will be sent encrypted


### Feature Requests

- Sending a Single Location as Attachment [forum post](https://support.delta.chat/t/send-location-only-one-time-android-v-0-301/380/2?u=schiminieee)
- Search for Messages by other Means
  - Search by Date [forum topic](https://support.delta.chat/t/make-it-possible-for-users-to-search-through-messages-using-the-calendar-tool/351)

- in app help/FAQ [forum topic](https://support.delta.chat/t/add-faq-and-search-feature/342)

- QR-Code Verification/ Join to group
  - Improvement to QR-Code contact verification (offline mode) [forum topic](https://support.delta.chat/t/release-the-basic-qr-code-contact-scanning-feature-independently/44)

- Multi Account [forum topic](https://support.delta.chat/t/multi-accounts-profiles-support/179/7)

- Avatar Pictures for Contacts (like Profile Pictures that the user can set instead using the ones from the system contacts)

More can be found on the [forum](https://support.delta.chat/c/features)

### Heavily Discussed Topics about compatibility to clasic MUA

- Subject of emails in clasic MUA [https://support.delta.chat/t/subject-of-emails/264]
- [[Discussion] Make DC a replacement for MUAs?](https://support.delta.chat/t/discussion-make-dc-a-replacement-for-muas/253)

- Contact Requests
  - [Make Contact Requests more visible](https://support.delta.chat/t/make-contact-requests-more-visible/196)
  - [Notify contact requests](https://support.delta.chat/t/notify-contact-requests-lets-discuss-about-this/190)



[chat-interaction-setting]: https://support.delta.chat/t/more-useful-chat-interaction-setting/381

# Deltachat URI-Schemes

Currently URI schemes are mainly supported by the app-internal QRcode scanner, at this time only `openpgp4fpr` (used for securejoin) is also registered as uri scheme handler on all platforms ([android](https://github.com/deltachat/deltachat-android), [ios](https://github.com/deltachat/deltachat-ios) and [desktop](https://github.com/deltachat/deltachat-desktop))

- related forum topic: https://support.delta.chat/t/custom-deltachat-url-uri-scheme/346
- core sourcecode that handles uri schemes: https://github.com/deltachat/deltachat-core-rust/blob/master/src/qr.rs and https://github.com/deltachat/deltachat-core-rust/blob/master/src/securejoin/qrinvite.rs

## **chat.delta**

Generic deltachat scheme, currently used by android as callback url for the oauth2 login method.
| | |
| ------------------- | ------------------------------- |
| Scheme | `chat.delta` |
| Used for | oauth2 Login (only android currently) |
| Related Terms\* | - |
| Available on | iOS (defined, but not used yet), android |
| Handled by the core| No|
| Other apps using it | none, only DeltaChat |
| Notes | Only used as scheme currently, not in qr codes |

### Syntax

[TODO]

### Reference

https://github.com/deltachat/deltachat-android/blob/8d9c02dd7a2be33fe588e0b9469be56fb0435a62/AndroidManifest.xml#L192-L195

```xml
<!-- this scheme is used as the redirect_url for getOauth2Url()
    and should be whitelisted by the supported oauth2 services -->
<data android:scheme="chat.delta" android:path="/${applicationId}/auth" tools:ignore="AppLinkUrlError"/>
<data android:scheme="chat.delta" android:path="/auth" tools:ignore="AppLinkUrlError"/>
```

## **OPENPGP4FPR** <a name="OPENPGP4FPR"></a>

|                         |                                 |
| ----------------------- | ------------------------------- |
| Scheme                  | `OPENPGP4FPR:`                  |
| Used for                | Verify Contact and Join a group |
| Related Terms\*         | Securejoin                      |
| Available on            | iOS, android, desktop           |
| Decoded by the core\*\* | Yes                             |
| Other apps using it     | <li>OpenKeychain(android)</li>  |

### Syntax

```
OPENPGP4FPR:FINGERPRINT#a=ADDR&n=NAME&i=INVITENUMBER&s=AUTH
OPENPGP4FPR:FINGERPRINT#a=ADDR&g=GROUPNAME&x=GROUPID&i=INVITENUMBER&s=AUTH
OPENPGP4FPR:FINGERPRINT#a=ADDR&b=BROADCAST_NAME&x=BROADCAST_ID&j=INVITENUMBER&s=AUTH
```

The fields `a`, `g`, `b`, and `n` are URL encoded.
`i` & `s` are 66 random bits endcoded as base-64.

> Note: Everything after `#` is a Delta Chat extension
>
> The `OPENPGP4FPR` scheme's data is also used for so called ["Invite Links"](#I-DELTA-CHAT)

#### Examples

verify contact

```
OPENPGP4FPR:EEA98F87742EF2FD6C23677F1E1142828C202998#a=demo.fn8hk%40five.chat&n=&i=rd82URz8_ac&s=MFRLUHvIHlq
```

join regular group

```
OPENPGP4FPR:EEA98F87742EF2FD6C23677F1E1142828C202998#a=demo.fn8hk%40five.chat&g=groupname2&x=iNekF7uW509&i=xW0ZAcLUQDf&s=OYV-PWe63Vv
```

join verified/protected group (same format as join regular group)

```
OPENPGP4FPR:EEA98F87742EF2FD6C23677F1E1142828C202998#a=demo.fn8hk%40five.chat&g=groupname&x=ylTH55NJF24&i=PpDNY9sRkh-&s=F8di8fNDToQ
```

## Invite Links: https://i.delta.chat <a name="I-DELTA-CHAT"></a>

|                         |                                                  |
| ----------------------- | ------------------------------------------------ |
| Universal link          | `https://i.delta.chat`                           |
| Used for                | Verify Contact and Join a group                  |
| Related Terms\*         | Securejoin, universal links                      |
| Available on            | iOS, android, desktop (only QR and paste)        |
| Decoded by the core\*\* | Yes                                              |
| Other apps using it     | No, not possible without a pr to the invite repo |

"Invite Links" are an alternative to scan each other's QR code to get in contact or to join groups.

The existing [OPENPGP4FPR](#OPENPGP4FPR) links have 2 major problems:
they are not usable by people who don't have Delta Chat installed
and they are not linkified (and thus not shareable) on 3rd party platforms.

The "Invite Links" solve these problems:

- You can share them over any 3rd party platform.
- If recipients taps the links, they are
  either offered to install Delta Chat and tap an "Open Chat" link
  or, depending on the platform, an installed Delta Chat opens directly without even going to the website.

> Since the 1.44 releases the qr codes that you copy to clipboard have this format.

### Syntax

```
https://i.delta.chat/#FINGERPRINT&a=ADDR&n=NAME&i=INVITENUMBER&s=AUTH
https://i.delta.chat/#FINGERPRINT&a=ADDR&g=GROUPNAME&x=GROUPID&i=INVITENUMBER&s=AUTH
https://i.delta.chat/#FINGERPRINT&a=ADDR&b=BROADCAST_NAME&x=BROADCAST_ID&j=INVITENUMBER&s=AUTH
```

The syntax is the same as in [OPENPGP4FPR](#OPENPGP4FPR) with two differences:

- `OPENPGP4FPR:` is replaced by `https://i.delta.chat/#`
- The `#` that comes directly after the `FINGERPRINT` is replaced by an `&` character.
  - This is to make browsers and operating systems handle the link correctly

Note, that all data are added to the [URI Fragment](https://en.wikipedia.org/wiki/URI_fragment),
by that, no user data is sent to the server.

#### Examples

get in contact / verify contact

```
https://i.delta.chat/#EEA98F87742EF2FD6C23677F1E1142828C202998&a=demo.fn8hk%40five.chat&n=&i=rd82URz8_ac&s=MFRLUHvIHlq
```

join regular group

```
https://i.delta.chat/#EEA98F87742EF2FD6C23677F1E1142828C202998&a=demo.fn8hk%40five.chat&g=groupname2&x=iNekF7uW509&i=xW0ZAcLUQDf&s=OYV-PWe63Vv
```

join verified/protected group (same format as join regular group)

```
https://i.delta.chat/#EEA98F87742EF2FD6C23677F1E1142828C202998&a=demo.fn8hk%40five.chat&g=groupname&x=ylTH55NJF24&i=PpDNY9sRkh-&s=F8di8fNDToQ
```

### Related Links

- Sourcecode of the website `https://i.delta.chat`: <https://github.com/deltachat/invite/>
- The file that tell apple which apps are allowed to handle this universal link: https://github.com/deltachat/invite/blob/main/.well-known/apple-app-site-association
- Deeplinking on the different platforms
  - Apple Universal Links: https://developer.apple.com/ios/universal-links/
  - Android App Links: https://developer.android.com/training/app-links/

## **DCACCOUNT** <a name="DCACCOUNT"></a>

|                          |                                                    |
| ------------------------ | -------------------------------------------------- |
| Scheme                   | `DCACCOUNT:`                                       |
| Used for                 | Account setup                                      |
| Related Terms\*          | Burner Accounts                                    |
| Available on             | iOS (only QR), android(only QR), desktop (only QR) |
| Decoded by the core \*\* | Yes                                                |
| Other apps using it      | none, only DeltaChat                               |

### Syntax

This scheme contains either the domain name of a chatmail server or an HTTPS URL.

If domain name is used, e.g. as `DCACCOUNT:example.org`,
then the client should generate a 9-character alphanumeric lowercase username,
e.g. `ipvzrws6x@example.org`,
and a password that is at least 30 characters long,
drawn from the full set of alphanumeric characters (`A-Z`, `a-z`, `0-9`).

If URL is used, e.g. `DCACCOUNT:https://example.org/new_email?t=1w_7wDjgjelxeX884x96v3`,
then the client should make an HTTP/1.1 GET request
and receive account setup information as a JSON object.
See the [mailadm](https://github.com/deltachat/mailadm) project for more details as this API was designed for use with burner account QR codes generated by mailadm.

You may want to use [`DCLOGIN`](#DCLOGIN) instead, if you want a qr code containing login information for a single account.

#### The HTTP endpoint needs the following api:

##### On Success

HTTP Status code 200

```ts
{
    email: string,
    password: string
}
```

json object can have other properties too, but currently they are ignored by core.

##### On Error

HTTP Status code: NOT 2XX, idealy the 4XX if it's user error and 5XX if it's the servers fault

```ts
{
    // The user facing error string, should explain what failed.
    error: string,
}
```

json object can have other properties too, but currently they are ignored by core.

## **DCLOGIN** <a name="DCLOGIN"></a>

|                          |                       |
| ------------------------ | --------------------- |
| Scheme                   | `DCLOGIN:`            |
| Used for                 | Account setup         |
| Related Terms\*          | Account Login QR code |
| Available on             | android, ios, desktop, deltatouch |
| Decoded by the core \*\* | YES                   |
| Other apps using it      | none, only DeltaChat  |

### Syntax

The generic URI schema is:

URI = scheme ":" ["//" authority] path ["?" query] ["#" fragment]
authority = [userinfo "@"] host [":" port]

For DCLOGIN this means:

- _scheme_ is always dclogin
- There must be an _authority_ section
  - The _userinfo_ part is required.
- The _path_ may be omitted or be a single `/`.
- The fragment must be omitted.
- The query parameters are described down below.

Examples:

```
dclogin://user@host/?p=password&v=1[&options]
# example: (email: me@example.com, password: securePassword)
dclogin://me@example.com?p=securePassword&v=1
# example: (email: myself@example.com, password: url/Encoded\@passw@rd)
dclogin://myself@example.com?p=url%2FEncoded%5C%40passw%40rd&v=1
# example: (email: myself@example.com, password: 123456, insecure smtp at different server)
dclogin://myself@example.com?p=123456&v=1&sh=mail.example.com&sc=3&ss=plain
```

#### Options `?options`

Format: URL Query parameters also known as GET variables (`varname=value` behind the question mark, chained/delimited by `&`)

The query parameters contain advanced options and a version parameter.
All advanced options are optional except for `v` and `p`, which are the only required options at this point.
(BTW: Later/Other versions in the future might specify a different authentication and thus `p` might become unnecessary in those formats.)

| short name | stands for                | description                                         | example               |
| ---------- | ------------------------- | --------------------------------------------------- | --------------------- |
| `v`        | `version`                 | defines the format version, more explanation below  | `v=1`                 |
| `p`        | `password`                | required in version 1, password of the account      |                       |
| ---------- | ------------------------- | --------------------------------------------------- | ----------------      |
| `ih`       | `imap_host`               | IMAP host                                           | `ih=imap.example.com` |
| `ip`       | `imap_port`               | IMAP port                                           | `ip=993`              |
| `iu`       | `imap_username`           | IMAP username                                       |                       |
| `ipw`      | `imap_password`           | IMAP password                                       |                       |
| `is`       | `imap_security`           | IMAP security: "`ssl`" or "`default`" or "`plain`"  | `is=ssl`              |
| `ic`       | `imap_certificate_checks` | IMAP certificate checks, see below for options      | `ic=1`                |
| ---------- | ------------------------- | --------------------------------------------------- | ----------------      |
| `sh`       | `smtp_host`               | SMTP host                                           | `sh=mail.example.com` |
| `sp`       | `smtp_port`               | SMTP port                                           | `sp=465`              |
| `su`       | `smtp_username`           | SMTP username                                       |                       |
| `spw`      | `smtp_password`           | SMTP password                                       |                       |
| `ss`       | `smtp_security`           | SMTP security: "`ssl`", "`starttls`" or "`plain`"   | `ss=plain`            |
| `sc`       | `smtp_certificate_checks` | SMTP certificate checks, see below for options      | `sc=3`                |

#### format version

Format version:
Used for breaking new versions that add new **required** properties, basically deltachat checks for this and if it's newer than the version deltachat supports it prompts the user to update the app.

The version number only increases on incompatible changes (changes to required properties).

#### `CertificateChecks`

New versions of Delta Chat do not have separate options for IMAP certificate checks and SMTP certificate checks.
**For best compatibility both `ic` and `sc` must be always set to the same value.**
`sc` is actually ignored by new Delta Chat and `ic` is used to configure both IMAP and SMTP certificate checks.

| code | name & description                                                                                               |
| ---- | ---------------------------------------------------------------------------------------------------------------- |
| 0    | `Automatic`, same as `AcceptInvalidCertificates` unless overridden by `strict_tls` setting in provider database. |
| 1    | `Strict`                                                                                                         |
| 3    | `AcceptInvalidCertificates`                                                                                      |

#### Important information for using the `DCLOGIN:` scheme

- There is a maximum length of how much data fits in side of a qr code (depending on the error correction level 1273 chars to 2953 chars)
  - only use the short names for advanced properties
  - If working with long domains/password/usernames in advanced options, **consider creating a configuration file at the server instead** using either [Autoconfigure](https://web.archive.org/web/20210402044801/https://developer.mozilla.org/en-US/docs/Mozilla/Thunderbird/Autoconfiguration)
- **Every value** (username & password too) **needs to be URI encoded**:
  - [`encodeURIComponent()` in JS](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)

#### Implementation hints

implementations should be somewhat tolerant:

- both `dclogin:` and `dclogin://` should work (though only `dclogin://` is technically correct)
- **only** implement short names (not the full names they stand for)
- have a test for usename+extension@host cases
- if version number is higher than what is implemented, tell the user to update

## **DCBACKUP**

|                     |                                                   |
| ------------------- | ------------------------------------------------- |
| Scheme              | `DCBACKUP:`                                       |
| Used for            | transferring a backup to another deltachat device |
| Related Terms\*     | -                                                 |
| Available on        | android, ios, desktop                             |
| Decoded by the core | Yes                                               |
| Other apps using it | No                                                |

### Syntax

```
DCBACKUP:data
```

The `data` itself contains an encoded `iroh::provider::Ticket`
structure serialised using it's `Display` trait. Ultimately that
implementation is the reference but here the details:

- The ticket itself consists of this struct:
  ```
  struct Ticket {
      hash: [u8; 32],
      peer: [u8; 32],
      addrs: Vec<SocketAddr>,
      token: [u8; 32],
  }
  ```
- This ticket is serialised to bytes using
  [postcard](https://postcard.jamesmunns.com/).
- These bytes are encoded using Base64 URL SAFE without padding.

#### Examples

This shows what a ticket looks like in practice.

```
DCBACKUP:IA84ohZpKlLVQaIe0AEejanGo2CCKmAgMQJLIcmO4Kp5IFNwcau_-xuQ2AhMSVWmodA63wUY7YmhSDVQh6tuCE8WAQB_AAAB0SJh2W8_TB3azsiP88tJXNEi554F4M7Q_jTw2_EnMdvrvQ
```

## **mailto** <a name="MAILTO"></a>

Usable as share to deltachat.

|                     |                                                              |
| ------------------- | ------------------------------------------------------------ |
| Scheme              | `mailto:`                                                    |
| Used for            | sharing to deltachat, creating a contact                     |
| Related Terms\*     | -                                                            |
| Available on        | android, desktop (own decoding), [TODO does ios support it?] |
| Decoded by the core | Yes, partially (only extracts address and creates contact)   |
| Other apps using it | most other email clients                                     |

### Syntax

```
mailto:[addr]?subject=[subject]&body=[body]
```

standard mailto syntax though deltachat might not respect all options yet, probably refer to https://tools.ietf.org/html/rfc2368 and https://tools.ietf.org/html/rfc6068.

## **SMTP** (unused?)

similar to [`mailto:`](#MAILTO)

|                     |                                                            |
| ------------------- | ---------------------------------------------------------- |
| Scheme              | `SMTP:`                                                    |
| Used for            | sharing to deltachat, creating a contact                   |
| Related Terms\*     | -                                                          |
| Available on        | ? [TODO]                                                   |
| Decoded by the core | Yes, partially (only extracts address and creates contact) |
| Other apps using it | ?                                                          |

### Syntax

```
SMTP:[addr]:[subject]:[body]
```

## **MATMSG** (unused?)

similar to [`mailto:`](#MAILTO)

|                     |                                                            |
| ------------------- | ---------------------------------------------------------- |
| Scheme              | `MATMSG:`                                                  |
| Used for            | sharing to deltachat, creating a contact                   |
| Related Terms\*     | -                                                          |
| Available on        | ? [TODO]                                                   |
| Decoded by the core | Yes, partially (only extracts address and creates contact) |
| Other apps using it | ?                                                          |

### Syntax

```
MATMSG:TO:[addr];SUB:[subject];BODY:[body];
```

## **BEGIN:VCARD**

|                     |                     |
| ------------------- | ------------------- |
| Scheme              | `BEGIN:VCARD`       |
| Used for            | importing a contact |
| Related Terms\*     | vcard               |
| Available on        | ? [TODO]            |
| Decoded by the core | Yes                 |
| Other apps using it | ?                   |

### Syntax

```
VCARD:BEGIN\nN:last name;first name;...;\nEMAIL;<type>:addr...;
```

## **Telegram Socks5 Proxy Codes** <a name="telegram-socks5-proxy">

|                     |                                                              |
| ------------------- | ------------------------------------------------------------ |
| Scheme              | `https://t.me/socks`                                         |
| Used for            | importing a proxy config                                     |
| Available on        | adding a proxy url on all platforms (not as system handler)  |
| Decoded by the core | Yes                                                          |
| Other apps using it | Telegram                                                     |
| Specification       | https://core.telegram.org/api/links#socks5-proxy-links       |

### Syntax

```
https://t.me/socks?server=<ip>&port=<port>&user=<user>&pass=<pass>
```

### Examples

```
https://t.me/socks?server=foo&port=666
https://t.me/socks?server=1.2.3.4
https://t.me/socks?server=jau&user=Da&pass=x%26%25%24X
```

## URI schemes that are qrcode reader only

- `http://` & `https://` - to make the qr code scanner more complete and allow users to scan common qr codes.

## Registered Handlers per Platform

List of which schemes the app is registered to handle in the OS.
When an scheme is reqistered as a handler

| Platform | Schemes                                                                                                                                                             | Sources (and a keyword to look for when the line-numbers have changed)                                                                                                                                                                                                                                                                                                                               |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| iOS      | [`mailto:`](#MAILTO)\*\*\*, `chat.delta`, [`openpgp4fpr:`](#OPENPGP4FPR), [`dclogin:`](#DCLOGIN), [`dcaccount:`](#DCACCOUNT), [https://i.delta.chat](#I-DELTA-CHAT) | [deltachat-ios/Info.plist](https://github.com/deltachat/deltachat-ios/blob/master/deltachat-ios/Info.plist#L28-L32) CFBundleURLSchemes                                                                                                                                                                                                                                                               |
| android  | [`mailto:`](#MAILTO), `chat.delta`, [`openpgp4fpr:`](#OPENPGP4FPR), [`dclogin:`](#DCLOGIN), [`dcaccount:`](#DCACCOUNT), [https://i.delta.chat](#I-DELTA-CHAT)       | [AndroidManifest.xml](<[https://github.com/deltachat/deltachat-android/blob/8d9c02dd7a2be33fe588e0b9469be56fb0435a62/AndroidManifest.xml](https://github.com/deltachat/deltachat-android/blob/master/AndroidManifest.xml)>) search for `android:scheme`                                                                                                                                              |
| desktop  | [`mailto:`](#MAILTO)\*\*\*, [`openpgp4fpr:`](#OPENPGP4FPR), [`dclogin:`](#DCLOGIN), [`dcaccount:`](#DCACCOUNT)                                                      | [build/gen-electron-builder-config.js](https://github.com/deltachat/deltachat-desktop/blob/b7340a22349e3c11e2938ef0532732db8e12bd7a/build/gen-electron-builder-config.js#L21-L33) build['protocols'] <br /> [src/main/windows/main.ts#L61](https://github.com/deltachat/deltachat-desktop/blob/988bade7c44b17665f91d013e04d8a5a877c6889/src/main/windows/main.ts#L61) app.on('open-url', ...) <br /> |

Caveat: the flathub version has sometimes problems in the support of uri schemes see: https://github.com/flathub/chat.delta.desktop/issues/115

## Footnote / Legend

\* terms that are used in the project that are related to it. Sometimes there are multiple terms refering to the same thing, for example contact requests are still sometimes refered to as "dead drops".

\*\* wether the core has logic to detect and decode it

\*\*\* not usable yet, does not work out of the box on desktop and for iOS we need to request permission from apple

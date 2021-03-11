# Markdown in messages

> This list is for every formating thing that goes beyond plain-text.

Deltachat is going to support the following subset of markdown:

### `*italics*` and `_italics_`

No whitespace as first nor as end char:
correct:

```
*italics* test
*italics test*
```

wrong:

```
* italics* test
```

### `**bold**` and `__bold__`

No whitespace as first nor as end char: see italics examples.

### `~~strikethrough~~`

No whitespace as first nor as end char: see italics examples.

### `https://delta.chat` - Urls

Make URLs clickable.

### `<http://example.org>` - Urls

### `` `inline-code` ``

useful to send non markdown text in your message like source code snippets.
Should get rendered in a monospace font and with a different background.
In contrast to bold, italics and strikethrough the content of inline-code can contain spaces at begining and ending.

### ` ``` fence code block ``` `

```
Similar to `inline-code` but not inline and it may supports code highlighting.
```

` ```[lang?] [content]``` ` (square brakets symbolize being a variable and are not used when using code blocks)
A bit modified from the common syntax to allow one liners.
Also get displayed with an monospace font (a side effect of this is that it allows to display small ascii art).
The code **highlighting** is **optional** as implementation (time)cost
may not be worth the small gain.
The `language` definition should be parsed separately and omitted in this case.

see https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#code-and-syntax-highlighting

examples:

<pre>```sh
echo hi
```</pre>
<pre>```
echo hi
```</pre>
<pre>```sh echo hi```</pre>
<pre>``` echo hi```</pre>


### `:emoji:`

- could also be used for custom dc emojis

### labeled links: `[Name](url)` links

When implementing this make sure to show the user the hidden url in a confirmation dialog to make scamming harder.
Also show the url as encode punycode to make punycode attacks useless.
Optionaly a client can implement a system to trust an domain (an "don't ask a again for links on this domain" checkbox in the confirmation dialog)

### Bot `/commands`

On click the command gets prefilled as the draft so it can be easialy send.

## `#tag`

Basically a clickable search shortcut. On click it opens the message search prefilled with that tag.

Inspired by twitters and telegrams #hashtag funtionality.

## Future:

### `mailto:email@address.example.com`

Make mailto links clickable with all parameters: `?subject=Sample%20Subject&body=Sample%20Body`

### Custom Deltachat URI Scheme

see https://support.delta.chat/t/custom-deltachat-url-scheme/346

### Mentions `@username`

Clickable. (could get replaced with an user hash/email/id on send/on recieve so that it's still valid on name change.)

On sending/recieving this is tranformed into an internal representation:

Implementation idea:

1. user types @Displayname and at best gets autocompletion while typing the url
2. on sending the username is converted to the transmition format (special format that contains the email address as id)
3. on recieving/storing the message inside of the database this format is converted again to contain the local contact id to allow for future email address migration/rotation.
   (4.) on forwarding/sharing as chat history the id representation needs to be converted from the contact id format to the transmition format again

see discords mention code for reference/inspiration https://blog.discordapp.com/how-discord-renders-rich-messages-on-the-android-app-67b0e5d56fbe

### $[inline TeX]$ $$[Tex displayed in block(new line)]$$

for sharing math/physics equations in LaTeX format.
see https://support.delta.chat/t/latex-code-in-deltachat/558

## Things that will not be suported:

- Inline HTML
- underline - can be confused with links

## other / internal

- Text
- linebreaks

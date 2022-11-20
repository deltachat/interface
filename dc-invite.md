# DC Invite

todo why?

todo what?


## How?

Deltachat will register to the following domains
- `https://invite.delta.chat/*` - official instace hosted by us 
- `https://dcinvite.*` - subdomain on any server for people that would like to selfhost it

Site MUST use HTTPS.

There is one single static site hosted there (sourcecode on https://github.com/deltachat/invite).

The site will be opened in DC if its installed, if not a website is shown with installation instructions and a button to open the link again (for now an alternative link from out own custom schemes, we don't know if desktop supports listening on https domains yet.)

The data is sent in the anchor part so not sent to the server like:

invite.delta.chat/#[data]

and has the following format: TBD


link could have different index html directories:

```
index.html - if no hash - explaination of how to get such a link
index.html# with hash - for person
group/index.html - for group

```
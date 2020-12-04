Testing mailto links
====================

Just click on all of these links and check if the result is the expected one:

* [Just an email address](mailto:abc@example.org) - should open a chat with `abc@example.org` (and maybe ask whether a chat should be created if it does not exist already)
* [email address with subject](mailto:abc@example.org?subject=testing%20mailto%20uris) - should open a chat with `abc@example.org` and fill `testing mailto uris`; as we created the chat in the previous step, it should not ask `Chat with …` but directly open the chat
* [email address with body](mailto:abc@example.org?body=this%20is%20a%20test) - should open a chat with `abc@example.org`, draft `this is a test`
* [email address with subject and body](mailto:abc@example.org?subject=testing%20mailto%20uris&body=this%20is%20a%20test) - should open a chat with `abc@example.org`, draft `testing mailto uris` \<newline\> `this is a test`
* [HTML encoding](mailto:%20info@example.org) - should open a chat with `info@example.org`
* [more HTML encoding](mailto:simplebot@example.org?body=!web%20https%3A%2F%2Fduckduckgo.com%2Flite%3Fq%3Dduck%2520it) - should open a chat with `simplebot@example.org`, draft `!web https://duckduckgo.com/lite?q=duck%20it`
* [no email, just subject&body](mailto:?subject=bla&body=blub) - this should let you choose a chat and create a draft `bla` \<newline\> `blub` there

---
layout: post
title: "LG Env Touch + Mac - Contacts"
date: 2009-08-08 13:22:38
categories:
- personal
- computing
---
Stumbled upon a really simple but effective way to copy your contacts from
your [OS/X](http://www.apple.com/macosx/ "Apple Mac OS/X")
[Address Book](http://www.apple.com/macosx/what-is-macosx/mail-ical-address-book.html "Apple Mac Address Book")
onto an [LG Env Touch](http://en.wikipedia.org/wiki/LG_enV_(VX9900) "LG Env Touch on Wikipedia").
The beauty is in how seamlessly the bluetooth operates between the Mac and the
phone.

The tool is an AppleScript called SendContacts.  You simply create a group in
Address Book named
"[SendContacts](http://ccsoftwarefactory.com/SendContacts/ "SendContacts Home")",
drag the addresses you'd like to copy to the phone into this group and then
execute the script.  The script opens Address Book if it's not already open
and copies the addresses in the special group.  My phone is setup to query me
if an upload is requested so I unlocked my phone, confirmed the upload and
away the script runs.  It took only a few seconds to copy around 70 contacts.

Nice.

Since a phone is used to, umm, make calls, I created my "SendContacts" group
as a Smart Group defining only those contacts for whom a phone number is
available:

{% img center /images/2009/08/sendcontacts-smartgroup-screenshot.png "Contacts Smart Group" "Using a Smart Group to Define Contacts to Send" %}

Kudos to
[Apple](http://www.apple.com/support/bluetooth/ "Apple Bluetooth Support"),
[LG](http://www.lge.com/products/category/list/mobile%2520phone.jhtml "LG Mobile Phones"),
and the [Bluetooth Consortium](http://www.bluetooth.org/ "Bluetooth") for
making this all so easy and to [C+C Software Factory](http://www.ccsoftwarefactory.com/)
for creating such a nice utility!

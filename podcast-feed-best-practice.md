gPodder Podcast Feed Best Practice
==================================

**Document Status: very early draft**

This document contains best practices for creating podcast feeds that should be
consumed by podcasting clients. It aims to be a guideline for podcast
publishers and systems creating podcast feeds on behalf of them, as well as for
podcast clients need to interpret those feeds.

This document is published by the [gPodder team] [gpodder] but aims for general
compatability among podcast applications.


Preface
-------

RSS and Atom feeds are commonly used to distribute and describe podcasts. Due
to their generic definition, they can be ambigously interpreted for the use
case of podcasts. This often resulted in incompatible uses of these standards
which then caused problems when processing some podcast feeds.

This document builds upon existing standards and established extensions, and
gives recommendations how these standards should be put to use. It should not
conflict with any standard that is mentioned.


Conventions
-----------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][RFC2119].


Feed Format
-----------

* TODO: RSS? Atom?


Feed Contents
-------------

One feed should describe one show, and its episodes.


### Contents

* Title
* Link
* Description
* Image / Cover
* Payment URL


Media Files
-----------

* TODO: How to handle multiple formats?
* TODO: Which audio/video formats are recommended? Is there a comprehensive/authoritative list of open source codecs?



Feed Meta Data
--------------

* TODO: Author information? 
* TODO Related feeds? 
* TODO Self-reference? Canonical URL?
* TODO: How to match uniquely identify an author among multiple feeds? Email?


Episode
-------

An episode describes one recording (?) of a podcast's show.

* TODO: number and order of episodes?
* TODO: alternative feeds with other selection of episodes


### Contents

* GUID
* Title
* Link
* Description
* Duration
* Publication DAte
* Payment URL



Enclosure
---------

### Contents

* Link
* Media Type
* File Size
* Length



Availability
------------

Each feed should have exactly one cannonical URL. A permanent redirect should
be used to indicate that the feed has moved to a different URL. Clients are
then instructed to updated the URL stored for the feed, and access the redirect
target directly in the future.

* TODO: how about RSS Redirects: http://cyber.law.harvard.edu/rss/rssRedirect.html ?
* TODO: how about <itunes:new-feed-url> ? 




References
----------

[RFC2119]: http://www.ietf.org/rfc/rfc2119.txt "RFC 2119 Key words for use in RFCs to Indicate Requirement Levels"
[gpodder]: https://github.com/gpodder/ "gPodder projects"


Authors
-------

* Stefan Kögl <stefan@skoegl.net>

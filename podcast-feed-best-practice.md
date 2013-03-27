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

[RSS][rss20] and [Atom][rfc4287] feeds are commonly used to distribute and
describe podcasts. Due to their generic definition, they can be ambigously
interpreted for the use case of podcasts. This often resulted in incompatible
uses of these standards which then caused problems when processing some podcast
feeds.

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

* TODO: [RSS][rss20]? [Atom][rfc4287]?
* TODO: Encoding? Always UTF-8? Defined in HTTP headers or in
  the content? iTunes [requires
  UTF-8](http://www.apple.com/itunes/podcasts/specs.html#encoding)


Podcast
-------

One feed describes one podcast and its episodes. There MAY be multiple feeds
describing different views of the same podcast (eg different media types,
different number and or selection of episodes, etc). See section
*Related Feeds*.


### Contents
* Title
* Link
* Description
* Image / Cover
* Payment URL


### Title

TODO


### Link

TODO


### Description

The description can be formatted using [Markdown][markdown].


### Image / Cover

* TODO: Image requirements?


### Payment URL

TODO


Media Files
-----------

* TODO: How to handle multiple formats?
* TODO: Which audio/video formats are recommended? Is there a
  comprehensive/authoritative list of open source codecs?

For iTunes support refer to the [audio and video formats recommended by
Apple](http://www.apple.com/itunes/podcasts/specs.html#formattingvideo).



Podcast Meta Data
-----------------

* TODO: Related feeds?
* TODO: Self-reference? Canonical URL?
* TODO: How to match uniquely identify an author among multiple feeds? Email?


### Author

Podcast feeds SHOULD include information about the author.

Specify [author][rfc4287author]. It is
recommended to include [name, URI and email
address](http://tools.ietf.org/html/rfc4287#section-3.2) of the author.

* TODO: Extensions are allowed. Any known?

Specify
[``<itunes:author>``](http://www.apple.com/itunes/podcasts/specs.html#authorId)
for iTunes support.

* TODO: RSS?



Episode
-------

A feed should contain a list of episodes ordered by their modification date,
starting with the one most recently modified.

Each episode describes one recording of a podcast's show.

* TODO: number of episodes? either suggest a number or a time frame (eg
  at least one week of episodes)
* TODO: alternative feeds with other selection of episodes
* TODO: only include episodes for which the media files are still available?


### Contents
* GUID
* Title
* Link
* Description
* Duration
* Publication Date
* Payment URL


### GUID

The GUID uniquely defines an episode. Two episode entries (possibly in two
different feeds) that describe the same episode (possibly in different
formats) MUST have the same GUID. Two episode entries that describe
different episodes MUST NOT have the same GUID.


### Title

TODO


### Link

TODO


### Description

* TODO: distinguish between subtitle, description, etc?


### Duration

TODO


### Publication Date

The publication date MUST conform to the [RFC 2822 Date and Time
Specification][rfc2822datetime].


### Payment URL

* TODO, see http://developers.flattr.net/feed/


Enclosure
---------

### Contents
* Link
* Media Type
* File Size
* Length


Related Feeds
-------------

* TODO: Reference all related feeds from every other feed, or reference one
  common resource that refers to all feeds; if so, which format?


Availability
------------

Each feed should have exactly one cannonical URL. A permanent redirect should
be used to indicate that the feed has moved to a different URL. Clients are
then instructed to updated the URL stored for the feed, and access the redirect
target directly in the future.

* TODO: how about [RSS Redirects](http://cyber.law.harvard.edu/rss/rssRedirect.html)?
* TODO: how about [`<itunes:new-feed-url>`](http://www.apple.com/itunes/podcasts/specs.html#newfeed) ?

* TODO: support ETag, other Cache-related HTTP headers



References
----------

[RFC2119]: http://www.ietf.org/rfc/rfc2119.txt "RFC 2119 Key words for use in RFCs to Indicate Requirement Levels"
[gpodder]: https://github.com/gpodder/ "gPodder projects"
[rfc2822datetime]: http://tools.ietf.org/html/rfc2822#section-3.3 "RFC 2822 Date and Time Specification"
[markdown]: http://daringfireball.net/projects/markdown/ "Markdown"
[rss20]: http://cyber.law.harvard.edu/rss/rss.html "RSS 2.0 at Harvard Law"
[rfc4287]: http://tools.ietf.org/html/rfc4287 "The Atom Syndication Format"
[rfc4287author]: (http://tools.ietf.org/html/rfc4287#section-4.2.1 (The "atom:author" Element)


Authors
-------

* Stefan Kögl <stefan@skoegl.net>

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


Overview
--------

### Terminology

A _podcast_ is a type of digital media consisting of an episodic series of
media files which are distributed through web syndication. A podcast is
described by one or more _podcast feeds_ (short _feeds_). A podcast contains
any number of _episodes_, each of which is represented by zero or more _media
files_.


### Structure

The remaineder of this document is divided into the following sections:

* **General Considerations** discusses general topics related to the
  distribution of podcasts
* **Podcasts** discusses pieces of information that describe a podcast
* **Feeds** discusses more technical details of the feeds describing a podcast
* **Episodes** discusses pieces of information that describe an episode
* **Media Files** discusses more technical details of the mediate files that
  contain the actual content of an episode


General Considerations
----------------------

TODO


Podcasts
--------

One feed describes one podcast and its episodes. There MAY be multiple feeds
describing different views of the same podcast (eg different media types,
different number and or selection of episodes, etc). See section
*Related Feeds*.


### Contents
* Title
* GUID
* Link
* Description
* Language
* Update Frequency
* Generator
* Payment URL
* Summary
* Author
* Image / Cover
* Copyright and License
* Categorization


### Title

The name of the podcast. A feed MUST contain a title.

Paths:
* Atom: `/atom10:feed/atom10:title`
* RSS: `/rss/channel/title`
* RSS (DC): `/rss/channel/dc:title`

**Open Questions**
* Should the title also contain a description of the feed (eg "MP3", "HQ",
  etc)? If not, where should such information go?


### GUID

A podcast feed SHOULD provide a globally unique Id (GUID).

TODOs
* RSS?
* Should the GUID represent the feed or the podcast?

Paths
* Atom `/atom10:feed/atom10:id`


### Link

The URL of the podcast's website. The resource that is available through the
specified URL should be accessible by a browser.

Paths:
* Atom: `/atom10:feed/atom10:link[@rel=”alternate”]/@href`
* Atom: `/atom10:feed/atom10:link[not(@rel)]/@href`
* RSS: `rss/channel/link`


### Description

A podcast MUST contain a textual description. The description MAY be formatted
using [Markdown][markdown].  It is RECOMMENDED to provide a short and long
version of the description. If there is only one description for the feed, the
short description SHOULD NOT be used.

Paths (Short Descriptions)
* Atom: `/atom10:feed/atom10:subtitle`
* RSS (iTunes): `/rss/channel/itunes:subtitle` (see [itunes:subtitle](http://www.apple.com/itunes/podcasts/specs.html#subtitle))

Paths (Long Description)
* RSS: `rss/channel/description`
* RSS (DC): `/rss/channel/dc:description`
* RSS (iTunes): (see [itunes:summary](http://www.apple.com/itunes/podcasts/specs.html#summary))


### Tags and Categorization

* TODO: http://pythonhosted.org/feedparser/reference-feed-tags.html



### Update Frequency

It is RECOMMENDED to providate information about the podcast's update
frequency using the [RDF Site Summary Syndication Module][synmod].

If a podcast is not longer updated with new episodes, it is RECOMMENDED to
indicate this by using the
[`<itunes:complete>`](http://www.apple.com/itunes/podcasts/specs.html#complete)
element from the iTunes extensions.


### Image / Cover

It is RECOMMENDED to provide an image or cover art for a podcast. The URL of
the image MUST be provided. All other information is OPTIONAL.

Paths
* Atom: `/atom10:feed/atom10:logo`
* RSS: `/rss/channel/image` (see [image](http://cyber.law.harvard.edu/rss/rss.html#ltimagegtSubelementOfLtchannelgt))
* RSS (iTunes): (see [itunes:image](http://www.apple.com/itunes/podcasts/specs.html#image))

**TODOs**
* Atom image?
* Atom: `/atom10:feed/atom10:icon`
* Image requirements?
* path of itunes:image


### License

It is RECOMMENDED to provide a link to the license under which a podcast is
published. If an RSS feed is available under a Creative Commons license, the
[creative commons namespace](http://www.rssboard.org/creative-commons) SHOULD
be used.

Paths
* Atom: `/atom10:feed/atom10:link[@rel=”license”]/@href`
* RSS (CC): `/rss/channel/creativeCommons:license`



### Language

A podcast feed SHOULD provide information about the primary language used in
the podcast. The language should be specified according to [RFC
3066](http://tools.ietf.org/html/rfc3066), [RFC
4647](http://tools.ietf.org/html/rfc4647) and [RFC
5646](http://tools.ietf.org/html/rfc5646).

Paths
* Atom: `feed/@xml:lang`
* RSS (DC): `/rss/channel/dc:language`
* RSS: `/rss/channel/language`


### Payment URL

It is RECOMMENDED to include a payment URL into a podcast feed, so that
listeners can support the creation of the podcast.

Services
* [Flattr](http://developers.flattr.net/feed/)

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:link[@rel="payment"]`



### Generator

A podcast feed SHOULD include information about the program by which it was
created. This MUST contain the name of the program, and SHOULD contain the
version and an URI associated with the program.

Atom allows to provide this information in a [structured
format](http://tools.ietf.org/html/rfc4287#section-4.2.4). In RSS one of the
following notations SHOULD be used.

* My Application
* My Application/2.5
* My Application (+http://example.com/)
* My Application/2.5 (+http://example.com/)

Paths
* Atom: `/atom10:feed/atom10:generator`
* RSS: `/rss/channel/generator`


### Authors and Contributors

Podcast feeds SHOULD include information about the authors and contributors.

Atom and Dubline Core allow to include structured information about author and
contributors.  It is RECOMMENDED to include name and URI and an email address.
When using the iTunes extension, it is RECOMMENDED to only specify the name of
the author.

Author Paths:
* Atom: `/atom10:feed/atom10:author` (see [author][rfc4287author] and [person][rfc4287person])
* RSS (DC): `/rss/channel/dc:creator` (see [dc][dc])
* RSS (iTunes): `/rss/channel/itunes:author` (see [author](http://www.apple.com/itunes/podcasts/specs.html#authorId)

Contributor Paths:
* Atom `/atom10:feed/atom10:contributor`
* RSS (DC): `/rss/channel/dc:contributor`

* TODO: should the author be included in the contributors?


Feeds
-----

### Meta Data

* TODO: Related feeds?
* TODO: Self-reference? Canonical URL?
* TODO: How to match uniquely identify an author among multiple feeds? Email?


### Format

A podcast MUST be published in either [RSS 2.0][rss20] or [Atom 1.0][rfc4287].

* TODO: Encoding? Always UTF-8? Defined in HTTP headers or in
  the content? iTunes [requires
  UTF-8](http://www.apple.com/itunes/podcasts/specs.html#encoding)


### Related Feeds

* TODO: Reference all related feeds from every other feed, or reference one
  common resource that refers to all feeds; if so, which format?


### Publication Date

A podcast feed SHOULD specify the date it was published. The publication date
MUST conform to the [RFC 2822 Date and Time Specification][rfc2822datetime].

Paths
* RSS: `/rss/channel/pubDate`


### Update Date

A podcast feed SHOULD specify the date if was last updated. The update
date MUST conform to the [RFC 2822 Date and Time
Specification][rfc2822datetime].

Paths
* Atom: `/atom10:feed/atom10:updated`
* RSS (DC): `/rss/channel/dc:date`

* TODO: if missing, use publication date / date of last episode / http header?


### Publisher

A podcast feed SHOULD specify its publisher.

Paths
* RSS (DC): `/rss/channel/dc:publisher`
* RSS (iTunes): `/rss/channel/itunes:owner`


### Availability

Each feed should have exactly one cannonical URL. A permanent redirect should
be used to indicate that the feed has moved to a different URL. Clients are
then instructed to updated the URL stored for the feed, and access the redirect
target directly in the future.

* TODO: how about [RSS Redirects](http://cyber.law.harvard.edu/rss/rssRedirect.html)?
* TODO: how about [`<itunes:new-feed-url>`](http://www.apple.com/itunes/podcasts/specs.html#newfeed) ?

* TODO: support ETag, other Cache-related HTTP headers


### PubSubHubbub

A podcast feed SHOULD be published through a [PubSubHubbub
hub](http://code.google.com/p/pubsubhubbub/).

Paths
* Atom: /atom10:feed/atom10:link[@rel=”alternate”]/@href
* RSS: /rss/channel/atom10:link[@rel=”alternate”]/@href (see [info](http://code.google.com/p/pubsubhubbub/wiki/RssFeeds))


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
* Comments


### Author

Episodes SHOULD include information about the authors and contributors.

Atom and Dubline Core allow to include structured information about author and
contributors.  It is RECOMMENDED to include name and URI and an email address.
When using the iTunes extension, it is RECOMMENDED to only specify the name of
the author.

Author Paths:
* Atom: `/atom10:feed/atom10:entry/atom10:author`
* RSS (DC): `/rss/channel/item/dc:author`
* RSS (iTunes): `/rss/channel/itunes:author`

Contributor Paths:
* Atom: `/atom10:feed/atom10:entry/atom10:contributor`
* RSS (DC): `/rss/channel/item/dc:contributor`
* RSS (iTunes): `/rss/channel/item/itunes:author` (see [author](http://www.apple.com/itunes/podcasts/specs.html#authorId)


* TODO: should the author be included in the contributors?


### Publisher

An episode SHOULD specify its publisher.

Paths
* RSS (DC): `/rss/item/dc:publisher`
* RSS (iTunes): `/rss/item/itunes:owner`


### Sources / Show Notes

Sources and Show notes

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:source`



### GUID

The GUID uniquely identifies an episode. Two episode entries (possibly in two
different feeds) that describe the same episode (possibly in different
formats) MUST have the same GUID. Two episode entries that describe
different episodes MUST NOT have the same GUID.

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:id`
* RSS: `/rss/channel/item/guid`


### Title

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:title`
* RSS (DC): `/rss/channel/item/dc:title`
* RSS: `/rss/channel/item/title`


### Link

The URL of the episode's website. The resource that is available through the
specified URL should be accessible by a browser.

Paths:
* Atom: /atom10:feed/atom10:entry/atom10:link[@rel=”alternate”]/@href
* Atom: /atom10:feed/atom10:entry/atom10:link[not(@rel)]/@href
* RSS: /rss/channel/item/link


### Description

An episode MUST contain a textual description. The description MAY be formatted
using [Markdown][markdown]. It is RECOMMENDED to provide a short and long
version of the description. If there is only one description for the feed, the
short description SHOULD NOT be used.

Paths (Short Description)
* Atom: `/atom10:feed/atom10:entry/atom10:summary`
* RSS: `/rss/channel/item/description`
* RSS: `/rss/channel/item/dc:description`

Paths (Long Description)
* Atom: `/atom10:feed/atom10:entry/atom10:content`
* RSS: `/rss/channel/item/body`
* RSS: `/rss/channel/item/content:encoded`
* RSS: `/rss/channel/item/fullitem`
* RSS: `/rss/channel/item/xhtml:body`

* TODO: check which RSS elements to use


### License

It is RECOMMENDED to provide a link to the license under which an episode is
published. If an episode in a RSS feed is available under a Creative Commons
license, the [creative commons
namespace](http://www.rssboard.org/creative-commons) SHOULD be used.

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:link[@rel=”license”]/@href`
* RSS (CC): `/rss/channel/item/creativeCommons:license`


### Update Date

An episode feed SHOULD specify the date if was last updated. The update
date MUST conform to the [RFC 2822 Date and Time
Specification][rfc2822datetime].

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:updated`
* RSS (DC): `/rss/channel/item/dcterms:modified`


### Duration

TODO


### Publication Date

The publication date MUST conform to the [RFC 2822 Date and Time
Specification][rfc2822datetime].

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:published`
* RSS: `/rss/channel/item/pubDate`
* RSS (DC): `/rss/channel/item/dcterms:issues` (see [issued](http://dublincore.org/documents/dcmi-terms/#terms-issued))


### Payment URL

It is RECOMMENDED to include a payment URL into a podcast feed, so that
listeners can support the creation of the podcast.

Services
* [Flattr](http://developers.flattr.net/feed/)

Paths
* Atom: `/atom10:feed/atom10:entry/atom10:link[@rel="payment"]`


### Comments

* TODO: http://bitworking.org/news/2012/08/wfw.html


### Tags and Categorization

Paths
* Atom: `/atom10:feed/atom10:entry/category`
* RSS: `/rss/channel/item/category`
* RSS (DC): `/rss/channel/item/dc:subject`
* RSS (iTunes): `/rss/channel/item/itunes:category`
* RSS (iTunes): `/rss/channel/item/itunes:keywords`


Media Files (Enclosures)
------------------------

### Contents
* Link
* Media Type
* File Size
* Length


**Open Questions**
* TODO: How to handle multiple formats?
* TODO: Which audio/video formats are recommended? Is there a
  comprehensive/authoritative list of open source codecs?

For iTunes support refer to the [audio and video formats recommended by
Apple](http://www.apple.com/itunes/podcasts/specs.html#formattingvideo).


Paths
* Atom: `/atom10:feed/atom10:entry/atom10:link[@rel="enclosure"]`
* RSS: `/rss/channel/item/enclosure`




References
----------

[RFC2119]: http://www.ietf.org/rfc/rfc2119.txt "RFC 2119 Key words for use in RFCs to Indicate Requirement Levels"
[gpodder]: https://github.com/gpodder/ "gPodder projects"
[rfc2822datetime]: http://tools.ietf.org/html/rfc2822#section-3.3 "RFC 2822 Date and Time Specification"
[markdown]: http://daringfireball.net/projects/markdown/ "Markdown"
[rss20]: http://cyber.law.harvard.edu/rss/rss.html "RSS 2.0 at Harvard Law"
[rfc4287]: http://tools.ietf.org/html/rfc4287 "The Atom Syndication Format"
[rfc4287author]: (http://tools.ietf.org/html/rfc4287#section-4.2.1 (The "atom:author" Element)
[frc4287person]: (http://tools.ietf.org/html/rfc4287#section-3.2 "Person Constructurs"
[itunes]: http://www.apple.com/itunes/podcasts/specs.html#subtitle "iTunes Extensions"
[synmod]: http://web.resource.org/rss/1.0/modules/syndication/ "RDF Site Summary 1.0 Modules: Syndication"
[dc]: http://tools.ietf.org/html/rfc5013 "The Dublin Core Metadata Element Set"


Authors
-------

* Stefan Kögl <stefan@skoegl.net>

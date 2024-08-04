---
title: Infrastructure CDN
permalink: /Infrastructure/CDN/
---

The **Unvanquished CDN** is a network of servers providing seeds for the
Unvanquished torrent. The relies on BitTorrent to download the game.

BitTorrent is a communication protocol for peer-to-peer file sharing
(P2P), which enables us to distribute updates over the Internet in a
decentralized manner.

# Torrent

Latest torrent url (zip content):

- (redirect to latest torrent file)

- (stable url without redirect)

Direct torrent url and mirrors:

# Trackers

Unvanquished relies on [FOSS Torrents](https://fosstorrents.com) as
primary BitTorrent tracker and a bunch of other trackers as a fallback.

-

Here is our page on FOSS Torrents website:
<https://fosstorrents.com/games/unvanquished/>

After , is it expected those maintained lists of trackers will be used
when creating new torrents:

- <https://raw.githubusercontent.com/ngosang/trackerslist/master/trackers_all.txt>
- <https://newtrackon.com/api/stable>

Those lists are meant to be updated and to only contain working
trackers.

# Seeds

It is possible to contribute to the CDN in two ways:

- by downloading the files and seed them with a BitTorrent software,
- by providing web seeds.

## BitTorrent seeds

Any user can contribute this way without having to get in touch with us.

One can simply download the bitTorrent file, add it to a BitTorrent
software and make sure the torrent gets configured to not get paused
once completed. A good idea is to enable the Super Seeding option for
the torrent if the software provides it.

See [Torrent RSS](#Torrent_RSS "wikilink") below for details for a way
to automatically fetch and seed the files when we distribute a new
release.

## Web seeds

Those are web servers used as BitTorrent seeds, they provides reliable
seeding, especially when no one downloaded the game over BitTorrent yet.
Bittorrent clients including the download game files from there in
addition to BitTorrent seeds.

Here are the current Unvanquished web seed servers, with location and
owner:

If you own a web server and want to add it to the list of web seeds,
tell us on
[forums](https://forums.unvanquished.net/viewtopic.php?p=18849#p18849),
as this will need some configuration from us to add your server to the
seeds.

# Torrent RSS

We provide an RSS feed for the latest torrent file:

-

This feed always provide the link for the latest torrent for the latest
game version. Some BitTorrent software has features to automatically
download and seed new torrents listed in such feed.

See [Tutorials/RSS BitTorrent
seeding](Tutorials_RSS_BitTorrent_seeding "wikilink") for instructions
to configure some BitTorrent software with RSS automatic download and
seeding.
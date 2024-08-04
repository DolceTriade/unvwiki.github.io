---
title: Tutorials RSS BitTorrent seeding
permalink: /Tutorials/RSS_BitTorrent_seeding/
---

Here are some tutorials for adding a Torrent RSS to some BitTorrent
software. This is a convenient way to set-up a BitTorrent software to
automatically download new versions of the game and seed them.

See [Infrastructure/CDN](Infrastructure_CDN "wikilink") for details
about the **Unvanquished CDN** and how BitTorrent is used by the .

# qBittorrent

qBittorrent has out of the box RSS torrent support.

So you fist need the [qBittorrent](https://www.qbittorrent.org/)
software.

In qBittorrent Preferences (*Tools* → *Preferences*), click “*RSS*” icon
and tick those two checkboxes:

- *Enable fetching RSS feeds*
- *Enable auto downloading of RSS torrents*

Then closes preferences window and in the main qBittorrent window, open
the “*RSS*” tab, click the “*New subscription*” button, and fill this
filed:

- *Feed URL*:

Then click the “*RSS Downloader…*” button of the “*RSS*” tab (or the
“*Edit auto downloading rules*” button in qBittorrent RSS preferences)

Click the “*+*” button next to “*Download Rules*” to add a rule.

Fill the fields this way:

- *New rule name*:

Tick this check box:

- *Apply Rule to Feeds*:

You can customize the folder where to download the Unvanquished files by
ticking this checkbox:

- *Save to a Different Directory*

And fill this field:

- *Save to*: as you want

If needed, you can force the download this way: on the “*RSS*” tab of
qBittorrent: right-click on the feed then “*Update*”, right-click on the
torrent name then “*Download torrent*”.

# Deluge

First, you'll need the [Deluge](https://deluge-torrent.org/) software
and the [YaRSS2](https://dev.deluge-torrent.org/wiki/Plugins/YaRSS2)
plugin.

In Deluge Preferences, enable the YaRSS2 plugin.

In YaRSS2 plugin, in “*Rss Feeds*” tab, click the “*Add Feed*” button
and fill those fields this way:

- *RSS Feed Name*:
- *RSS Feed URL*:

Then in “*Subscription*” tab, click the “*Add Subscription*” button and
fill those fields this way:

- *Subscription name*:
- *RSS Feed*: select the “*Unvanquished*” feed in the drop down list
- *Filter include (regex)*:

In “Options” tab you may also want to customize “*Download location*”
and “*Move completed*” fields.

The “Move completed” feature is handy if you download with bittorrent
the files for a web seed: once the download is completed the files will
be moved to a specific folder you can chose, making sure they are
complete once they are written to this folder.

If needed you can force the download this way: on the Subscription list
you can right click the “*Unvanquished*” subscription and click “*Reset
last matched timestamp*” then “*Run this subscriptions*”.

[Category:Tutorials](Category:Tutorials "wikilink")
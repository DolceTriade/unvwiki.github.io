---
title: Infrastructure Servers
permalink: /Infrastructure/Servers/
---

## Dedicated server hosted by \`Ishq

99% Unvanquished stuff, \`Ishq hosts one personal service.

Administration is shared among some team members.

### System

- System: Debian
- Web server: Nginx
- PHP application server: PHP-FPM
- Database: MariaDB/MySQL
- SSL certificates: Let's Encrypt

### Hosted web services

- <https://unvanquished.net> blog
  - Software: Wordpress
- <https://unvanquished.net/activity> Pluto rss/atom planet for
  development activity
  - Software: Pluto, <https://github.com/feedreader/pluto>
  - Configuration: <https://github.com/Unvanquished/pluto-devfeeds>
- <https://unvanquished.net/servers> Wordpress plugin for server listing
  - Software: XonPress, <https://github.com/DaemonEngine/XonPress>
    ([originally written](https://gitlab.com/mattia.basaglia/Xonpress)
    by Melanosuchus)
- <https://forums.unvanquished.net> forums
  - Software: phpBB
- <https://wiki.unvanquished.net> wiki
  - Software: MediaWiki
- <https://login.unvanquished.net> shared authentication system
  - Software: SimpleSAMLphp
- <http://dl.unvanquished.net> primary download server (releases, ingame
  download)
  - Software: raw Nginx
- <http://cdn.unvanquished.net> primary CDN server
  - Software: raw Nginx

### Hosted game services

- `master.unvanquished.net` primary master server (unvanquished-master)
- `unvanquished.net:27960` official US game server

### Hosted chat services

- Overmind IRC bot: autovoice webchat users, welcome messages, antispam
  features
  - Software: PyTIBot, <https://github.com/DefaultUser/PyTIBot>
- Unvanquished IRC bot: announce game and events
  - Software: Mantis, <https://gitlab.com/Viech/Mantis/>
- Granger: keeps note for users, do some fun stuff as well (markov
  chains)
  - Software: ruby-rbot, <https://github.com/ruby-rbot/rbot>
- Dretch (DiscordFlips): bridge IRC, Matrix and Discord
  - Software: matterbridge, <https://github.com/42wim/matterbridge>

See [Chat#Chat bots](Chat#Chat_bots "wikilink") for details about what
those chat bots do.

## Dedicated server hosted by illwieckz

99% personnal stuff, some Unvanquished services among others.

Has been used as a landing page when \`Ishq dedicated server was
offline.

Administration is not shared. It may be possible to share administration
powers on the game-related virtual machine or to redesign things to make
it possible.

### System

- System (hypervisor): Debian Xen
- Web front: Nginx
- SSL certificates: Let's Encrypt
- System (web virtual machine): Debian
- Web: Nginx
- System (gaming virtual machine): Ubuntu
- Web: Nginx

### Hosted web services

- <http://cdn.illwieckz.net/unvanquished> CDN mirror
- <https://dl.illwieckz.net/share/unvanquished/release> release mirror
- <http://gg.illwieckz.net/dl/unvanquished/pkg> in-game download

### Hosted game services

- `master2.unvanquished.net` secondary master server
  (unvanquished-master)
- `gg.illwieckz.net:27960` official EU game server

[Category:Infrastructure](Category:Infrastructure "wikilink")
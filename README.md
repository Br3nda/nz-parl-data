# nz-parl-data

Open, structured data about the New Zealand Parliament, published in standard formats rather
than locked inside a PDF or a one-off CSV schema.

New Zealand doesn't currently publish a feed like this itself - [data.govt.nz's Members of
Parliament dataset](https://catalogue.data.govt.nz/dataset/members-of-parliament) is CSV only.
This repo exists to make the same kind of data available in formats that other open-parliament
tools and researchers already know how to use.

## What's here

- **`parlparse/popolo.json`** - every MP and party membership, in [Popolo](#popolo) format.
  Covers every Parliament back to the 1st (1853). The underlying data is
  [data.govt.nz's own Members of Parliament dataset](https://catalogue.data.govt.nz/dataset/members-of-parliament)
  (Parliamentary Service / Department of Internal Affairs) - this file doesn't add any new facts
  to it, it's the same data converted into Popolo format via [Hot Air](https://hotair.nz)'s own
  database. Regenerated and republished periodically, not live-updated.

## Popolo

[Popolo](https://www.popoloproject.com/) is an open data standard for describing people,
organisations and the relationships between them - built specifically for political and
legislative data. A Popolo document has three main kinds of things:

- **persons** - people, e.g. an MP
- **organizations** - groups, e.g. a political party
- **memberships** - links a person to an organization over some period of time, e.g. "this MP
  held this electorate seat for this party between these two dates"

It's JSON-based and deliberately simple, which is why it's become a common interchange format
for parliamentary/political data projects internationally (it's the format
[EveryPolitician](http://everypolitician.org/) used to publish parliamentary membership data for
233 countries and territories, before the project was placed on hold in 2019).

## parlparse

[`parlparse`](https://github.com/mysociety/parlparse) is [mySociety](https://www.mysociety.org/)'s
own project for turning the UK Parliament's Hansard into structured data - it's the engine behind
[TheyWorkForYou](https://www.theyworkforyou.com/), the long-running UK site this project (and Hot
Air generally) takes inspiration from. It doesn't use Popolo itself (it predates Popolo and has
its own XML format), but it's the closest existing prior art for what this repo and Hot Air are
doing for New Zealand - scraping/parsing an official parliamentary record into open, structured
data that other tools can build on. The `parlparse/` directory name here is a nod to that project,
not a claim that its contents use parlparse's own format - they're Popolo, not parlparse XML.

## Licence and attribution

The underlying data is sourced from
[data.govt.nz's Members of Parliament dataset](https://catalogue.data.govt.nz/dataset/members-of-parliament)
(Parliamentary Service / Department of Internal Affairs, Crown copyright), published under
[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/).
This repo's own conversion of that data into Popolo format is released under the same licence.

# nz-parl-data

Open, structured data about the New Zealand Parliament, published in standard formats rather
than locked inside a PDF or a one-off CSV schema.

New Zealand doesn't currently publish a feed like this itself - [data.govt.nz's Members of
Parliament dataset](https://catalogue.data.govt.nz/dataset/members-of-parliament) is CSV only.
This repo exists to make the same kind of data available in formats that other open-parliament
tools and researchers already know how to use.

## What's here

- **`popolo/members.json`** - every MP and party membership, in [Popolo](#popolo) format.
  Covers every Parliament back to the 1st (1853). The underlying data is
  [data.govt.nz's own Members of Parliament dataset](https://catalogue.data.govt.nz/dataset/members-of-parliament)
  (Parliamentary Service / Department of Internal Affairs) - this file doesn't add any new facts
  to it, it's the same data converted into Popolo format via [Hot Air](https://hotair.nz)'s own
  database. Regenerated and republished periodically, not live-updated.
- **`popolo/vote_events.json`** - every counted parliamentary division (vote), in Popolo
  [Vote Event](#vote-events) format. The underlying data is Hansard, the official transcript of
  Parliament, parsed by Hot Air - again, not new facts, just the same votes converted into a
  standard format. Regenerated and republished periodically, not live-updated.

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

## Vote Events

[Popolo's Vote Event](https://www.popoloproject.com/specs/vote-event.html) format covers a single
counted division: the motion text, when it happened, the result, a tally of how many voted each
way, and (where known) how each individual MP voted. `popolo/vote_events.json` has one entry per
vote with:

- **`motion_text`** / **`start_date`** / **`legislative_session_id`** - what was being decided,
  when, and in which Parliament
- **`result`** - `"pass"` or `"fail"`
- **`counts`** - how many votes each option (`yes`/`no`/`abstain`) got
- **`votes`** - each MP's `voter_id` (matching the `id` used for that MP in
  `popolo/members.json`) and which way they voted

Only counted divisions are included - many votes in Hansard are decided "on the voices" with no
tally at all, and those aren't vote events here. Older party votes, from before Hansard recorded
how every individual MP voted, only have a party-level tally: for those, `counts` has one entry
per party (`group_id` matching that party's `id` in `popolo/members.json`) and `votes` is empty,
since there's no individual-level data to report.

## parlparse

[`parlparse`](https://github.com/mysociety/parlparse) is [mySociety](https://www.mysociety.org/)'s
own project for turning the UK Parliament's Hansard into structured data - it's the engine behind
[TheyWorkForYou](https://www.theyworkforyou.com/), the long-running UK site this project (and Hot
Air generally) takes inspiration from. It doesn't use Popolo itself (it predates Popolo and has
its own XML format), but it's the closest existing prior art for what this repo and Hot Air are
doing for New Zealand - scraping/parsing an official parliamentary record into open, structured
data that other tools can build on.

## Licence and attribution

`popolo/members.json` is derived from data under Crown copyright: sourced from
[data.govt.nz's Members of Parliament dataset](https://catalogue.data.govt.nz/dataset/members-of-parliament)
(Parliamentary Service / Department of Internal Affairs), published under
[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/).

`popolo/vote_events.json` is derived from Hansard, the official transcript of the New Zealand
Parliament. Under [section 27(1) of the Copyright Act 1994](https://www.legislation.govt.nz/act/public/1994/0143/latest/DLM346602.html),
no copyright exists in NZ Parliamentary debates, so this file isn't under any licence - it's
public domain.

This repo's own conversion work (the format, the code that produces it) is considered CC0 -
public domain, no rights reserved - except where that would conflict with the underlying Crown
copyright/CC BY terms on the members data, which still applies to the facts being conveyed.

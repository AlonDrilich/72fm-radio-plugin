---
name: find-radio-station
description: Find live internet radio stations and give the user a working stream URL. Use when the user asks for a radio station, a genre or country of radio, what is popular on radio in a place, or the stream or playlist address of a named station.
---

# Find a live internet radio station

Use the `internet-radio` tools. They search the Radio Browser directory, a public-domain, community-run list of live internet radio stations.

## Choosing a tool

- **A named station** ("BBC World Service", "KEXP"): `search_stations` with `name`. If several stations share the name, show the country and bitrate so the user can choose.
- **A genre, mood or language** ("jazz in Brazil", "lofi", "Hebrew news"): `search_stations` with `tag`, `countrycode` (ISO 3166-1 alpha-2, such as `BR`) and/or `language`. Ask for `order: votes` to get the stations listeners rate highest.
- **What is popular**: `top_stations` with `by` set to `votes`, `clicks` or `trending`, optionally narrowed by `countrycode` or `tag`.
- **What can be searched**: `list_countries` (stations per country) and `list_genres` (the most-used genre tags). Use these to pick valid `countrycode` and `tag` values before searching.
- **More about one station**: `get_station` with the station's `id`.

## What to give the user

For each station give its name, country, genre tags, bitrate and codec, and:

- `stream_url`: the direct audio address. It plays in VLC, mpv, Kodi, foobar2000, a Wi-Fi radio that accepts custom stations, or an audio element in a web page.
- `listen_url`: a page where the station plays in a browser, with no install.

Offer to make a short M3U playlist when the user wants several stations: one `#EXTINF:-1,<name>` line followed by the `stream_url` for each.

## Be accurate

- Stations belong to their broadcasters. Do not describe them as curated or endorsed, and do not claim a quality, such as "HD" or "ad-free", that the result does not state. Any adverts on air are the broadcaster's.
- A stream can be offline even if the directory lists it. If a stream fails, say so and offer the next result.
- Results come from a live search, so quote counts and rankings as of now, not as fixed facts.

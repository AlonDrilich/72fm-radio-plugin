# 72FM Radio: a Claude plugin for internet radio

This plugin lets Claude find live internet radio stations and hand you a working stream URL. Ask for "jazz stations in Brazil", "the most popular radio in Japan" or "the stream address of BBC World Service", and Claude searches the Radio Browser directory for you. It adds one skill, `find-radio-station`, and one local MCP server, `internet-radio`, with five read-only tools: `search_stations`, `get_station`, `top_stations`, `list_countries` and `list_genres`.

## What it connects to

The server makes outbound HTTPS GET requests, and only to the public Radio Browser API at `de1.api.radio-browser.info`, `de2.api.radio-browser.info` and `all.api.radio-browser.info` (it tries them in that order). The requests carry your search words and the User-Agent `internet-radio-mcp/1.0 (+https://72fm.com)`. Nothing else is sent: no files, no account details, no credentials, and the plugin needs none. It does not run shell commands, write files or read anything outside its own folder. Each result includes a `listen_url` on 72fm.com; that is only a link, and nothing contacts 72fm.com unless you open it.

Radio Browser is a community-run, public-domain directory of radio stations. Stations belong to their broadcasters; neither this plugin nor 72FM owns, hosts or curates them, and a listed stream can occasionally be offline.

## Install

Add the plugin from the Claude directory once it is listed. Until then, the same server runs on its own in Claude Code, Claude Desktop, Cursor or VS Code: see [internet-radio-mcp](https://github.com/AlonDrilich/internet-radio-mcp), for example `claude mcp add internet-radio -- npx -y github:AlonDrilich/internet-radio-mcp`.

The plugin's server needs Node.js 20 or newer. It runs from one self-contained file, `dist/server.mjs`, so nothing is installed when the plugin is installed. That file is built from `server/` and the committed `package-lock.json` with `npm ci && npm run build` (esbuild, no minification), and it is committed so that what runs is what you can read in this repository.

## Source and license

The server source is in `server/`, readable and unminified; `dist/server.mjs` is the unminified bundle of that source and its two runtime packages (`@modelcontextprotocol/server` and `zod`). It is the same code as [AlonDrilich/internet-radio-mcp](https://github.com/AlonDrilich/internet-radio-mcp), which also runs standalone with `npx`. MIT licensed. Made by [72FM](https://72fm.com/developers), a free web radio player built on the same directory.

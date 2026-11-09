# How to connect Meetup to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Meetup account.** The official Meetup app in ChatGPT helps people discover events by interest, location and date. Cotlet.dev connects your own signed-in Meetup account to any AI agent, so you can ask in plain words and the AI creates and copies events for you.

## What you can ask

> Create a "Founders Coffee" event in my Austin Startups group for Thursday, March 12 at 8 am at Epoch Coffee, limit 25 RSVPs.

> Copy last week's "Python Night" event to every Tuesday in April at 6:30 pm, same venue and description.

> Duplicate our Saturday hike event, change the trail to Barton Creek and set the start to 9 am.

> Create a free online workshop called "Intro to Email Marketing" on May 7 at 1 pm with a Zoom link and 3 hosts: me, Priya and Tom.

> Copy the "Spring Networking Mixer" event into my Dallas group and move it to Friday, June 5 at 7 pm.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Meetup tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"meetup":{"command":"uvx","args":["meetup-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t meetup-mcp .
docker run -i --rm -e COTLET_API_KEY meetup-mcp
```

Tools: `meetup_guide`, `meetup_status`, `meetup_open`, `meetup_read`, `meetup_click`, `meetup_type`, `meetup_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install meetup-mcp        # or run it once: uvx meetup-mcp connect
meetup-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 meetup_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 meetup_agent.py status    # is Meetup ready in your Cotlet.dev account
python3 meetup_agent.py guide     # Meetup screens and sign-in link
python3 meetup_agent.py read      # open Meetup, read the page, close the browser
python3 meetup_agent.py tools     # list Cotlet.dev tools
python3 meetup_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Meetup users

**Does Meetup have an API?**

Meetup has a GraphQL API, but only members with an active Meetup Pro subscription can get access, and it stops working when Pro lapses (checked 11 Oct 2026). Even with Pro it cannot message members, copy events or manage attendees. Cotlet.dev works in your own signed-in Meetup account, so your AI agent can create and copy events with no API key and no code.

**How do I connect Meetup to ChatGPT?**

The official Meetup app in ChatGPT is for discovering events. To create and copy events in your own account, add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Meetup once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Meetup API key.

**Is there a way to use Claude with Meetup?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Meetup account.

**Is there a Meetup MCP server?**

Yes. Cotlet.dev is a hosted MCP server that works in Meetup for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Meetup on Cotlet.dev](https://cotlet.dev/integrations/meetup-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=meetup&utm_content=find)
- [PyPI package meetup-mcp](https://pypi.org/project/meetup-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-meetup-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/meetup-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=meetup

Start free: https://cotlet.dev/signup?app=meetup&utm_source=github&utm_medium=readme&utm_campaign=meetup

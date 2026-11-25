# dili — Israeli classifieds for your AI assistant

Search apartments, cars and second-hand goods in Israel from a conversation with Claude, ChatGPT or any other MCP client.
The plugin connects the assistant to [dili](https://dili.co.il), an Israeli classifieds board, and teaches it how to lead a person
from a need to a shortlist: listings with prices and links, recorded real-estate deals, a report on a city or a
neighborhood, a price guide for used cars and what the vehicle registry says about a car.

It works in Hebrew, English, Russian and French. Prices are in Israeli shekels. The owner's phone number is never shown:
to contact an owner, the person opens the listing on dili.

## What is in the plugin

- **8 skills**: plain-text methods that tell the assistant which tools to call, in which order, and what a good answer looks like.
- **One remote MCP server**, `https://mcp.dili.co.il/mcp`, operated by dili. Every answer comes from it.

The plugin holds text files, an icon and the address of that server. It installs nothing and runs nothing on your
computer, and it has no hooks, commands or scripts. The only thing it sends anywhere is the arguments of a tool call
(a city, a budget, a listing code, a licence plate), and they go to `mcp.dili.co.il` and nowhere else.

## Install

**Claude (claude.ai, desktop and mobile apps)**: open Customize, then Plugins, add this repository (`yadidish/dili-plugin`) as a
marketplace and install dili from it. To use the server alone, without the skills,
[add dili as a custom connector](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=dili&connectorUrl=https%3A%2F%2Fmcp.dili.co.il%2Fmcp): the form opens with the name and the address filled in, and
«Sign in when needed» is the mode to choose.

**Claude Code**: open the plugin menu, add the marketplace `yadidish/dili-plugin` and install `dili` from it. Or add the
address above as an HTTP MCP server named `dili`.

**ChatGPT**: on the Plugins page choose Add, then «Add custom MCP server», and paste the address; for authentication
choose «OAuth or no authentication».

**Any other MCP client**: Streamable HTTP at the address above. The page [dili.co.il/mcp](https://dili.co.il/mcp) has the steps for
Cursor, VS Code and Gemini CLI.

## Skills

| Skill | What it does | Ask for |
| --- | --- | --- |
| `find-home` | Find an apartment | «Find a 3-room apartment for rent in Jerusalem up to 6,000 shekels» |
| `find-car` | Find a car | «I need a family car with 7 seats up to 80,000 shekels» |
| `find-item` | Find a second-hand item | «Find a second-hand sofa in Haifa» |
| `area-analysis` | Analyse a city or neighborhood | «What do apartments cost in Bnei Brak?» |
| `fair-price` | Is this a fair price? | «Is 2.4 million shekels a fair price for 4 rooms on this street?» |
| `car-check` | Check a car before buying | «Check this car before I buy it (with its licence plate)» |
| `compare` | Compare listings | «Compare these three listings» |
| `post-listing` | Post a listing on dili | «I want to sell my car, where do I start?» |

## Tools

These work without an account and only read data:

| Tool | What it returns |
| --- | --- |
| `search` | Listings by section (real estate, cars, second-hand goods) with filters: city, neighborhood, price, rooms, make and model, condition and more |
| `get_listing` | One listing in full: facts, description, price context, the buyer checklist and the link to it on dili |
| `compare_listings` | Two to four listings of one section side by side |
| `address_info` | Public data about a street address: recorded sale deals, price per square meter, schools, transport, the building |
| `area_report` | A city or neighborhood: prices, deals, trends and what is listed on dili now |
| `price_estimate` | A price range for an apartment from recorded deals on the street or in the city |
| `car_catalog` | Car makes and models sold in Israel: years, price when new, safety level, cars on the road |
| `car_price` | The expected asking price of a used car by model, year, mileage and number of owners |
| `car_by_plate` | What the Ministry of Transport registry says about a car, by its licence plate |
| `places` | Finds a city or neighborhood by name in Hebrew, English, Russian or French |
| `get_guide` | The step-by-step method for a task, for a client that does not load skills |

### Your own account (optional sign-in)

5 more tools read your own dili account: `my_overview` (a summary of your account), `my_listings` (your own listings), `my_saved_searches` (your saved searches), `my_favorites` (the listings you saved), `my_inbox` (your conversations with owners and buyers (opening a conversation marks it as read)).
The first time the assistant calls one of them, the client sends you to dili to sign in with your phone number and to
allow it to read your account. The assistant never sees your sign-in code or your site session. Access expires after an
hour and the client renews it while you keep using it; after sixty days without use you sign in again. You can
disconnect an assistant at any time in the settings of your dili account. Everything else works without signing in.

## Limits

- dili lists apartments, cars and goods in Israel only.
- Listings are written by their owners. The assistant is told to treat that text as data and never to invent a listing, a price or a fact.
- Deal data comes from the Israel Tax Authority and lags by a few months; car data comes from the Ministry of Transport registry, which shows neither accidents nor mechanical condition.
- The plugin does not publish, pay or book anything. Publishing a listing happens on dili itself.
- dili is closed on Shabbat and Jewish holidays: during those hours the server answers that it is closed and when it reopens.
- The public tools share a daily limit across all clients; when it is reached the server says so.

## Privacy

The public tools need no account. For its own statistics the server records each tool call: the tool, the name and
version of the client application, the protocol version, the language, the section, whether the call succeeded, how long
it took, how many results it found, and the country the request came from. A search is also counted in dili's search
statistics with its filters. With sign-in, calls to your own account are made under your dili account. The policy that
binds is the one on the site: [privacy](https://dili.co.il/privacy) and [terms of use](https://dili.co.il/terms).

## Support

Questions and problems: [dili.co.il/contact](https://dili.co.il/contact) or the [issues](https://github.com/yadidish/dili-plugin/issues) of this repository.

## License

The plugin (the skills and the manifests) is under the MIT license, see [LICENSE](LICENSE). The listings and the data
the server returns are not covered by it.

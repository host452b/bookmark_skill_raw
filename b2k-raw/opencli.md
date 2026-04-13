**Turn websites, browser sessions, Electron apps, and local tools into deterministic interfaces for humans and AI agents.**
Reuse your logged-in browser, automate live workflows, and crystallize repeated actions into reusable CLI commands.

[](/jackwener/OpenCLI/blob/main/README.zh-CN.md)
[](https://www.npmjs.com/package/@jackwener/opencli)
[](https://nodejs.org)
[](/jackwener/OpenCLI/blob/main/LICENSE)

OpenCLI gives you one surface for three different kinds of automation:

- **Use built-in adapters** for sites like Bilibili, Zhihu, Xiaohongshu, Reddit, HackerNews, Twitter/X, and [many more](#built-in-commands).

- **Drive a live browser directly** with `opencli browser` when an AI agent needs to click, type, extract, or inspect a page in real time.

- **Generate new adapters** from real browser behavior with `explore`, `synthesize`, `generate`, and `cascade`.

It also works as a **CLI hub** for local tools such as `gh`, `docker`, and other binaries you register yourself, plus **desktop app adapters** for Electron apps like Cursor, Codex, Antigravity, ChatGPT, and Notion.

- **CLI All Electron** — CLI-ify apps like Antigravity Ultra! Now AI can control itself natively.

- **Browser Automation** — `browser` gives AI agents direct browser control: click, type, extract, screenshot — any interaction, fully scriptable.

- **Website → CLI** — Turn any website into a deterministic CLI: 87+ pre-built adapters, or crystallize your own with `opencli record`.

- **Account-safe** — Reuses Chrome/Chromium logged-in state; your credentials never leave the browser.

- **Anti-detection built-in** — Patches `navigator.webdriver`, stubs `window.chrome`, fakes plugin lists, cleans ChromeDriver/Playwright globals, and strips CDP frames from Error stack traces. Extensive anti-fingerprinting and risk-control evasion measures baked in at every layer.

- **AI Agent ready** — `explore` discovers APIs, `synthesize` generates adapters, `cascade` finds auth strategies, `browser` controls the browser directly.

- **External CLI Hub** — Discover, auto-install, and passthrough commands to any external CLI (gh, obsidian, docker, etc). Zero setup.

- **Self-healing setup** — `opencli doctor` diagnoses and auto-starts the daemon, extension, and live browser connectivity.

- **Dynamic Loader** — Simply drop `.js` adapters into the `clis/` folder for auto-registration.

- **Zero LLM cost** — No tokens consumed at runtime. Run 10,000 times and pay nothing.

- **Deterministic** — Same command, same output schema, every time. Pipeable, scriptable, CI-friendly.

- **Broad coverage** — 87+ sites across global and Chinese platforms (Bilibili, Zhihu, Xiaohongshu, Reddit, HackerNews, and more), plus desktop Electron apps via CDP.

npm install -g @jackwener/opencli
### 2. Install the Browser Bridge Extension
[

](#2-install-the-browser-bridge-extension)

OpenCLI connects to Chrome/Chromium through a lightweight Browser Bridge extension plus a small local daemon. The daemon auto-starts when needed.

- Download the latest `opencli-extension.zip` from the GitHub [Releases page](https://github.com/jackwener/opencli/releases).

- Unzip it, open `chrome://extensions`, and enable **Developer mode**.

- Click **Load unpacked** and select the unzipped folder.

### 4. Run your first commands
[

](#4-run-your-first-commands)

opencli list
opencli hackernews top --limit 5
opencli bilibili hot --limit 5

Use OpenCLI directly when you want a reliable command instead of a live browser session:

- `opencli list` shows every registered command.

- `opencli &lt;site&gt; &lt;command&gt;` runs a built-in or generated adapter.

- `opencli register mycli` exposes a local CLI through the same discovery surface.

- `opencli doctor` helps diagnose browser connectivity.

Use two different entry points depending on the task:

Install the packaged skills with:

npx skills add jackwener/opencli

Or install only what you need:

npx skills add jackwener/opencli --skill opencli-usage
npx skills add jackwener/opencli --skill opencli-browser
npx skills add jackwener/opencli --skill opencli-explorer
npx skills add jackwener/opencli --skill opencli-oneshot

In practice:

- start with `opencli-explorer` when the agent needs a reusable command for a site (it covers both automated and manual flows)

- use `opencli-browser` when the agent needs to inspect or steer the page directly

Available browser commands include `open`, `state`, `click`, `type`, `select`, `keys`, `wait`, `get`, `screenshot`, `scroll`, `back`, `eval`, `network`, `init`, `verify`, and `close`.

Use `opencli browser` when the task is inherently interactive and the agent needs to operate the page directly.
### Built-in adapters: stable commands
[

](#built-in-adapters-stable-commands)

Use site-specific commands such as `opencli hackernews top` or `opencli reddit hot` when the capability already exists and you want deterministic output.
### `explore` / `synthesize` / `generate`: create new CLIs
[

](#explore--synthesize--generate-create-new-clis)

Use these commands when the site you need is not covered yet:

- `explore` inspects the page, network activity, and capability surface.

- `synthesize` turns exploration artifacts into evaluate-based JS adapters.

- `generate` runs the verified generation path and returns either a usable command or a structured explanation of why completion was blocked or needs human review.

### `cascade`: auth strategy discovery
[

](#cascade-auth-strategy-discovery)

Use `cascade` to probe fallback auth paths such as public endpoints, cookies, and custom headers before you commit to an adapter design.
### CLI Hub and desktop adapters
[

](#cli-hub-and-desktop-adapters)

OpenCLI is not only for websites. It can also:

- expose local binaries like `gh`, `docker`, `obsidian`, or custom tools through `opencli &lt;tool&gt; ...`

- control Electron desktop apps through dedicated adapters and CDP-backed integrations

- **Node.js**: &gt;= 21.0.0 (or **Bun** &gt;= 1.0)

- **Chrome or Chromium** running and logged into the target site for browser-backed commands

**Important**: Browser-backed commands reuse your Chrome/Chromium login session. If you get empty data or permission-like failures, first confirm the site is already open and authenticated in Chrome/Chromium.

Variable
Default
Description

`OPENCLI_DAEMON_PORT`
`19825`
HTTP port for the daemon-extension bridge

`OPENCLI_WINDOW_FOCUSED`
`false`
Set to `1` to open automation windows in the foreground (useful for debugging)

`OPENCLI_BROWSER_CONNECT_TIMEOUT`
`30`
Seconds to wait for browser connection

`OPENCLI_BROWSER_COMMAND_TIMEOUT`
`60`
Seconds to wait for a single browser command

`OPENCLI_BROWSER_EXPLORE_TIMEOUT`
`120`
Seconds to wait for explore/record operations

`OPENCLI_CDP_ENDPOINT`
—
Chrome DevTools Protocol endpoint for remote browser or Electron apps

`OPENCLI_CDP_TARGET`
—
Filter CDP targets by URL substring (e.g. `detail.1688.com`)

`OPENCLI_VERBOSE`
`false`
Enable verbose logging (`-v` flag also works)

`OPENCLI_DIAGNOSTIC`
`false`
Set to `1` to capture structured diagnostic context on failures

`OUTPUT`
—
Override output format: `json`, `yaml`, or `table`

`DEBUG`
—
Set to `opencli` for internal debug logging

`DEBUG_SNAPSHOT`
—
Set to `1` for DOM snapshot debug output

npm install -g @jackwener/opencli@latest

# If you use the packaged OpenCLI skills, refresh them too
npx skills add jackwener/opencli

Or refresh only the skills you actually use:

npx skills add jackwener/opencli --skill opencli-usage
npx skills add jackwener/opencli --skill opencli-browser
npx skills add jackwener/opencli --skill opencli-explorer
npx skills add jackwener/opencli --skill opencli-oneshot

Install from source:

git clone git@github.com:jackwener/opencli.git
cd opencli
npm install
npm run build
npm link

To load the source Browser Bridge extension:

- Open `chrome://extensions` and enable **Developer mode**.

- Click **Load unpacked** and select this repository's `extension/` directory.

Site
Commands

**xiaohongshu**
`search` `note` `comments` `feed` `user` `download` `publish` `notifications` `creator-notes` `creator-notes-summary` `creator-note-detail` `creator-profile` `creator-stats`

**bilibili**
`hot` `search` `history` `feed` `ranking` `download` `comments` `dynamic` `favorite` `following` `me` `subtitle` `user-videos`

**tieba**
`hot` `posts` `search` `read`

**hupu**
`hot` `search` `detail` `mentions` `reply` `like` `unlike`

**twitter**
`trending` `search` `timeline` `lists` `bookmarks` `post` `download` `profile` `article` `like` `likes` `notifications` `reply` `reply-dm` `thread` `follow` `unfollow` `followers` `following` `block` `unblock` `bookmark` `unbookmark` `delete` `hide-reply` `accept`

**reddit**
`hot` `frontpage` `popular` `search` `subreddit` `read` `user` `user-posts` `user-comments` `upvote` `upvoted` `save` `saved` `comment` `subscribe`

**zhihu**
`hot` `search` `question` `download` `follow` `like` `favorite` `comment` `answer`

**amazon**
`bestsellers` `search` `product` `offer` `discussion` `movers-shakers` `new-releases`

**1688**
`search` `item` `assets` `download` `store`

**gitee**
`trending` `search` `user`

**gemini**
`new` `ask` `image` `deep-research` `deep-research-result`

**yuanbao**
`new` `ask`

**notebooklm**
`status` `list` `open` `current` `get` `history` `summary` `note-list` `notes-get` `source-list` `source-get` `source-fulltext` `source-guide`

**spotify**
`auth` `status` `play` `pause` `next` `prev` `volume` `search` `queue` `shuffle` `repeat`

**xianyu**
`search` `item` `chat`

**xiaoe**
`courses` `detail` `catalog` `play-url` `content`

**quark**
`ls` `mkdir` `mv` `rename` `rm` `save` `share-tree`

87+ adapters in total — **[→ see all supported sites &amp; commands](/jackwener/OpenCLI/blob/main/docs/adapters/index.md)**

OpenCLI acts as a universal hub for your existing command-line tools — unified discovery, pure passthrough execution, and auto-install (if a tool isn't installed, OpenCLI runs `brew install &lt;tool&gt;` automatically before re-running the command).

External CLI
Description
Example

**gh**
GitHub CLI
`opencli gh pr list --limit 5`

**obsidian**
Obsidian vault management
`opencli obsidian search query="AI"`

**docker**
Docker
`opencli docker ps`

**lark-cli**
Lark/Feishu — messages, docs, calendar, tasks, 200+ commands
`opencli lark-cli calendar +agenda`

**dingtalk**
DingTalk — cross-platform CLI for DingTalk's full suite, designed for humans and AI agents
`opencli dingtalk msg send --to user "hello"`

**wecom**
WeCom/企业微信 — CLI for WeCom open platform, for humans and AI agents
`opencli wecom msg send --to user "hello"`

**vercel**
Vercel — deploy projects, manage domains, env vars, logs
`opencli vercel deploy --prod`

**Register your own** — add any local CLI so AI agents can discover it via `opencli list`:

Control Electron desktop apps directly from the terminal. Each adapter has its own detailed documentation:

App
Description
Doc

**Cursor**
Control Cursor IDE — Composer, chat, code extraction
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/cursor.md)

**Codex**
Drive OpenAI Codex CLI agent headlessly
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/codex.md)

**Antigravity**
Control Antigravity Ultra from terminal
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/antigravity.md)

**ChatGPT App**
Automate ChatGPT macOS desktop app
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/chatgpt-app.md)

**ChatWise**
Multi-LLM client (GPT-4, Claude, Gemini)
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/chatwise.md)

**Notion**
Search, read, write Notion pages
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/notion.md)

**Discord**
Discord Desktop — messages, channels, servers
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/discord.md)

**Doubao**
Control Doubao AI desktop app via CDP
[Doc](/jackwener/OpenCLI/blob/main/docs/adapters/desktop/doubao-app.md)

To add a new Electron app, start with [docs/guide/electron-app-cli.md](/jackwener/OpenCLI/blob/main/docs/guide/electron-app-cli.md).

OpenCLI supports downloading images, videos, and articles from supported platforms.

Platform
Content Types
Notes

**xiaohongshu**
Images, Videos
Downloads all media from a note

**bilibili**
Videos
Requires `yt-dlp` installed

**twitter**
Images, Videos
From user media tab or single tweet

**douban**
Images
Poster / still image lists

**pixiv**
Images
Original-quality illustrations, multi-page

**1688**
Images, Videos
Downloads page-visible product media from item pages

**zhihu**
Articles (Markdown)
Exports with optional image download

**weixin**
Articles (Markdown)
WeChat Official Account articles

For video downloads, install `yt-dlp` first: `brew install yt-dlp`

opencli xiaohongshu download abc123 --output ./xhs
opencli bilibili download BV1xxx --output ./bilibili
opencli twitter download elonmusk --limit 20 --output ./twitter
opencli 1688 download 841141931191 --output ./1688-downloads

All built-in commands support `--format` / `-f` with `table` (default), `json`, `yaml`, `md`, and `csv`.

opencli bilibili hot -f json    # Pipe to jq or LLMs
opencli bilibili hot -f csv     # Spreadsheet-friendly
opencli bilibili hot -v         # Verbose: show pipeline debug steps

opencli follows Unix `sysexits.h` conventions so it integrates naturally with shell pipelines and CI scripts:

Code
Meaning
When

`0`
Success
Command completed normally

`1`
Generic error
Unexpected / unclassified failure

`2`
Usage error
Bad arguments or unknown command

`66`
Empty result
No data returned (`EX_NOINPUT`)

`69`
Service unavailable
Browser Bridge not connected (`EX_UNAVAILABLE`)

`75`
Temporary failure
Command timed out — retry (`EX_TEMPFAIL`)

`77`
Auth required
Not logged in to target site (`EX_NOPERM`)

`78`
Config error
Missing credentials or bad config (`EX_CONFIG`)

`130`
Interrupted
Ctrl-C / SIGINT

opencli spotify status || echo "exit $?"   # 69 if browser not running
opencli github issues 2&gt;/dev/null
[ $? -eq 77 ] &amp;&amp; opencli github auth       # auto-auth if not logged in

Extend OpenCLI with community-contributed adapters:

opencli plugin install github:user/opencli-plugin-my-tool
opencli plugin list
opencli plugin update --all
opencli plugin uninstall my-tool

See [Plugins Guide](/jackwener/OpenCLI/blob/main/docs/guide/plugins.md) for creating your own plugin.
## For AI Agents (Developer Guide)
[

](#for-ai-agents-developer-guide)

**Quick mode**: To generate a single command for a specific page URL, see [opencli-oneshot skill](/jackwener/OpenCLI/blob/main/skills/opencli-oneshot/SKILL.md) — just a URL + one-line goal, 4 steps done.

**Full mode**: Before writing any adapter code, read [opencli-explorer skill](/jackwener/OpenCLI/blob/main/skills/opencli-explorer/SKILL.md). It contains the complete browser exploration workflow, the 5-tier authentication strategy decision tree, and debugging guide.

opencli explore https://example.com --site mysite   # Discover APIs + capabilities
opencli synthesize mysite                            # Generate JS adapters
opencli generate https://example.com --goal "hot"   # One-shot: explore → synthesize → register
opencli cascade https://api.example.com/data         # Auto-probe: PUBLIC → COOKIE → HEADER

See **[TESTING.md](/jackwener/OpenCLI/blob/main/TESTING.md)** for how to run and write tests.

- **"Extension not connected"** — Ensure the Browser Bridge extension is installed and **enabled** in `chrome://extensions` in Chrome or Chromium.

- **"attach failed: Cannot access a chrome-extension:// URL"** — Another extension may be interfering. Try disabling other extensions temporarily.

- **Empty data or 'Unauthorized' error** — Your Chrome/Chromium login session may have expired. Navigate to the target site and log in again.

- **Node API errors** — Ensure Node.js &gt;= 21. Some features require `node:util` styleText (stable in Node 21+).

- **Daemon issues** — Check status: `curl localhost:19825/status` · View logs: `curl localhost:19825/logs`

[](https://star-history.com/#jackwener/opencli&amp;Date)

[Apache-2.0](/jackwener/OpenCLI/blob/main/LICENSE)
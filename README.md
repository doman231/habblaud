<p align="center">
  <img src="client/public/assets/brand/logo-mark@4x.png" width="96" alt="Logo do Habblaud: um pequeno prédio em pixel art" />
</p>

<h1 align="center">Habblaud</h1>

<p align="center">
  <b>The virtual office for your Claude Code agents (and Codex too).</b><br />
  Each project becomes a room, and each agent becomes a pixel-art character that shows, in real time, what they’re doing.
</p>

<p align="center">
  <img alt="Node.js 22.12+" src="https://img.shields.io/badge/node-%E2%89%A522.12-5fa04e?logo=node.js&logoColor=white" />
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-7-3178c6?logo=typescript&logoColor=white" />
  <img alt="Docker" src="https://img.shields.io/badge/Docker-ready-2496ed?logo=docker&logoColor=white" />
  <img alt="Zero runtime dependencies" src="https://img.shields.io/badge/runtime%20dependencies-0-f08a3c" />
  <img alt="Portuguese interface" src="https://img.shields.io/badge/interface-PT--BR-4aa8e8" />
</p>

<p align="center">
  <img src="docs/screenshots/office.gif" width="820" alt="Animation of a Habblaud room: characters typing at their desks, subagents with badges and activity balloons" />
</p>

---

You open Claude Code in multiple projects, launch subagents, leave tasks running… and lose track of who is doing what. Habblaud turns that into an office that you can understand at a glance: who is typing, who raised a hand because they need you, who delivered the work and left, who went to grab coffee while waiting for the next instruction — and how much of each account you’ve already used in the 5-hour session and the week.

And when two or more agents are idle, the office gains social life: each one has its own personality, and they watch football together in the lounge, play video games and ping-pong, chat in the break room, get ready in the mirror, and bet coins in rock-paper-scissors. See [Social life](#social-life).

Everything runs on your machine, reading the files that Claude Code itself writes (and only the shell `alias` lines, to match each account’s name). Nothing leaves the computer: Habblaud does not read credentials or make external calls.

## Table of contents

- [What it looks like](#what-it-looks-like)
- [Installation](#installation)
- [How to use](#how-to-use)
- [Accounts and usage (5 hours and weekly)](#accounts-and-usage-5-hours-and-weekly)
- [Configuration](#configuration)
- [How it works](#how-it-works)
- [Privacy and security](#privacy-and-security)
- [Development](#development)
- [Troubleshooting](#troubleshooting)
- [Warning](#warning)
- [License](#license)
- [Social life](#social-life)

## What it looks like

**Overview.** The building has a reception area with elevators, a break room, bathrooms, and a lounge; each project with an open session gets its own room along the corridor. At the top are the counters and usage for each account; on the left, the rooms and agents; below, the activity feed.

![Overview of Habblaud: building with reception, break room, bathrooms, lounge, and project rooms; sidebar with rooms and agents; account usage at the top; activity feed below](docs/screenshots/overview.png)

<table>
  <tr>
    <td width="50%"><img src="docs/screenshots/agent-details.png" alt="Agent details drawer with current activity, tasks, subagents, timeline, and statistics" /></td>
    <td width="50%"><img src="docs/screenshots/night.png" alt="The office at night, with lamps on and rooms lit" /></td>
  </tr>
  <tr>
    <td><b>Agent details:</b> current activity, tasks with progress, subagents, timeline, and statistics.</td>
    <td><b>Day and night:</b> the sky in the windows and the lighting follow the local time.</td>
  </tr>
</table>

<table>
  <tr>
    <td width="42%"><img src="docs/screenshots/collab.png" alt="Subagent delivering results to the main agent while another agent asks for permission" /></td>
    <td width="58%">
      <b>Collaboration in plain sight.</b> Subagents are coworkers with their own names and badges: they arrive by the elevator, work in the project room, and when finished, they go to the agent who called them to deliver the result (📦) before leaving.<br /><br />
      <b>Needs you.</b> When an agent is waiting for permission or a response in the terminal, they run to their desk and raise a hand, with a flashing alert — and a notice appears on screen (optionally with sound and browser notification). You can approve it, answer the question, or send the next instruction right there.
    </td>
  </tr>
</table>

<table>
  <tr>
    <td width="58%">
      <b>Waiting for the shell.</b> When the agent finishes a turn but leaves a command running (tests, build, deploy…), they don’t leave to wander: they stay at the desk with an hourglass spinning above their head, the terminal showing progress, and a balloon with the command and time. And the wait becomes comedy: first they eat popcorn watching the terminal; after 3 minutes they cross their arms and spin in the chair; after 10 minutes they gather cobwebs; after 25 minutes they nap. When the command ends, they stand up and celebrate with confetti — or get a rain cloud if it failed. In the side list and details, a timer shows how long each command has been running.
    </td>
    <td width="42%"><img src="docs/screenshots/shell-wait.png" alt="Agent eating popcorn at the desk with an hourglass over their head and a balloon that says 'Run test suite · 1 min'; in the row ahead, the agent is waiting" /></td>
  </tr>
</table>

**The lights go out.** When you close the last session of a project, the last character goes to the switch, turns off the light, leaves by the elevator — and the room is dismantled, turning into a garden until a new project arrives. If the garden ends up between two rooms, the farthest room moves there: it is constructed in the empty space, the staff walk to it, and the old address disappears and is dismantled. That way the building never has gaps and shrinks on its own.

| 1. The room is assembled, still dark | 2. Someone turns on the light and everyone works | 3. The last one leaves and turns off the light | 4. The room becomes a garden |
| --- | --- | --- | --- |
| ![Room being assembled, with furniture appearing and lights off](docs/screenshots/lifecycle-1.png) | ![Room lit with three agents working at the tables](docs/screenshots/lifecycle-2.png) | ![Room with the last agent leaving and turning off the light](docs/screenshots/lifecycle-3.png) | ![Garden replacing the room after the last agent leaves](docs/screenshots/lifecycle-4.png) |

<table>
  <tr>
    <td width="34%"><img src="docs/screenshots/mobile.png" alt="Habblaud on a phone, with account usage at the top" /></td>
    <td>
      <b>Also on mobile.</b> The interface adapts to small screens: account usage sits at the top, the list of rooms turns into a drawer, and details open from bottom to top. See how to enable local network access in
      <a href="#open-on-mobile-optional">Open on mobile</a>.
    </td>
  </tr>
</table>

> The images above use the demo mode (fictional projects, people, and accounts).

## Installation

### Requirements

- **macOS** (tested) or Linux.
- **[Claude Code](https://code.claude.com)** installed, with one or more accounts (2.1.287 or newer for the mod).
- **Node.js 22.12+** and **npm** (developed with Node 24; Docker already uses Node 24).
- **Docker Desktop** (or Docker Engine with Compose v2), if you plan to run it in a container.

### 1. Download the project

```bash
git clone https://github.com/marmottajr/habblaud.git
cd habblaud
npm install
```

> `npm install` only downloads build tools (Vite, TypeScript, tsx…). The Habblaud server has no runtime dependencies: it uses only Node’s native modules.

### 2. Start Habblaud

**Option A — Docker (recommended for keeping it running all the time)**

```bash
npm run docker:up
```

The script detects your Claude Code accounts, mounts only the necessary folders (read-only), builds the image, and starts the container — which restarts automatically with Docker. Open **http://localhost:4747**.

**Option B — Node, without Docker**

```bash
npm run build
npm start
```

Open **http://localhost:4747**. For development, use `npm run dev` (server + Vite with hot reloading).

Now open Claude Code in any project and watch your agent arrive by the elevator. 🎉

### 3. Install the Habblaud mod in Claude Code (recommended)

```bash
npm run mod:install                        # the mod and permission/message plugins, in each account
npm run mod:install -- --sem-permissoes    # without responding to permissions and questions from the office
npm run mod:install -- --sem-mensagens     # without sending messages to agents from the office
```

Habblaud ships with a [mod](https://code.claude.com/docs/en/plugins/mods/overview) (a plugin that runs inside Claude Code) and installs it in each account through `claude plugin`, from this folder. With it:

- the **5-hour and weekly usage** of each account appears live in Habblaud;
- the terminal shows a line when **another session needs you** (permission or response);
- the command **`/habblaud`** becomes available in Claude Code;
- you can **approve or reject permission requests from the office** (“Do you want to…”) and **answer agent questions** with the `habblaud-permissoes` plugin (see [Respond from the office](#respond-from-the-office));
- you can **send messages to the agent from the office**, as if you were typing in their terminal, with the `habblaud-mensagens` plugin (see [Send messages](#send-messages)).

You need **Claude Code 2.1.287 or newer** (`claude --version`). The mod runs inside each session, with your permissions, and accesses only what is listed in [`mod/README.md`](mod/README.md); to check without running anything, `claude plugin validate mod/habblaud` shows the events it handles and the calls it makes. Sessions already open load the mod with `/reload-plugins` (or when reopened). If the account had the old setup (below), `mod:install` removes the tap and hook from `settings.json` (with backup), because the mod does the same. Check with `npm run mod:status`; to undo: `npm run mod:uninstall`.

> The mod is read from this folder. If you move the folder, run `npm run mod:install` again.

<details>
<summary><b>Claude Code older than 2.1.287: the old way</b></summary>

Without mods, the live usage and responding from the office come from two installers that edit each account’s `settings.json` (with backup before):

```bash
npm run usage:install    # adds a "tap" in front of the statusline of each account, which captures 5h/weekly usage
npm run hooks:install    # adds the PermissionRequest hook to respond to permissions from the office
```

Your statusline continues to appear the same. To undo: `npm run usage:uninstall` and `npm run hooks:uninstall`.
Both point to this folder: if you move the folder, run them again (until then, the account statusline shows an error). When updating Claude Code, switch to the mod: `npm run mod:install` removes the old tap and hook (with backup) so they do not capture usage or respond to the same request twice.

</details>

### 4. Codex in the office (optional)

If you also use **Codex** from OpenAI (the `codex` CLI or app), its sessions enter the same office: each project is a room — the same room as Claude Code when both are open in the same project — and each session is a character with the **CODEX** badge. Habblaud finds the Codex folder by itself (`~/.codex`, `CODEX_HOME`, or `~/.codex*`) and reads the conversations without installing anything. To see Codex **live** (what it’s doing now, who needs you) and approve commands from the office, install the hooks:

```bash
npm run codex:install      # adds the Habblaud hooks to ~/.codex/hooks.json (backup first; other hooks remain)
npm run codex:status       # checks status
```

Then **open Codex and approve the Habblaud hooks in `/hooks`**: Codex only runs a new hook after you approve it (Habblaud never stores that approval). With Habblaud in Docker, to send messages to Codex sessions also leave `npm run codex:bridge` running on Mac (see [Codex](#codex)).

### Open on mobile (optional)

By default Habblaud only accepts connections from the same computer. To open it on a phone (on the same Wi‑Fi), with Docker:

```bash
printf 'HABBLAUD_BIND=0.0.0.0\n' > .env
npm run docker:up -- --no-build
```

Then open `http://<computer-ip>:4747` on the phone (on macOS: `ipconfig getifaddr en0`; if it comes back empty, `ipconfig getifaddr en1`). In Node mode, use `HABBLAUD_HOST=0.0.0.0 npm start`.

> ⚠️ With this enabled, any device on the network can see the agents’ activity (commands, files, session titles). Use it only on trusted networks. The [terminal](#terminal) (and therefore responding and sending messages from the office) is disabled while the port is exposed. To revert: delete the `.env` and run `npm run docker:up -- --no-build`.

### Update

The version in use appears in the top bar, next to “Connected,” and in **Settings › About**. Every 6 hours Habblaud checks GitHub to see if a new version has been released (the [releases](https://github.com/marmottajr/habblaud/releases) of this repo). When a new one is released, a green **New version** badge appears in place of the number, along with a notice and a dot on the settings button. In **About** you’ll find the link to what changed and the **Check now** button (the notes for each version are also in [`CHANGELOG.md`](CHANGELOG.md)). To update:

```bash
git pull
npm install
npm run docker:up        # or: npm run build && npm start (and then npm run mod:install)
```

> If `git pull` stops with “Your local changes to the following files would be overwritten by merge:
> package-lock.json”, run `git checkout -- package-lock.json` and repeat: until 0.4.0, `npm install` changed that file.

The `docker:up` command also updates the mod for accounts where it is already installed (never installs on its own) and says:
“Mod updated to 0.3.0 in Account D; open sessions: /reload-plugins”. In Node mode, run `npm run mod:install` after updating. To avoid checking GitHub, use `HABBLAUD_UPDATE_CHECK=0` (in `.env`, for Docker).

#### Coming from CodeTown

Habblaud was called **CodeTown** until 0.3.2. After `git pull`, do this once:

```bash
npm install
npm run mod:install      # replaces the codetown marketplace and plugins with the habblaud ones, in each account
npm run docker:up        # removes the codetown container and copies the old volume data into the new one
```

- **Mod:** until `mod:install`, the Claude Code accounts complain about the `codetown` marketplace (the `mod/codetown*` folders changed names). `docker:up` warns, but does not change it automatically.
- **Docker:** the old volume (`codetown_codetown-data`) remains intact. After confirming the character names came through, delete it with `docker volume rm codetown_codetown-data`, and the old image with `docker image rm codetown:local`.
- **Local folder:** `~/.codetown` becomes `~/.habblaud` on its own (in the server, in `docker:up`, and in `mod:install`).
- **Browser:** preferences and coins carry over to the new keys the first time the page opens.
- **Variables:** the `CODETOWN_*` variables are no longer valid; rename them to `HABBLAUD_*` in `.env` (for example, `HABBLAUD_BIND`). The server and `docker:up` warn when they find an old one.
- **Repository:** it is now `github.com/marmottajr/habblaud` (GitHub redirects the old address). To correct the clone: `git remote set-url origin https://github.com/marmottajr/habblaud.git`. The local folder can keep the old name.
- Backups of `settings.json` taken before the switch remain with the name `settings.json.codetown-backup-<date>`.

### Uninstall

```bash
npm run mod:uninstall                       # removes the mod, message/permission plugins, and marketplace
npm run codex:uninstall                     # removes Habblaud hooks from Codex (other hooks remain)
npm run docker:down                         # stops the container
docker volume rm habblaud_habblaud-data     # deletes the container data (names, rooms, timeline, and stats)
docker image rm habblaud:local              # deletes the image
rm -rf ~/.habblaud                          # deletes local data (captured usage, names, rooms, timeline, and stats)
```

Then just delete the project folder — run `mod:uninstall` **first**, otherwise the Claude Code accounts will complain about the missing marketplace. If you used the old method, also run `npm run usage:uninstall` (restores the original statusline) and `npm run hooks:uninstall` (removes the permission hook); without them, the account statusline starts showing errors (and the hook fails silently). The `mod:install` command, which removes the old tap and hook, and the old installers and uninstallers leave copies named `settings.json.habblaud-backup-<date>` in each account folder (for example: `~/.claude/`); delete them if you no longer need them.

## How to use

### What each character is doing

| Status | What you see |
| --- | --- |
| **Working** | At the desk, typing. The monitor and a balloon show the activity: 📖 reading, ✏️ editing, 💻 terminal, 🧪 tests, 🌐 searching… |
| **Needs you** | Runs to the desk and raises a hand, with a flashing alert: they are waiting for a permission or response in the terminal. |
| **Waiting for the shell** | Finished the turn but left a command running (tests, build, deploy…), so they stay at the desk with an hourglass spinning over their head and the terminal in progress: they eat popcorn while watching it; after a while they get annoyed, spin in the chair, then fall asleep. |
| **Idle** | Finished the turn and walks around: coffee in the break room, water fountain, bathrooms, lounge sofa, phone on the sofa, mirror. With colleagues idle, they join a group: TV, video games, ping-pong, coffee talk, conversations, etc. |
| **Subagent completed** | Goes to the agent who called them, delivers the result, and leaves by the elevator. |
| **Session ended** | Leaves; if it was the last one in the room, it turns off the light before leaving. |

Each character has a **unique Brazilian name** (Marina, Henrique, Luan…) that stays with them while the session exists, and a **colored chip with the account letter** (C, D…).

### Interface

- **Top bar:** counters (rooms, agents, working, subagents, running shells, need your help) and an **account usage** card. The shells counter only appears while some command is running; click it to jump to whoever is waiting. Under the logo are the connection and version in use, which becomes the **New version** badge when a new version is released (see [Update](#update)).
- **Sidebar panel:** search, account filter, and the list of rooms with their agents and subagents.
- **Details drawer:** click a character (in the building or the list) to see activity, tasks, subagents, timeline, and statistics (tools, tokens, cost, changed lines, model, branch).
- **Feed:** the latest activities across the office.
- **Settings (⚙):** names, balloons, how much idle agents wander, day/night cycle, sounds, browser notifications, demo mode, and **About** (current version and new version). **Help (?)** has the full legend and shortcuts.
- **My day (📊):** where the time of the day went (see [My day](#my-day)). **Timelapse** and **History** (the clocks in the top bar): see [Day timelapse](#day-timelapse) and [Terminal](#terminal).

**Camera:** drag to move, scroll to zoom, double-click a character to follow them.

**Shortcuts:** `/` search · `F` follow selected · `T` terminal · `L` timelapse · `M` my day · `P` next request
(permission or question) · `O` or `0` overview · `Esc` clear selection · `[` sidebar · `]` feed · arrows/`WASD` move ·
`+` `-` zoom · `?` help.

### Day, night, and sounds

The office follows the **local time**: at night and in the early morning the grass and street turn bluish and dark, the streetlights, lamps, machines, and monitors light up with glow, rooms with people are illuminated (the light that turns off when the room empties still counts), cars pass with headlights on and fireflies appear in the garden. At dawn (~5–7 am) and dusk (~5–7 pm) everything gains a warm tone, and during the day the sun enters through the windows and draws light stripes on the floor — short at midday, long and orange at sunset. In **Settings › Day/Night Cycle** you can choose automatic, always day, or always night; to test a time, use `?hora=21:30` in the URL.

The **sounds** are off by default. When enabled in **Settings › Sounds**, they are synthesized in the browser itself (no audio files) and include: the keyboard of people working in the rooms, the “ding” of the elevator when someone arrives or leaves, the bell when someone needs you, the task completion chime, and the ping-pong and arcade sounds from the social circles.
You can control the overall volume and each category separately. With the tab hidden, only the bell plays.

### Terminal

Click an agent and use **Open terminal** to see the session conversation as Claude Code shows it: prompts, responses, each tool call (with the command or diff), and results, updated live. This works for main agents and subagents; in demo mode the conversation is fictional.

At the footer, for main agents, you can **type**: `Enter` sends the message and `Shift+Enter` inserts a new line. The text enters the session as if you typed it in their terminal (see [Send messages](#send-messages)); if the agent is busy, it is sent when they finish their current task. Subagents and historical sessions are read-only.

- **Search:** with the terminal in focus, `Ctrl+F` (`⌘F` on Mac) or the magnifying glass in the header opens a search in the conversation, case-insensitive and accent-insensitive. The counter shows the position (“3/17”); `Enter` and `Shift+Enter` jump to the next and previous match, expanding collapsed blocks (“… +N lines”) where the term appears. The search continues to work as new messages arrive. `Esc` closes the search; another `Esc` closes the terminal.
- **Filter:** **All**, **Only prompts** (your prompts and the agent’s final responses, excluding intermediary steps), or **Without tools**.
- **Copy:** hover (or focus) over a prompt, response, command, or result to copy it.
- **History:** the clock in the top bar lists sessions from the last 7 days of all accounts (up to 150), grouped by day, with search by title, project, or account. A closed session opens in the terminal with the project, title, and date in the header and “Session ended at …” at the footer; an open session opens the live terminal of the agent.

Because the terminal (and history) shows the entire conversation, it only exists when Habblaud is accessible **only from your own computer** (the default) and opened via `http://localhost` or `http://127.0.0.1`. With the port exposed to the network (`HABBLAUD_BIND=0.0.0.0` or `HABBLAUD_HOST=0.0.0.0`), it is disabled. Details in [Privacy and security](#privacy-and-security).

### Day timelapse

The **Timelapse** button (clock with the back arrow, or the `L` key) replays the day at high speed: rooms turning on and off, agents arriving, working, waiting for you, joining the social circles, subagents entering and leaving.
The playback bar shows the day, play/pause, speed (60×, 180×, or 600×: a 10-hour day in 10, 3⅓, or 1 minute), a draggable timeline with a graph of who was present and working, markers for the peaks (click to jump to them), and **Back to live**. While that happens, the office looks slightly sepia with the label **REPLAY 14:32**, and the feed continues to show what is happening now.

The server records the timeline **from the moment it is turned on** (it cannot reconstruct the past): summaries of what the office shows, without conversations, in `~/.habblaud/timeline/` (in Docker, in the data volume), with size limits per day and the last **7 days** kept. To disable recording: `HABBLAUD_TIMELINE=0`. Details in [`server/README.md`](server/README.md#timelapse-line).

Characters walk faster in replay mode, but at high speeds those who spend little time in the office barely reach their desks; jumping to another point shows everyone already in place.

### Respond from the office

With the permissions plugin installed (`npm run mod:install`, which installs it together with the mod; in Claude Code older than 2.1.287, `npm run hooks:install`), when an agent requests permission — to run a command, edit a file, open a page — the request appears in the office: the character raises a hand, a **Respond** alert appears on screen, and in the agent details the **Requests permission** card shows the command (or the edit diff) with the buttons:

- **Approve** — and, when Claude Code suggests it, **Approve and do not ask again** (the same rule the terminal would offer, for example `Bash(npm test:*)` in this project);
- **Reject** — with an optional reason, which goes to the agent, and the option to interrupt them;
- **Respond in terminal** — Habblaud leaves the request aside.

The dialog continues appearing in the terminal at the same time, and the first response wins: if you respond in the terminal, the office request disappears by itself. The **need your help** counter (and the `P` key) takes you to each request.

**Agent questions** (`AskUserQuestion`) also appear: the question card shows each question with the options and descriptions, as the terminal would. Choose an option (or several, when allowed) or write your own in **Other**, then use **Respond**; **Reject…** tells the agent you do not want to answer, and **Respond in terminal** leaves the question there. The response reaches the agent as if you had chosen it in the terminal.

- The request passes through a Claude Code `PermissionRequest` hook (the plugin version, or the old one), which only redirects it when there is **some Habblaud page open** on this computer; with Habblaud stopped or with no page open, it exits immediately and the terminal continues normally.
- Without a response from the office within 5 minutes, the request returns to terminal-only (the options for the plugin are in [`mod/README.md`](mod/README.md); in the old way, `npm run hooks:install -- --timeout 120` changes the time and `--port`, the port). In **background subagents** the Claude Code only shows the dialog in the terminal after the hook finishes: respond from the office or use **Respond in terminal**.
- It works with the same restriction as the terminal: only when Habblaud is accessible only from the local machine and opened via `http://localhost`. Check with `npm run mod:status` (or `npm run hooks:status`, in the old way).
- In demo mode, fictional agents also ask for permission and ask questions (fictitiously), to let you try it.

### Send messages

With the message plugin installed (`npm run mod:install`, which installs it alongside the mod; requires Claude Code 2.1.287 or newer), each main agent’s details gain a **Send message** section, and the footer of the [terminal](#terminal) becomes a typing box. Write and press `Enter` (`Shift+Enter` for a new line): the text enters the session **as if you had typed it in their terminal**. You can respond when the agent finishes the turn and waits for the next request, give a new instruction, or correct the course without searching for the right window.

- The box shows the state: **in queue** (the session checks for messages every 2 seconds), **delivered**, or **not delivered**, with the reason. If the agent is busy, the message waits and enters when they finish the turn, like a prompt typed while they are working.
- The plugin runs inside each session and only speaks with Habblaud on `127.0.0.1`. Without it (or in a session opened before installation: use `/reload-plugins`), a install hint appears in its place. Subagents do not receive messages.
- It works with the same terminal restrictions (only local access) and can be disabled with `HABBLAUD_MENSAGENS=0`.
  Read the warning in [Privacy and security](#privacy-and-security).
- In demo mode, fictional agents also receive messages (fictitiously).

### Edit the character

Each session arrives with a random name and appearance. To fix the character of a project, open the main agent’s details and click the pencil next to the name (**Edit character**). In the editor:

- **Name:** up to 24 characters. It cannot repeat the name of someone already in the office or the name chosen for another project.
- **Randomize:** picks another appearance.
- **Parts:** skin, hair, beard, eyes, top, bottom, shoes, and accessory, with a preview beside it.
- **Save:** applies to the project (the room). The next session opened there receives this character. If two sessions are open at the same time in the same room, the second receives a randomly generated character.
- **Back to random:** undo the choice.

The choice is stored in `~/.habblaud/names.json` and disappears after 60 days without use of the project. The editor follows the same restriction as the terminal: the pencil only appears with the terminal enabled (without `HABBLAUD_TERMINAL=0`) and local access, i.e. with Habblaud accessible only from your own computer and opened via `http://localhost`.

### Codex

Codex sessions (CLI or app) appear like Claude Code sessions: character, project room, activity, tasks, subagents, terminal, history, 5-hour and weekly usage, and **My day** (only tokens: Codex does not provide cost info). The account chip for Codex is empty and gets the **CODEX** badge.

- **Without installing anything**, Habblaud reads the files Codex itself writes (the conversations in `~/.codex/sessions` and the locks for open sessions in `~/.codex/thread-writer-locks`). However, Codex writes each step **after** it finishes and never writes “waiting for you”: without hooks, the office shows Codex delayed and does not notify when it needs you.
- **With hooks** (`npm run codex:install` and approve them in `/hooks`), Codex notifies Habblaud at each step: the session appears immediately, the activity is live, and a permission request raises the character’s hand.
- **Approve from the office:** with some Habblaud page open, the Codex approval request waits for your response in the **Requests permission** card for up to **25 seconds** (`npm run codex:install -- --espera <s>`, from 5 to 120): **Approve** or **Reject** (with reason). Unlike Claude Code, Codex only shows the approval in the terminal **after** the office responds or the time runs out — during that time the terminal shows “Awaiting response in Habblaud…”. There is no “always allow” or “interrupt,” and Codex does not allow answering its questions elsewhere.
- **Send messages:** the **Send message** box works for Codex too, through `codex queue`: the message enters the session queue and Codex picks it up when it finishes its current task (up to about 10 seconds later). In Node mode the Habblaud itself runs the command; **in Docker**, leave `npm run codex:bridge` running on Mac (the container cannot see your Codex).
- **5-hour and weekly usage:** comes from Codex’s own files and only refreshes while a session is running; the card shows the age of the numbers and “no quota” when the workspace is out of credits.
- **When the session enters:** with the first message (that is when Codex writes the project folder); a newly opened CLI without conversation does not appear.
- **When the session leaves the office:** the Codex CLI runs sessions on a background server that keeps them loaded up to a minute after they become idle and no one is watching; for that reason the character may take a little while to leave after you close the terminal.
- Cloud chat conversations from ChatGPT (without a file on the computer) do not appear. `HABBLAUD_CODEX=0` disables Codex.

### GitHub in the office

What agents do on GitHub animates the project room, without a token and without accessing the internet: Habblaud reads in the transcripts the commands (`gh pr create`, `gh pr merge`, `git push`, `gh run watch`, `gh pr checks`, `gh run view`, `gh release create`, and GitHub MCP tools) and their results.

| Event | What happens |
| --- | --- |
| 🎉 **PR opened or merged, release published** | Confetti falls in the room, everyone celebrates with jumps and a banner says the reason (“PR #12 merged!”) for ~12 s. |
| 🚨 **CI red** | Flashing sirens in the corners of the room, red floor, and a “!” balloon over whoever saw the failure, until a green CI in the room (which becomes a party) or for 10 min. |
| 🚀 **Push** | Only the alert and feed. |

<table>
  <tr>
    <td width="50%"><img src="docs/screenshots/github-party.png" alt="app-mobile room in a party: confetti falling, the golden banner 'PR #12 merged!' and Jéssica standing with arms up and a huge smile" /></td>
    <td width="50%"><img src="docs/screenshots/github-alarm.png" alt="data-pipeline room in alarm: red floor, red banner 'CI failed (feat/checkout)', flashing beacons at the top corners and a balloon '!' above the agent who saw it" /></td>
  </tr>
</table>

Each event also generates a notice (“🎉 Danilo opened PR #12 in habblaud”, “🚨 CI failed in habblaud (feat/x)”) and enters the feed. Only what happens live animates the room: what was already in the transcripts when Habblaud opened is only added to the history. With “reduce motion” enabled in the system, nothing blinks or spins. In demo mode, fictional PRs, merges, and CIs appear from time to time.

### My day

The **My day** button (or the `M` key) shows where the day went: how much time agents spent working and, in highlighted form, how much time they spent **waiting for you** (permission, question, or choice) — including the biggest wait, who waited, where, and when. Next to it, sessions, subagents, requests, tokens, and cost (when Claude Code records cost in the transcript), plus hourly charts, by project (what waited for you the most to the least), and by account, along with the ranking of the longest waits. Choose the day in the selector (Habblaud keeps the last 30); with today open, the panel updates every 30 s. Each chart has a table version, and the legend toggles each status.

The time is **agent time**: two agents working for one hour count as two hours. Habblaud only counts what happens while it is running, and the day follows your browser’s time zone. With demo mode enabled, the panel shows fictional numbers (with the “demo” badge) and allows switching to real data; demo agents never appear in the real statistics.

### Demo mode

Want to see the office full without having any sessions open?

- Add **`?mock=1`** to the URL (for example: http://localhost:4747/?mock=1) to simulate everything in the browser, without your real sessions. Parameters: `&speed=3` speeds up time and `&sessions=6` changes the number of simulated sessions.
- Or enable it from the interface — **View demo** (when the office is empty) or **Settings › Demo mode** — which adds fictional agents alongside the real ones. With `npm run demo` (or `HABBLAUD_DEMO=1` in the Docker `.env`), this mode starts enabled.

## Accounts and usage (5 hours and weekly)

> **Codex** accounts are included automatically (each `~/.codex*` folder or `CODEX_HOME` is an account; the letter comes from an `alias x='CODEX_HOME=… codex'`, if any), and their usage comes from Codex files; see [Codex](#codex). The rest of this section is about Claude Code.

If you use more than one Claude Code account (for example, alias `c` with `~/.claude` and alias `d` with `CLAUDE_CONFIG_DIR=~/.claude-account2`), Habblaud shows them together: each agent gets the chip of their account and the top bar shows, for each account, the **percentage used** of the 5-hour and weekly sessions and **when each limit resets**.

**How accounts are recognized.** Each Claude Code configuration folder is an account: `~/.claude` and any `~/.claude*` with `projects/` or `sessions/` (and `CLAUDE_CONFIG_DIR`). To assign the letter to each one, Habblaud reads, from shell files (`~/.zshrc`, `~/.bashrc`…), only the `alias x='... claude ...'` lines:

```bash
alias c='claude'
alias d='CLAUDE_CONFIG_DIR=~/.claude-account2 claude'
```

becomes **Account C** and **Account D**. Only shortcuts of up to 3 letters count; accounts without a shortcut receive A, B…

**Where the numbers come from.** The recommended method is the Habblaud mod (`npm run mod:install`, Claude Code 2.1.287+):
inside each session, it receives the plan limits from Claude Code itself and stores only the percentages of 5 hours and the week (and when they reset) in `~/.habblaud/usage/<account>.json`. The numbers arrive after the next response from each account. Check with `npm run mod:status`. In older Claude Code versions, the statusline tap (`npm run usage:install`) does the same via the statusline command, in the same file.

<details>
<summary><b>Details of the tap and the /usage cache</b></summary>

- The `usage:install` (old method) changes, in `<account>/settings.json`, **only** the `statusLine.command` field: the original command (for example, `npx -y ccstatusline`) is run through `node "<habblaud folder>/scripts/statusline-tap.mjs" -- <original command>` (on Windows, the original command runs in Git Bash as Claude Code would). A copy of the file is saved before as `settings.json.habblaud-backup-<date>`. If the account had no statusline, one is created that only captures usage. `npm run usage:install -- --dry-run` shows what would change without writing anything.
- The tap forwards the same JSON to the statusline (output and exit code remain the same) and writes **only** `{accountId, configDir, fetchedAt, five_hour, seven_day}` — nothing about prompts, costs, or project paths. Any capture failure is ignored: the statusline never breaks because of Habblaud.

| Source | How it works |
| --- | --- |
| **Habblaud mod** (recommended) | Live, as described above. Replaces the tap: `mod:install` removes the tap from the account. |
| Statusline tap (Claude Code older than 2.1.287) | Live, via the statusline command, in the same file. |
| `/usage` cache (always on) | Claude Code saves the last result of the `/usage` command. In Node mode, Habblaud reads it every 60 s; in Docker, the value from the last `npm run docker:up` is used. |
| `claudeaccount`… | ??? |

The sources are local files: none of them read passwords or tokens, and none make network calls. The newest numbers always win. Numbers older than 30 minutes appear as **stale**; a window that restarted since the last collection appears as **—** until new numbers arrive.

</details>

## Configuration

Everything works without any configuration. If you need to adjust it, use environment variables:

| Variable | Default | Purpose |
| --- | --- | --- |
| `HABBLAUD_PORT` | `4747` | HTTP port (in Docker, the port published on the host). |
| `HABBLAUD_HOST` | `127.0.0.1` | Server bind interface in Node mode. Outside `127.0.0.1`/`localhost`, the terminal (and responding and sending messages from the office) is disabled. |
| `HABBLAUD_BIND` | `127.0.0.1` | Docker-only (in `.env`): where the port is published. `0.0.0.0` exposes the local network (and disables the terminal and anything that acts on sessions). |
| `HABBLAUD_CLAUDE_DIRS` | auto-detection | Account folders, separated by commas (for example: `/path/account1,/path/account2`). |
| `HABBLAUD_DATA_DIR` | `~/.habblaud` | Where Habblaud stores its own data (character names and room names, timeline data, and My day stats). |
| `HABBLAUD_TIMELINE` | enabled | `0` disables timeline recording (days already recorded remain in timelapse). In Docker it is always enabled. |
| `HABBLAUD_USAGE_DIR` | `~/.habblaud/usage` | Where the mod (or the statusline tap) stores usage. |
| `HABBLAUD_DEMO` | disabled | `1` enables demo mode at startup. |
| `HABBLAUD_ALLOWED_HOSTS` | — | Extra hostnames accepted in the address (for example: `my-mac.local`), in addition to `localhost` and IPs. |
| `HABBLAUD_TERMINAL` | enabled (only with local access) | `0` disables the terminal, responding and sending messages from the office, and the character editor. If the port is exposed they are already disabled, so the route just returns 403/403-like errors. |
| `HABBLAUD_MENSAGENS` | enabled (with terminal) | `0` disables office messaging only (the box in the terminal and agent details). |
| `HABBLAUD_CODEX` | enabled | `0` disables Codex in the office. |
| `HABBLAUD_CODEX_DIRS` | auto-detection | Codex folders, separated by commas (instead of `~/.codex*` and `CODEX_HOME`). |
| `HABBLAUD_CODEX_BIN` | `codex` from PATH (on Windows, `codex.exe`) | The Codex binary that delivers messages (`codex queue`), in Node mode or with `npm run codex:bridge`. |
| `HABBLAUD_UPDATE_CHECK` | enabled | `0` disables the new version check (a query to GitHub releases every 6 hours). |
| `HABBLAUD_ACCOUNTS` | — | JSON to personalize name, letter, or color, keyed by the account folder name. Example: `[{"id":".claude-account2","name":"Work","short":"T","color":"#5cc97b"}]`. |

**In Docker**, the variables `HABBLAUD_PORT`, `HABBLAUD_BIND`, `HABBLAUD_ALLOWED_HOSTS`, `HABBLAUD_DEMO`, `HABBLAUD_TERMINAL`,
`HABBLAUD_MENSAGENS`, `HABBLAUD_CODEX`, and `HABBLAUD_UPDATE_CHECK` apply (in `.env` or the environment), and `HABBLAUD_CLAUDE_DIRS`, `HABBLAUD_CODEX_DIRS`, `HABBLAUD_USAGE_DIR`, and `HABBLAUD_ACCOUNTS` are read by `docker:up` on the host; the rest remain fixed inside the container. Options: `npm run docker:up -- --no-build` (starts without rebuilding), `npm run docker:down` (stops), and `npm run docker:logs` (follows logs).

## How it works

```
 ~/.claude*/sessions/<pid>.json ─────────────────┐
 ~/.claude*/projects/<project>/<session>.jsonl ───┼──▶ Node server ──▶ office model ──▶ SSE ──▶ browser
 .../<session>/subagents/**/agent-*.jsonl ────────┘    (1 s polling)                                 (canvas + interface)
```

- **Who is in the office:** while a session is open, Claude Code keeps `sessions/<pid>.json` with the project and status (busy, idle, waiting for you, or waiting for a shell in the background). That is what determines who appears and what each one is doing.
- **Running shells:** in the transcripts, each `Bash` in the background (or long-running command in the foreground) becomes a “shell” with a label and timer, until the notification says it finished, failed, or was interrupted.
- **Social life:** the circles, personalities, and coins are simulated by the browser (`client/src/world/social/`), without affecting the real agents. The personality comes from each agent’s seed (the same in any browser); wallets are stored in the browser’s `localStorage`.
- **What each one is doing:** the server tracks the end of session transcripts (`.jsonl`) and translates each tool call into a Portuguese activity with an icon. It also derives tasks, title, model, and stats.
- **Subagents:** transcripts in `<session>/subagents/` (including workflow ones) become characters linked to the agent who called them.
- **GitHub:** PRs, pushes, CI, and releases come from the same transcript lines (the command and its output, or the `gitOperation` that Claude Code itself logs); nothing is queried from GitHub.
- **The drawing:** the browser receives the state through SSE and draws everything on a canvas — characters, furniture, floors, and walls are pixel art generated by code; the logo, illustrations, and wall frames were generated with AI.

<details>
<summary><b>Code structure and API</b></summary>

```
shared/   protocol (types.ts), PT-BR activities, names, demo simulator
server/   HTTP + SSE server: accounts and usage, reading sessions and transcripts, office model
client/   Vite: src/art (procedural pixel art), src/world (the office on canvas), src/ui (interface)
scripts/  build scripts, docker-up, installers (mod, statusline tap, permission hook), and screenshots
mod/      Habblaud mod and permission/message plugins (Claude Code plugins; marketplace in .claude-plugin/)
```

| Route | Description |
| --- | --- |
| `GET /api/stream` | SSE with `snapshot`, `feed`, and `notice` events (format in `shared/types.ts`). |
| `GET /api/snapshot` | Current office state. |
| `GET /api/agents/:id` | Agent details, with up to 200 activities. |
| `GET /api/agents/:id/terminal` | Terminal SSE (events `init` and `append`); local-only. |
| `PUT /api/agents/:id/character` | Edit character: `{name, seed, parts}` stores the name and appearance of the agent as the project character; local-only. |
| `DELETE /api/agents/:id/character` | “Back to random”: deletes the project character and the agent reverts to the random name; local-only. |
| `GET /api/sessions/recent` | History: sessions from the last 7 days of all accounts (up to 150); local-only. |
| `GET /api/sessions/:account/:sessionId/terminal` | SSE for a historical session conversation (same protocol as terminal); local-only. |
| `GET /api/stats?day=AAAA-MM-DD` | My day statistics (time by status, projects, accounts, hours, waits, tokens, and cost). |
| `GET /api/stats/days` | Days with stats (last 30). |
| `GET /api/timeline/days` | Days with recorded timelapse data, including size and first/last recorded times. |
| `GET /api/timeline/:day` | Timelapse for one day (`AAAA-MM-DD`), as JSONL (with gzip). |
| `GET /api/health` | Health: version, demo, Docker, terminal, responding and sending messages from the office, sources, and usage status for each account. |
| `POST /api/demo` | `{"enabled": true | false}` enables or disables simulated agents. |
| `POST /api/rooms/rename` | `{"id": room, "name": name}` renames a room (empty reverts to folder name); name stored in `rooms.json` in the data folder. Local-only. |
| `GET /api/mod/summary` | For the Claude Code mod: version, number of agents, how many are working, and who needs you (excluding demo mode and, with `?account=&session=`, excluding the current session). |
| `/api/permissions…` | Respond from the office: the permission hook records the request (permission or question) and waits; the page fetches the details and decides or responds. Local-only. |
| `/api/messages…` and `/api/mod/inbox…` | Send messages: the page leaves the message in the queue and monitors delivery; the `habblaud-mensagens` plugin fetches it, delivers it to the session, and confirms. Local-only. |
| `POST /api/codex/events` | Events from Codex hooks (session opened, tool usage, approval, end of turn). Local-only. |
| `/api/codex/bridge/poll` and `/ack` | The `npm run codex:bridge` command checks for messages for Codex and confirms delivery. Local-only. |

More details about the server in [`server/README.md`](server/README.md).

</details>

<details>
<summary><b>What Docker mounts and why</b></summary>

| Host | Container | Purpose |
| --- | --- | --- |
| `<account>/sessions/` | `/claude/<account>/sessions` (read-only) | Open sessions and their status. |
| `<account>/projects/` | `/claude/<account>/projects` (read-only) | Session and subagent transcripts. |
| `~/.habblaud/usage/` | `/usage` (read-only) | Usage captured by the mod (or statusline tap). |
| volume `habblaud-data` | `/data` | Habblaud data (character names, timelapse timeline, and My day stats). |

The account folder is **never** mounted in full (that is where credentials and settings live). The container runs as an unprivileged user, with a read-only filesystem, no extra capabilities, and `no-new-privileges`. Account metadata (letter, email, organization) is read on the host by `docker:up` and passed to the container.

</details>

## Privacy and security

- **Read-only:** Habblaud never writes to Claude Code folders. The exceptions are the installers you run:
  the `npm run mod:install` / `mod:uninstall` command uses `claude plugin` itself (which registers the marketplace and plugins in `settings.json` and `<account>/plugins/`) and, during installation, removes the old tap and hook with backup; in the old way, `npm run usage:install` / `usage:uninstall` only changes `statusLine.command` in `settings.json`, and `npm run hooks:install` / `hooks:uninstall` only updates the `hooks.PermissionRequest` list — always with a backup first.
- **The mod:** runs inside each Claude Code session, with your permissions (like any plugin), and does only what is listed in [`mod/README.md`](mod/README.md) — `claude plugin validate mod/habblaud` shows the events and calls without executing anything. It only writes the 5-hour and weekly usage percentages (and when they reset) in `~/.habblaud/usage/<account>.json`; for the “needs you” line and the `/habblaud` command, it only speaks with Habblaud on `127.0.0.1`. It does not read the conversation, does not call the model, and does not send anything outside your computer. It is loaded from this folder: whatever is in it (including after a `git pull`) is what runs. The message plugin (`habblaud-mensagens`) is separate precisely because it acts: it types into the session what you sent from the office.
- **Local-only by default:** the server only accepts connections from your own computer; exposing the local network is optional.
  There is no telemetry. The only external call is the version check: every 6 hours, an anonymous query to GitHub’s public API (`api.github.com/repos/marmottajr/habblaud/releases/latest`) without a token. It does not send anything about your sessions; GitHub only sees your IP and the version in use, which are included in the `User-Agent`.
  `HABBLAUD_UPDATE_CHECK=0` disables the query.
- **No credentials:** Habblaud does not read passwords or access tokens. From each account’s `.claude.json`, it only uses the email, organization, and `/usage` cache; live usage comes from the mod (or the statusline tap).
- **Secrets masked:** tokens and passwords with a known format (`Bearer`, `-u username:password`, `TOKEN=`, keys like `sk-…`, `ghp_…`, `AKIA…`, JWTs, URLs with passwords) are turned into `***` before reaching the browser.
- **Protected against malicious sites:** the server rejects addresses that are not `localhost`/IP (DNS rebinding) and `POST` requests from other origins (CSRF), and does not allow the page to be embedded in other sites.
- **Terminal is local-only:** the full conversation of sessions (and the history of closed sessions, with titles) only leaves the server when Habblaud is accessible only from your own computer (`HABBLAUD_HOST` local in Node; `HABBLAUD_BIND` local in Docker) — there is no way to enable it with the port exposed — and each request must come through `localhost`/`127.0.0.1`: network IPs and names in `HABBLAUD_ALLOWED_HOSTS` (proxies, tunnels) are rejected. Secrets are masked and long text is truncated before reaching the browser; in demo mode the conversation is fictional. `HABBLAUD_TERMINAL=0` disables it entirely.
- **Timelapse timeline:** only the summaries already shown on screen (activity in one line, status, titles, account usage, without emails, full commands, or conversations) are recorded in `~/.habblaud/timeline/` and deleted after 7 days. `HABBLAUD_TIMELINE=0` disables recording.
- **Respond from the office, local-only:** approving or rejecting acts on real sessions, so it follows the same restriction as the terminal (local bind, local `Host`, no proxies or tunnels) and only exists with the permission hook installed (the `habblaud-permissoes` plugin or the old version). Responses require JSON and a local origin (a browser page cannot send them), the hook only speaks with `127.0.0.1`, and if there is doubt — Habblaud offline, an error, timeout — it exits without deciding: terminal rules apply. The full command or diff leaves the server only to the person who opened the page from their own computer. “Always allow” only applies a rule that Claude Code itself suggested for that request. Caution: any program or person who can open `http://localhost:4747` on this machine can also respond; on shared machines with other users, do not install the hook (`npm run mod:install -- --sem-permissoes`).
- **Send messages, local-only — and with a warning:** the message enters the session as if you had typed it, so it follows what the agent can do with a request from you. It uses the same restrictions (local bind, local `Host`, JSON and local origin, so a browser page cannot send it), but **any program on this machine** that talks to `http://localhost:4747` — including an agent running a command — can leave a message for another session that has the plugin. If that is not acceptable for you (shared machine, agents running without supervision), do not install the plugin (`npm run mod:install -- --sem-mensagens`) or disable it with `HABBLAUD_MENSAGENS=0`. The text of messages is not stored: it disappears from the server as soon as it is delivered.
- **Character editor, local-only:** saving or resetting changes the office and writes to `names.json`, so it follows the same restriction as the terminal (local bind, local `Host`, no proxies or tunnels): without it, the pencil does not appear and the server responds `403`. Changes require JSON and a local origin. `HABBLAUD_TERMINAL=0` disables it together.
- **My day stats:** only aggregated numbers (time by status, counts, tokens, cost) with project, account, and agent names, stored in `HABBLAUD_DATA_DIR/stats/` for 30 days — nothing from the conversation.
- **Codex:** Habblaud reads only the conversations (`sessions/`, `archived_sessions/`) and open-session locks (`thread-writer-locks/`); in Docker, only these three folders are mounted, read-only. It never reads `auth.json`, `config.toml`, the shell environment (`shell_snapshots/`), prompt history, logs, or Codex databases, and it does not show ChatGPT account IDs. `npm run codex:install` only adds groups in `hooks.json` (with backup; other app hooks remain in the same place) and stores `~/.habblaud/codex-hook.json`; approving hooks is always your decision, in `/hooks`. The hooks only speak with `127.0.0.1`. Messages to Codex use the same warning as Claude Code: any program on this machine that speaks to Habblaud can leave a message in a session queue.
- **What appears on screen:** summaries of activity (tool, file, command, or query), session titles, tasks, and stats (and, in the terminal, the conversation). Do not expose the port on networks you do not trust.

## Development

| Command | What it does |
| --- | --- |
| `npm run dev` | Server + Vite at http://localhost:4747, with hot reloading. |
| `npm run dev:client` | Vite only, at http://localhost:5173 (open with `?mock=1`; `/api` is proxied to port 4747). |
| `npm run demo` | `npm run dev` with demo mode enabled. |
| `npm run build` / `npm start` | Build and run the production version. |
| `npm test` | Tests (Vitest). |
| `npm run typecheck` | Type checking for client, server, and scripts. |
| `claude plugin test mod/habblaud` | Mod tests (without a session, account, or network); same for `mod/habblaud-mensagens`. |
| `claude plugin validate .` | Validates the marketplace (`.claude-plugin/marketplace.json`); with `mod/habblaud`, `mod/habblaud-permissoes`, or `mod/habblaud-mensagens`, validates the plugin and lists events and calls. |
| `claude --plugin-dir mod/habblaud` | Opens a session with the mod from this folder, without installing (edit and run `/reload-plugins`). |
| `npm run mod:status` | Shows, by account, the marketplace, plugins, and installed versions. |
| `npm run demo:timeline` | Generates a fictional timeline (demo mode simulator) for timelapse. |
| `npm run release` | Publishes the `package.json` version on GitHub (tag and release with notes from `CHANGELOG.md`). |

To take screenshots without opening a browser, `scripts/shot.mjs` uses an isolated headless Chromium (Playwright).
On the first run, download the browser once: `npx playwright-core install chromium-headless-shell`.

```bash
node scripts/shot.mjs 'http://localhost:4747/?mock=1&speed=3' /tmp/habblaud.png --size 1400x900 --wait 4000
```

In the browser console, `habblaud.world.debug` has tools for testing scenes (for example:
`habblaud.world.debug.setHour(21)` to see the night). To fix the time when opening, use `?hora=21:30` in the URL.

**Timelapse only with fictional data** (for example, to record a GIF): `npm run demo:timeline` runs the demo simulator offline and saves a full day (by default, yesterday from 9am to 7pm, with a busy morning, a quieter lunch, and an afternoon peak) in `<tmp>/habblaud-demo/timeline/`. Then start a Habblaud instance that reads only this folder and does not show your sessions, and open Timelapse:

```bash
npm run demo:timeline -- --data-dir /tmp/habblaud-demo        # options: --date, --start 8:30, --hours, --sessions, --seed
mkdir -p /tmp/habblaud-demo/vazio
HABBLAUD_DATA_DIR=/tmp/habblaud-demo HABBLAUD_TIMELINE=0 HABBLAUD_CLAUDE_DIRS=/tmp/habblaud-demo/vazio \
  HABBLAUD_PORT=4848 npm start                                 # after npm run build; then open http://localhost:4848
```

`HABBLAUD_TIMELINE=0` prevents writing to that folder; with recording enabled, days older than 7 days are deleted.

**Publishing a release:** every version has its own section in [`CHANGELOG.md`](CHANGELOG.md), with what changed. During development, note changes under “Unreleased”. To release:

1. Bump the version with `npm version minor --no-git-tag-version` (or `patch` for a bugfix-only release).
2. Replace “Unreleased” with the version and date (`## [0.3.0] - AAAA-MM-DD`), leave an empty “Unreleased” at the top, and update the links at the end. `npm test` fails if the `package.json` version does not have a matching section.
3. Merge to `main` and run `npm run release` (requires authenticated [`gh`](https://cli.github.com/); `-- --dry-run` shows only the release notes). The script creates the `v0.3.0` tag and a release with the text from the section. After that, anyone using Habblaud sees the **New version** badge.

## Troubleshooting

<details>
<summary><b>The office is empty</b></summary>

Only **open** Claude Code sessions appear. Check that there is a session running and that the account was detected in `http://localhost:4747/api/health`. If your account folders are elsewhere, use `HABBLAUD_CLAUDE_DIRS=/path/account1,/path/account2`.

</details>

<details>
<summary><b>The usage shows “no data” or “stale”</b></summary>

Run `npm run mod:install` (or, in Claude Code older than 2.1.287, `npm run usage:install`) and check with `npm run mod:status` (or `npm run usage:status`). The numbers arrive after the next response in an open session for that account; for a session opened before installation, run `/reload-plugins` or reopen the session. A **—** in place of the percentage means the window restarted since the last collection.

</details>

<details>
<summary><b>The mod does not load in a session</b></summary>

Run `npm run mod:status`: it shows the Claude Code version (the mod needs 2.1.287 or newer) and, by account, whether the marketplace points to this folder and whether the plugins are installed and enabled. In a session opened before installation, run `/reload-plugins`; `/plugin` shows, below the tabs, the loaded mods (for example: `1 mod active · habblaud`). Mods do not run with `"disableAllHooks": true` in the account `settings.json` or with `claude --safe-mode`.

</details>

<details>
<summary><b>“Port 4747 is already in use”</b></summary>

Another Habblaud instance (Node or Docker) is already running. Stop it (`npm run docker:down`, or Ctrl+C in the terminal running `npm start`) or use another port: `HABBLAUD_PORT=4848 npm run docker:up` (Docker) or `HABBLAUD_PORT=4848 npm start` (Node).

</details>

<details>
<summary><b>It does not open on mobile</b></summary>

Check that you created `.env` with `HABBLAUD_BIND=0.0.0.0` and recreated the container (`npm run docker:up -- --no-build`), that the phone is on the same Wi‑Fi, and that the firewall allows connections to port 4747. IP works directly; to open by name (for example: `my-mac.local`), add `HABBLAUD_ALLOWED_HOSTS=my-mac.local` (in Docker, in the same `.env`).

</details>

<details>
<summary><b>The terminal does not open</b></summary>

The terminal only exists when Habblaud is accessible only from your own computer. Check that `.env` does not contain `HABBLAUD_BIND=0.0.0.0` (or, in Node mode, that you did not use `HABBLAUD_HOST=0.0.0.0`) and that `HABBLAUD_TERMINAL=0` is not set; then open via `http://localhost:4747` (opening by network IP or a name in `HABBLAUD_ALLOWED_HOSTS` is rejected). In Docker, a container created before this feature needs to be recreated: `npm run docker:up`. The startup log (`npm run docker:logs`) tells whether the terminal is enabled and, if not, why.

</details>

<details>
<summary><b>The permission request (or question) does not appear in the office</b></summary>

Run `npm run mod:status`: it tells you, by account, whether the `habblaud-permissoes` plugin is installed and enabled (and whether an old hook remains, which would make two respond), and whether Habblaud is responding to requests. In the old way, `npm run hooks:status` tells whether the hook is installed and pointing to this folder. The request is only diverted when some Habblaud page is open via `http://localhost` (or `127.0.0.1`) and the terminal is enabled (same restriction). Sessions opened before installation load the plugin with `/reload-plugins` (or when reopened). In the old way, if Habblaud uses another port, reinstall with `npm run hooks:install -- --port <port>`. For agent questions, the plugin must be version 0.6.0 or newer: run `npm run mod:install` after updating.

</details>

<details>
<summary><b>Codex does not appear in the office (or appears delayed)</b></summary>

The startup log (`npm run docker:logs`) tells how many Codex accounts Habblaud found; if there are none, point to the folder with `HABBLAUD_CODEX_DIRS` (and run `npm run docker:up` again: in Docker, only the folders that existed when `docker:up` was run are mounted). Without hooks, Codex appears through its own files, which are only written after each step:
run `npm run codex:install`, **approve the hooks in `/hooks` in Codex**, and check with `npm run codex:status`. Codex runs hooks through the login shell, which may have an older Node; `codex:install` chooses a Node 22+ and says which one (or use `--node <path>`). A newly opened CLI session only appears with the **first message**: before that, Codex does not tell which project folder it is in (it only creates the session lock), and without the folder there is no room.

</details>

<details>
<summary><b>The message box does not appear (or stays in queue)</b></summary>

The box only appears for main agents whose session has the `habblaud-mensagens` plugin connected: run `npm run mod:status` (it tells, by account, whether the plugin is installed and whether Habblaud has messages enabled) and, in sessions opened before installation, `/reload-plugins`. Without the plugin, the agent details show the install hint. Messages follow the terminal restriction and `HABBLAUD_MENSAGENS=0` disables them; the startup log (`npm run docker:logs`) tells whether they are enabled and, if not, why. A message that stays **in queue** and fails with “the session did not fetch the message” means the session stopped checking Habblaud (it was closed, or the plugin was disabled).

</details>

<details>
<summary><b>In Docker, a closed session remains in the office</b></summary>

This happens if Claude Code was forcibly closed without deleting its own registration in `sessions/` (in Docker it is impossible to confirm whether the process still exists). Running with Node (`npm start`), Habblaud checks processes and this does not happen.

</details>

<details>
<summary><b>In Docker, an account outside /Users does not appear</b></summary>

Docker Desktop only shares some macOS folders with containers (by default `/Users`, `/Volumes`, `/private`, and `/tmp`). Add the folder in *Settings › Resources › File sharing*.

</details>

<details>
<summary><b>I want to start from scratch</b></summary>

`npm run docker:down`, then `docker volume rm habblaud_habblaud-data` (deletes stored names) and `npm run docker:up`.

</details>

## Warning

Habblaud is an independent project, **not affiliated with, sponsored by, or endorsed by Anthropic**. “Claude” and “Claude Code” are trademarks of Anthropic, used here only to describe what the project works with.

To show the agents, Habblaud reads only local files that Claude Code writes on your machine (session records, transcripts, and account settings). This format is not documented and may change between Claude Code versions:
after an update, Habblaud may stop working, partially or completely, until it is adjusted.

## License

[MIT](LICENSE). The images in `client/public/assets` (logo, illustrations, frames, and posters) were generated with AI for this project and converted to pixel art by the scripts in `scripts/assets/`.

## Social life

When two or more agents are idle — idle or waiting for a shell for more than 40 seconds — they stop wandering alone and join up. No one plans anything: each character has a **personality**, **friends**, and **rivals**, and that decides what they prefer to do, with whom, and what they say. Anyone waiting for a shell leaves the desk for the social circle (alone, still with popcorn) and takes the hourglass with them; when the command ends — or when you send a new request to someone — they announce it to the group (“Opa, they called me! 🏃”) and run back to the desk.

<p align="center">
  <img src="docs/screenshots/social-lounge.gif" width="816" alt="Habblaud lounge with three circles at the same time: three coworkers on the sofa watching football on TV (the screen flashes GOL), a ping-pong match in the background, and a coffee break with several colleagues" />
</p>

### The circles

| | Circle | What happens |
| --- | --- | --- |
| 📺 | **TV in the lounge** | Football, soap opera, or cartoons, with popcorn on the sofa. During football, the crowd celebrates together with the flashing “GOL” on the screen (or laments the opponent’s goal); in soap opera scenes, hearts appear and the group reacts. |
| 🎮 | **Video game** | Two on the sofa with the controller, TV split-screen (racing or fighting), best of 3, provocations (“What lag is this?!”), and cheering. |
| 👾 | **Arcade** | Duel on the two machines in the lounge, single match. |
| 🏓 | **Ping-pong** | Up to 5 points, with the ball going back and forth, scoreboard in balloons (“3 × 2 🏓”), and cheering behind the table. |
| ☕ | **Coffee talk** | Everyone grabs coffee (or water) and sits at the table: gossip with the names of colleagues (“Did you see Rafaela’s commit? 👀”), jokes (the group laughs), work (“Deploy this Friday? 🚀”), and small talk. |
| 💬 | **Conversation** | Two colleagues standing in a corner of the reception, break room, or lounge. |
| ✊ | **Rock-paper-scissors with coins** | “Jo… ken… po!”, the gestures appear above their heads, the winner celebrates and coins fly from one to the other; the loser is upset and, if competitive, asks for a rematch. |
| 💄 | **Bathroom mirror** | Lipstick or combing, with the face reflected in the mirror and a glow at the end. It can be alone or in pairs (“Lend me the comb?”). |

<table>
  <tr>
    <td width="50%"><img src="docs/screenshots/social-rps.png" alt="Rock-paper-scissors at the reception: Lia celebrates with a coin above her head and a balloon 'I won!', coins flying from Bruna (upset, with a balloon 'Again?!')" /></td>
    <td width="50%"><img src="docs/screenshots/social-kitchen.png" alt="Coffee break: four colleagues sitting at the long table with coffee, with balloons 'Everything will work out!' and 'Hahaha'" /></td>
  </tr>
  <tr>
    <td><b>Rock-paper-scissors with coins.</b> The stakes come from personality (who is gambling bets high, who is frugal bets little) and never exceed the balance of whoever has less.</td>
    <td><b>Coffee talk.</b> The one who talks the most is the more sociable one; reactions depend on the subject (laughter for jokes, 👀 for gossip).</td>
  </tr>
  <tr>
    <td><img src="docs/screenshots/social-mirror.png" alt="Two colleagues in front of sink mirrors fixing themselves up, with their faces reflected and the balloon 'You look amazing!'" /></td>
    <td><img src="docs/screenshots/social-drawer.png" alt="Social life section in the agent details: 'Watching a soap opera on TV with Bruna and Iara', 115 coins, 1 win and 0 losses, character traits, recent events, and wallet summary" /></td>
  </tr>
  <tr>
    <td><b>In the mirror.</b> People who care about appearance pass by the bathroom whenever they can — and appear reflected.</td>
    <td><b>In the agent details.</b> What they are doing, wallet, score, personality, friendships and rivalries (with history), and the account summary.</td>
  </tr>
</table>

### Personalities

Each agent has 2 or 3 traits, randomly assigned from their seed (it is always the same person, in any browser):

🏆 Competition · 🎲 Betting · 🎮 Games · 📺 Series and TV · 🗣️ Gossip · 💄 Vanity · ☕ Caffeine · 😂 Jokes · 🏓 Sports ·
🙈 Shyness · 💰 Economy · 😴 Laziness · 🧘 Calm · 📚 Reading

The traits affect what each one chooses (people who like series turn on the TV, those who like sports call for ping-pong), who invites whom (friends seek friends; rivals challenge each other), what they say, and even who plays better. Each one also has a catchphrase (“It’s on me!”, “Let’s code!”). Hover over a trait in the agent details to see what it does.

### Coins

Fictional coins (🪙), just to make the betting fun:

| | |
| --- | --- |
| **Joined the office** | 🪙100 (subagents, 🪙30) |
| **Task completed** (task list item) | +🪙10 |
| **Request handled** (end of turn) | +🪙5 |
| **Subagent delivered result** | +🪙15 |
| **Bets** (rock-paper-scissors; matches between rivals or with someone who likes betting) | what the loser gives goes to the winner |

Each gain appears as “+🪙10” above the head; matches and bets enter the activity feed. The balance, score, and history are saved in the browser (each browser has its own economy: bets are drawn there) and are forgotten three days after the agent leaves.

> All of this is just a performance of Habblaud: nothing changes in the real Claude Code agents, which keep working normally.

---

<p align="center">
  Made with ☕ and many <a href="https://code.claude.com">Claude Code</a> agents.
</p>
```

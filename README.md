<h1 align="center">Claude Egress</h1>

<p align="center">A fixed outbound address for Claude, on a server you own.<br>Claude Code, Claude Desktop and the Claude sites in your browser leave from one IP.<br>Everything else, including your VPN, keeps its usual route.</p>

<p align="center">
  <img src="docs/dashboard.png" width="820" alt="The Claude Egress dashboard">
</p>

## What you need

- macOS 13 or later.
- An Ubuntu VPS of your own, with a public IPv4 and SSH reachable. Each person needs their own.
- Your own Claude account.

No server is bundled. The app ships with no addresses and no passwords: on first run it asks for yours and sets the VPS up over SSH.

## Install

1. Download **`claude-egress-<version>-macos.dmg`** from the [latest release](../../releases/latest).
2. Open it and drag **Claude Egress** onto Applications.
3. Open it from Applications.

The app is signed with a Developer ID and notarised by Apple, so it opens straight away. It updates itself afterwards, with your say-so.

<sub>The release also carries `…-macos.zip`, which is what the built-in updater downloads. Either one installs the same app.</sub>

## First run

It closes any running Claude, then asks four questions.

| Question | What to answer |
| --- | --- |
| Clear Claude data? | **No**, unless you want a clean slate. A backup is saved either way. |
| Server | **Add a server** → **Set up a server over SSH**, then your VPS address, user and port. OpenSSH asks for the password itself; the app never stores it. |
| Project folder | Where Claude Code should open. |
| Allow a system PAC | Needed for the Claude sites in your ordinary browser. macOS asks for your administrator password in its own dialog. |

Then press **Sign in**, finish signing in through the browser that opens, and press **Terminal**.

Adding a server that is already set up costs nothing: the app checks it is healthy and reuses it, without reinstalling or restarting anything.

## Browser proxying

One button, three modes. The line underneath always says what the current one actually routes.

<table>
<tr>
<td align="center" width="33%"><img src="docs/dashboard.png" alt="Claude only"><br><b>Claude only</b><br><sub>default</sub></td>
<td align="center" width="33%"><img src="docs/all-sites.png" alt="All sites"><br><b>All sites</b><br><sub>everything but localhost</sub></td>
<td align="center" width="33%"><img src="docs/off.png" alt="Off"><br><b>Off</b><br><sub>browser untouched</sub></td>
</tr>
</table>

In **Claude only** the published Claude and Anthropic domains go through your server and nothing else does. **All sites** sends the whole browser through it, except `localhost`, `*.local` and private networks, so the sign-in callback and your intranet still work — and your server sees where every tab goes. **Off** puts your previous browser settings back; Claude Code and Desktop keep using the server either way.

## Updates

<p align="center"><img src="docs/update.png" width="760" alt="An available update"></p>

The version sits in the header. The app checks at startup and whenever you press **Re-check**, and tells you when there is nothing new. An update is verified against its published SHA256 and its contents are checked before anything is replaced; the browser settings are restored and the relay stopped first, so an update never leaves the machine half-configured.

## When something is wrong

<p align="center"><img src="docs/error.png" width="760" alt="A failed connection"></p>

The status line fills red and the app stops the relay rather than let traffic leave from the wrong address. Click the line for the full message. **Report** writes a zip to your Desktop with the version, the environment and the tail of both logs — your password, server address and user name are removed from it.

Keep the window open: the connection lives as long as it does.

## Honest limits

This is a relay, not a system-wide block. Programs that ignore proxy settings can still reach the network directly, and a fixed address does not guarantee that a service is available to you or that an account is in good standing. Windows is written but has not been piloted on real hardware.

## Licence

MIT. See [LICENSE](LICENSE) and the [changelog](CHANGELOG.md).

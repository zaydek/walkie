# Walkie privacy

Last updated: 2026-10-17. This covers Walkie 0.2.

## In short

- Walkie runs on your computer. Your phone reaches it only over your own Tailscale network, and only the Tailscale
  account this computer is signed in to can open it.
- What you say goes to xAI to be turned into words, and the replies Walkie reads aloud go to xAI to be spoken. Both go
  straight from your computer to xAI with your own xAI key.
- Feedback goes only when you send it.
- Walkie sends a few usage counts to its own server (that it was installed, started, that a phone joined, and how
  many turns were sent and read aloud), never your words. `walkie telemetry off` stops them.
- Everything else Walkie keeps stays on your computer, in the folders listed below.

## What it reads

- **Your phone's microphone**: while you hold the button, or while hands-free is on, if you turn it on. The phone's
  browser asks you first.
- **Your Claude Code sessions on this computer**: each session's folder and name, and its transcript, to show your
  messages, Claude's replies and steps on your phone, and to read the replies aloud.
- **Each Claude Code session's context settings**: only the few settings that set its context window, from how that
  session was started. The rest of its environment is never kept or logged.
- **Tailscale's status on this computer**, to check it is ready and to find your phone's link.
- **Your xAI key**, from the settings file below.
- **Your settings** for Walkie.

## What it keeps on this computer

| What | Where | How long, how big |
| --- | --- | --- |
| Your xAI key and this install's feedback sign-in | `~/.config/walkie/env` (only you can read it) | Until you uninstall |
| What you said, as audio, so you can tap your message and hear it again | `~/.local/share/walkie/state/takes/` | Until you uninstall |
| What you said, while it waits to reach Claude Code | `~/.local/share/walkie/state/inbox/` | Removed after 2 days |
| Spoken replies, so a repeat is not made twice | `~/.local/share/walkie/state/tts/` | Up to 300 MB; the oldest go first |
| Sample voices for the Settings screen | `~/.local/share/walkie/state/voices/` | Until you uninstall |
| Feedback you write, with its files | `~/.local/share/walkie/state/feedback/` | Until you uninstall |
| Settings | `~/.local/share/walkie/state/prefs.json` | Until you uninstall |
| A log of what Walkie did | `~/.local/share/walkie/state/server.log` (only you can read it) | Until you uninstall |
| The app | `~/.local/share/walkie/` | Until you uninstall |
| The `walkie` command, and one line in your shell's startup file that puts it on your PATH | `~/.local/bin/walkie`, and `~/.zshrc` on a Mac or `~/.bashrc` on Linux | Until you uninstall |
| The Claude Code plugin | Claude Code's plugin folders | Until you uninstall |

## What it sends, to whom, and when

| What | To | When |
| --- | --- | --- |
| Your words, as audio | xAI's speech-to-text, with your key | When you let go of the button, or when hands-free hears you finish |
| The text of each reply it reads aloud | xAI's text-to-speech, with your key | As each reply arrives; a line it has made before is played from disk instead |
| Your words, as text | The Claude Code session you picked, on this computer | After xAI turns them into words |
| What happens in that session | Your phone, over your Tailscale network | While the phone has it open |
| A request for a sample voice | xAI's public docs site, with no key | When you preview a voice in Settings, once per voice |
| An install id, and which download fits your computer (macOS or Linux, and its CPU) | Walkie's own server | When you run the install line or `walkie update` |
| A sign-in with GitHub or Google, if you choose it (you can continue as a guest) | Walkie's own server, and GitHub or Google | When you install |
| Your feedback's words, the files you add (screenshots or a screen recording), and the recent messages of the chat you were in unless you turn that off | Walkie's own server, for Walkie's author | Only when you send feedback; if it can't go, it is kept and tried again while Walkie is on |
| A request for the newest version | Walkie's own server | Only when you run `walkie update` |
| Usage counts: what happened (installed or updated, started in the foreground or background, a phone joined, a turn sent, a reply read aloud), a count since Walkie started, the time, Walkie's version, and your computer's system and CPU (for example linux-x64). Each is sent with this install's feedback sign-in, so it is filed under this install, and under your GitHub or Google account if you signed in with one | Walkie's own server, for Walkie's author | As each happens, once, never queued or retried. Never after `walkie telemetry off`, or while `DO_NOT_TRACK=1` is set |

## What it never sends

- Your xAI key, except to xAI.
- Anything from your phone or your sessions to Walkie's own server, except feedback you send and the usage counts above.
- In a usage count: your words, audio, session names, folder paths, your computer's name or your Tailscale login.
- The audio it keeps on your computer, and its log.

## Turning usage counts off

`walkie telemetry off` stops them, and `walkie telemetry on` starts them again. Setting `DO_NOT_TRACK=1` stops them
too. `walkie telemetry show` and `walkie status` say whether they are on.

## How to delete it

In a terminal: `walkie uninstall`. It removes the app, its settings and key, everything in the table above, the
Claude Code plugin, the PATH line and the `walkie` command.

## Changes

A change to this page is published here, with a new date at the top, when a version that needs it ships.

## Contact

Open an issue at https://github.com/zaydek/walkie/issues.

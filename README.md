# Sid Browser releases

Sid Browser is a Mac browser with an agent built in, and `sid` is its command line. This repository holds the releases only: the
app, its checksums, and the installer.

## Install

```sh
curl -fsSL https://sid0709.github.io/sid-releases/install.sh | sh
```

Then, in a new terminal:

```sh
sid init
```

**What you need:** a Mac with Apple silicon and macOS 15 or later.

**What the installer does:**
1. It downloads the latest release.
2. It checks the release's SHA-256 and the certificate it is signed with.
3. It puts `SidBrowser.app` in `/Applications`, or in `~/Applications` when it can't write there.
4. It links the command at `~/.sid/bin/sid` and puts that folder on your PATH.

Nothing is run as root, and the downloads are the only requests it makes.

### Installer options

```sh
curl -fsSL https://sid0709.github.io/sid-releases/install.sh | sh -s -- --version 2.6.0 --app-dir ~/Applications --no-modify-path
```

| Option | What it does |
| --- | --- |
| `--version` | installs that release instead of the latest |
| `--channel beta` | installs from the beta channel |
| `--app-dir` | chooses where the app goes |
| `--no-modify-path` | leaves your shell's start-up file alone |
| `--yes` | asks nothing |

## Using it

```sh
sid "summarize the pricing page of example.com as a table"
```

- **Background:** when Sid is closed, the command starts it in the background, with no window.
- **Watching:** `sid show` brings the window forward, and `sid hide` sends it back.
- **All commands:** `sid help`.

## Updating and removing

| Command | What it does |
| --- | --- |
| `sid update` | moves to the newest release; Sid starts again as it was |
| `sid update --check` | says whether there is one |
| `sid uninstall` | removes the app and the command, and keeps your profiles and history |
| `sid uninstall --all` | removes those as well |

## Checking a download

**Checksums:** each release lists `SHA256SUMS` beside its zip.

**Signature:** the releases are signed with Sid's own certificate, and the installer and `sid update` check it. They are not
notarized by Apple. Installing with the line above avoids Gatekeeper's warning, because a file that `curl` downloads is not marked
as coming from the internet.

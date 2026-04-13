[](https://discord.com/invite/WVBeWsNXK4)

**A free, open source, and extensible speech-to-text application that works completely offline.**

Handy is a cross-platform desktop application that provides simple, privacy-focused speech transcription. Press a shortcut, speak, and have your words appear in any text field. This happens on your own computer without sending any information to the cloud.

Handy was created to fill the gap for a truly open source, extensible speech-to-text tool. As stated on [handy.computer](https://handy.computer):

- **Free**: Accessibility tooling belongs in everyone's hands, not behind a paywall

- **Open Source**: Together we can build further. Extend Handy for yourself and contribute to something bigger

- **Private**: Your voice stays on your computer. Get transcriptions without sending audio to the cloud

- **Simple**: One tool, one job. Transcribe what you say and put it into a text box

Handy isn't trying to be the best speech-to-text app—it's trying to be the most forkable one.

- **Press** a configurable keyboard shortcut to start/stop recording (or use push-to-talk mode)

- **Speak** your words while the shortcut is active

- **Release** and Handy processes your speech using Whisper

- **Get** your transcribed text pasted directly into whatever app you're using

The process is entirely local:

- Silence is filtered using VAD (Voice Activity Detection) with Silero

- Transcription uses your choice of models:

**Whisper models** (Small/Medium/Turbo/Large) with GPU acceleration when available

- **Parakeet V3** - CPU-optimized model with excellent performance and automatic language detection

- Works on Windows, macOS, and Linux

- Download the latest release from the [releases page](https://github.com/cjpais/Handy/releases) or the [website](https://handy.computer)

**macOS**: Also available via [Homebrew cask](https://formulae.brew.sh/cask/handy): `brew install --cask handy`

- **Windows**: Also available via [winget](https://github.com/microsoft/winget-pkgs): `winget install cjpais.Handy` 

**Note:** The Homebrew cask and winget package are not maintained by the Handy developers.

- Install the application

- Launch Handy and grant necessary system permissions (microphone, accessibility)

- Configure your preferred keyboard shortcuts in Settings

- Start transcribing!

For detailed build instructions including platform-specific requirements, see [BUILD.md](/cjpais/Handy/blob/main/BUILD.md).

[](https://www.raycast.com/mattiacolombomc/handy)

Control Handy from [Raycast](https://www.raycast.com) — start/stop recording, browse transcript history, manage dictionary, switch models and languages.

[Source](https://github.com/mattiacolombomc/raycast-handy) · by [@mattiacolombomc](https://github.com/mattiacolombomc)

Handy is built as a Tauri application combining:

- **Frontend**: React + TypeScript with Tailwind CSS for the settings UI

- **Backend**: Rust for system integration, audio processing, and ML inference

- **Core Libraries**:

`whisper-rs`: Local speech recognition with Whisper models

- `transcribe-rs`: CPU-optimized speech recognition with Parakeet models

- `cpal`: Cross-platform audio I/O

- `vad-rs`: Voice Activity Detection

- `rdev`: Global keyboard shortcuts and system events

- `rubato`: Audio resampling

Handy includes an advanced debug mode for development and troubleshooting. Access it by pressing:

- **macOS**: `Cmd+Shift+D`

- **Windows/Linux**: `Ctrl+Shift+D`

Handy supports command-line flags for controlling a running instance and customizing startup behavior. These work on all platforms (macOS, Windows, Linux).

**Remote control flags** (sent to an already-running instance via the single-instance plugin):

handy --toggle-transcription    # Toggle recording on/off
handy --toggle-post-process     # Toggle recording with post-processing on/off
handy --cancel                  # Cancel the current operation

**Startup flags:**

handy --start-hidden            # Start without showing the main window
handy --no-tray                 # Start without the system tray icon
handy --debug                   # Enable debug mode with verbose logging
handy --help                    # Show all available flags

Flags can be combined for autostart scenarios:

handy --start-hidden --no-tray

**macOS tip:** When Handy is installed as an app bundle, invoke the binary directly:

/Applications/Handy.app/Contents/MacOS/Handy --toggle-transcription

## Known Issues &amp; Current Limitations
[

](#known-issues--current-limitations)

This project is actively being developed and has some [known issues](https://github.com/cjpais/Handy/issues). We believe in transparency about the current state:
### Major Issues (Help Wanted)
[

](#major-issues-help-wanted)

**Whisper Model Crashes:**

- Whisper models crash on certain system configurations (Windows and Linux)

- Does not affect all systems - issue is configuration-dependent

If you experience crashes and are a developer, please help to fix and provide debug logs!

**Wayland Support (Linux):**

- Limited support for Wayland display server

- Requires [`wtype`](https://github.com/atx/wtype) or [`dotool`](https://sr.ht/~geb/dotool/) for text input to work correctly (see [Linux Notes](#linux-notes) below for installation)

**Text Input Tools:**

For reliable text input on Linux, install the appropriate tool for your display server:

Display Server
Recommended Tool
Install Command

X11
`xdotool`
`sudo apt install xdotool`

Wayland
`wtype`
`sudo apt install wtype`

Both
`dotool`
`sudo apt install dotool` (requires `input` group)

- **X11**: Install `xdotool` for both direct typing and clipboard paste shortcuts

- **Wayland**: Install `wtype` (preferred) or `dotool` for text input to work correctly

- **dotool setup**: Requires adding your user to the `input` group: `sudo usermod -aG input $USER` (then log out and back in)

Without these tools, Handy falls back to enigo which may have limited compatibility, especially on Wayland.

**Other Notes:**

- 

**Runtime library dependency (`libgtk-layer-shell.so.0`)**:

Handy links `gtk-layer-shell` on Linux. If startup fails with `error while loading shared libraries: libgtk-layer-shell.so.0`, install the runtime package for your distro:

Distro
Package to install
Example command

Ubuntu/Debian
`libgtk-layer-shell0`
`sudo apt install libgtk-layer-shell0`

Fedora/RHEL
`gtk-layer-shell`
`sudo dnf install gtk-layer-shell`

Arch Linux
`gtk-layer-shell`
`sudo pacman -S gtk-layer-shell`

- 

For building from source on Ubuntu/Debian, you may also need `libgtk-layer-shell-dev`.

- 

The recording overlay is disabled by default on Linux (`Overlay Position: None`) because certain compositors treat it as the active window. When the overlay is visible it can steal focus, which prevents Handy from pasting back into the application that triggered transcription. If you enable the overlay anyway, be aware that clipboard-based pasting might fail or end up in the wrong window.

- 

If you are having trouble with the app, running with the environment variable `WEBKIT_DISABLE_DMABUF_RENDERER=1` may help

- 

If Handy fails to start reliably on Linux, see [Troubleshooting → Linux Startup Crashes or Instability](#linux-startup-crashes-or-instability).

- 

**Global keyboard shortcuts (Wayland):** On Wayland, system-level shortcuts must be configured through your desktop environment or window manager. Use the [CLI flags](#cli-parameters) as the command for your custom shortcut.

**GNOME:**

Open **Settings &gt; Keyboard &gt; Keyboard Shortcuts &gt; Custom Shortcuts**

- Click the **+** button to add a new shortcut

- Set the **Name** to `Toggle Handy Transcription`

- Set the **Command** to `handy --toggle-transcription`

- Click **Set Shortcut** and press your desired key combination (e.g., `Super+O`)

**KDE Plasma:**

- Open **System Settings &gt; Shortcuts &gt; Custom Shortcuts**

- Click **Edit &gt; New &gt; Global Shortcut &gt; Command/URL**

- Name it `Toggle Handy Transcription`

- In the **Trigger** tab, set your desired key combination

- In the **Action** tab, set the command to `handy --toggle-transcription`

**Sway / i3:**

Add to your config file (`~/.config/sway/config` or `~/.config/i3/config`):

bindsym $mod+o exec handy --toggle-transcription

**Hyprland:**

Add to your config file (`~/.config/hypr/hyprland.conf`):

bind = $mainMod, O, exec, handy --toggle-transcription

- 

You can also manage global shortcuts outside of Handy via Unix signals, which lets Wayland window managers or other hotkey daemons keep ownership of keybindings:

Signal
Action
Example

`SIGUSR2`
Toggle transcription
`pkill -USR2 -n handy`

`SIGUSR1`
Toggle transcription with post-processing
`pkill -USR1 -n handy`

Example Sway config:

bindsym $mod+o exec pkill -USR2 -n handy
bindsym $mod+p exec pkill -USR1 -n handy

`pkill` here simply delivers the signal—it does not terminate the process.

- **macOS (both Intel and Apple Silicon)**

- **x64 Windows**

- **x64 Linux**

### System Requirements/Recommendations
[

](#system-requirementsrecommendations)

The following are recommendations for running Handy on your own machine. If you don't meet the system requirements, the performance of the application may be degraded. We are working on improving the performance across all kinds of computers and hardware.

**For Whisper Models:**

- **macOS**: M series Mac, Intel Mac

- **Windows**: Intel, AMD, or NVIDIA GPU

- **Linux**: Intel, AMD, or NVIDIA GPU

**For Parakeet V3 Model:**

- **CPU-only operation** - runs on a wide variety of hardware

- **Minimum**: Intel Skylake (6th gen) or equivalent AMD processors

- **Performance**: ~5x real-time speed on mid-range hardware (tested on i5)

- **Automatic language detection** - no manual language selection required

## Roadmap &amp; Active Development
[

](#roadmap--active-development)

We're actively working on several features and improvements. Contributions and feedback are welcome!

**Debug Logging:**

- Adding debug logging to a file to help diagnose issues

**macOS Keyboard Improvements:**

- Support for Globe key as transcription trigger

- A rewrite of global shortcut handling for MacOS, and potentially other OS's too.

**Opt-in Analytics:**

- Collect anonymous usage data to help improve Handy

- Privacy-first approach with clear opt-in

**Settings Refactoring:**

- Cleanup and refactor settings system which is becoming bloated and messy

- Implement better abstractions for settings management

**Tauri Commands Cleanup:**

- Abstract and organize Tauri command patterns

- Investigate tauri-specta for improved type safety and organization

## Verify Release Signatures
[

](#verify-release-signatures)

Handy release artifacts are signed with Tauri's updater signature format. The public key is stored in [`src-tauri/tauri.conf.json`](/cjpais/Handy/blob/main/src-tauri/tauri.conf.json) under `plugins.updater.pubkey`.

To verify a release manually, set `ARTIFACT` to the filename you downloaded, save the `pubkey` value from `src-tauri/tauri.conf.json` to `handy.pub.b64`, then decode the public key and matching `.sig` file from base64 and verify the artifact with `minisign`:

# Replace with the file you downloaded
ARTIFACT="Handy_0.8.1_amd64.AppImage"

python3 - "$ARTIFACT" &lt;&lt;'PY'
import base64, pathlib, sys

artifact = sys.argv[1]

pub = pathlib.Path("handy.pub.b64").read_text().strip()
pathlib.Path("handy.pub").write_bytes(base64.b64decode(pub))

sig = pathlib.Path(f"{artifact}.sig").read_text().strip()
pathlib.Path(f"{artifact}.minisig").write_bytes(base64.b64decode(sig))
PY

minisign -Vm "$ARTIFACT" \
  -p handy.pub \
  -x "$ARTIFACT.minisig"

On success, `minisign` prints:
```
Signature and comment signature verified

```

Do not use `gpg` for these `.sig` files.

### Manual Model Installation (For Proxy Users or Network Restrictions)
[

](#manual-model-installation-for-proxy-users-or-network-restrictions)

If you're behind a proxy, firewall, or in a restricted network environment where Handy cannot download models automatically, you can manually download and install them. The URLs are publicly accessible from any browser.
Step 1: Find Your App Data Directory[

](#step-1-find-your-app-data-directory)

- Open Handy settings

- Navigate to the **About** section

- Copy the "App Data Directory" path shown there, or use the shortcuts:

**macOS**: `Cmd+Shift+D` to open debug menu

- **Windows/Linux**: `Ctrl+Shift+D` to open debug menu

The typical paths are:

- **macOS**: `~/Library/Application Support/com.pais.handy/`

- **Windows**: `C:\Users\{username}\AppData\Roaming\com.pais.handy\`

- **Linux**: `~/.config/com.pais.handy/`

Step 2: Create Models Directory[

](#step-2-create-models-directory)

Inside your app data directory, create a `models` folder if it doesn't already exist:

# macOS/Linux
mkdir -p ~/Library/Application\ Support/com.pais.handy/models

# Windows (PowerShell)
New-Item -ItemType Directory -Force -Path "$env:APPDATA\com.pais.handy\models"
Step 3: Download Model Files[

](#step-3-download-model-files)

Download the models you want from below

**Whisper Models (single .bin files):**

- Small (487 MB): `https://blob.handy.computer/ggml-small.bin`

- Medium (492 MB): `https://blob.handy.computer/whisper-medium-q4_1.bin`

- Turbo (1600 MB): `https://blob.handy.computer/ggml-large-v3-turbo.bin`

- Large (1100 MB): `https://blob.handy.computer/ggml-large-v3-q5_0.bin`

**Parakeet Models (compressed archives):**

- V2 (473 MB): `https://blob.handy.computer/parakeet-v2-int8.tar.gz`

- V3 (478 MB): `https://blob.handy.computer/parakeet-v3-int8.tar.gz`

**For Whisper Models (.bin files):**

Simply place the `.bin` file directly into the `models` directory:
```
{app_data_dir}/models/
├── ggml-small.bin
├── whisper-medium-q4_1.bin
├── ggml-large-v3-turbo.bin
└── ggml-large-v3-q5_0.bin

```

**For Parakeet Models (.tar.gz archives):**

- Extract the `.tar.gz` file

- Place the **extracted directory** into the `models` folder

- The directory must be named exactly as follows:

**Parakeet V2**: `parakeet-tdt-0.6b-v2-int8`

- **Parakeet V3**: `parakeet-tdt-0.6b-v3-int8`

Final structure should look like:
```
{app_data_dir}/models/
├── parakeet-tdt-0.6b-v2-int8/     (directory with model files inside)
│   ├── (model files)
│   └── (config files)
└── parakeet-tdt-0.6b-v3-int8/     (directory with model files inside)
    ├── (model files)
    └── (config files)

```

**Important Notes:**

- For Parakeet models, the extracted directory name **must** match exactly as shown above

- Do not rename the `.bin` files for Whisper models—use the exact filenames from the download URLs

- After placing the files, restart Handy to detect the new models

Step 5: Verify Installation[

](#step-5-verify-installation)

- Restart Handy

- Open Settings → Models

- Your manually installed models should now appear as "Downloaded"

- Select the model you want to use and test transcription

Handy can auto-discover custom Whisper GGML models placed in the `models` directory. This is useful for users who want to use fine-tuned or community models not included in the default model list.

**How to use:**

- Obtain a Whisper model in GGML `.bin` format (e.g., from [Hugging Face](https://huggingface.co/models?search=whisper%20ggml))

- Place the `.bin` file in your `models` directory (see paths above)

- Restart Handy to discover the new model

- The model will appear in the "Custom Models" section of the Models settings page

**Important:**

- Community models are user-provided and may not receive troubleshooting assistance

- The model must be a valid Whisper GGML format (`.bin` file)

- Model name is derived from the filename (e.g., `my-custom-model.bin` → "My Custom Model")

### Linux Startup Crashes or Instability
[

](#linux-startup-crashes-or-instability)

If Handy fails to start reliably on Linux — for example, it crashes shortly after launch, never shows its window, or reports a Wayland protocol error — try the steps below in order.

**1. Install (or reinstall) `gtk-layer-shell`**

Handy uses `gtk-layer-shell` for its recording overlay and links against it at runtime. A missing or broken installation is the most common cause of startup failures and can manifest as a crash or a hang well before any window is shown. Make sure the runtime package is installed for your distro:

Distro
Package to install
Example command

Ubuntu/Debian
`libgtk-layer-shell0`
`sudo apt install libgtk-layer-shell0`

Fedora/RHEL
`gtk-layer-shell`
`sudo dnf install gtk-layer-shell`

Arch Linux
`gtk-layer-shell`
`sudo pacman -S gtk-layer-shell`

If it is already installed and you still see startup problems, try reinstalling it (e.g. `sudo pacman -S gtk-layer-shell` again) in case the library files were corrupted by a partial upgrade.

**2. Disable the GTK layer shell overlay (`HANDY_NO_GTK_LAYER_SHELL`)**

If installing the library does not help, you can skip `gtk-layer-shell` initialization entirely as a workaround. On some compositors (notably KDE Plasma under Wayland) it has been reported to interact poorly with the recording overlay. With this variable set, the overlay falls back to a regular always-on-top window:

HANDY_NO_GTK_LAYER_SHELL=1 handy

**3. Disable WebKit DMA-BUF renderer (`WEBKIT_DISABLE_DMABUF_RENDERER`)**

On some GPU/driver combinations the WebKitGTK DMA-BUF renderer can cause the window to fail to render or to crash. Try:

WEBKIT_DISABLE_DMABUF_RENDERER=1 handy

**Making a workaround permanent**

Once you've found a flag that helps, export it from your shell profile (`~/.bashrc`, `~/.zshenv`, …) or from the desktop autostart entry that launches Handy. If you launch Handy from a `.desktop` file, you can prefix the `Exec=` line, e.g.:

Exec=env HANDY_NO_GTK_LAYER_SHELL=1 handy

If a workaround helps you, please [open an issue](https://github.com/cjpais/Handy/issues) describing your distro, desktop environment, and session type — that information helps us narrow down the underlying bug.

- **Check existing issues** at [github.com/cjpais/Handy/issues](https://github.com/cjpais/Handy/issues)

- **Fork the repository** and create a feature branch

- **Test thoroughly** on your target platform

- **Submit a pull request** with clear description of changes

- **Join the discussion** - reach out at [contact@handy.computer](mailto:contact@handy.computer)

The goal is to create both a useful tool and a foundation for others to build upon—a well-patterned, simple codebase that serves the community.

## Sponsors

MIT License - see [LICENSE](/cjpais/Handy/blob/main/LICENSE) file for details.

- **Whisper** by OpenAI for the speech recognition model

- **whisper.cpp and ggml** for amazing cross-platform whisper inference/acceleration

- **Silero** for great lightweight VAD

- **Tauri** team for the excellent Rust-based app framework

- **Community contributors** helping make Handy better
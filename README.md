# indir

A robust, feature-rich Bash wrapper script around `yt-dlp` for downloading YouTube videos and audio with automated configurations, quality capping, smart duplicate renaming, and metadata/thumbnail embedding.

## Features

- **Format Selection:** Easily download as high-quality video (MP4) or high-quality audio (Opus).
- **Quality Capped at 4K:** Automatically downloads the absolute best resolution up to 4K (2160p), avoiding excessive bandwidth consumption from 8K streams.
- **Smart Duplicate Prevention:** If a file with the same name already exists in the destination folder, the script automatically appends `(2)`, `(3)`, etc. instead of overwriting.
- **Playlist Resumption:** Automatically tracks downloaded playlist items using a persistent archive file, allowing seamless resumption if interrupted.
- **Anti-Blocking Measures:** Configured with a standard Chrome User Agent, random sleep intervals (10-25s), retries, and rate limits to mimic human behavior and avoid Google's rate limits.
- **Metadata & Thumbnails:** Automatic embedding of metadata and thumbnails (using `mutagen` for tag injection).
- **Cookies Integration:** Auto-detects Netscape-format cookies from a configured local file for smooth downloads.

---

## Dependencies for Arch Linux Users

Ensure the following packages are installed on your Arch Linux system:

### 1. Core Packages
Install `ffmpeg` and `deno` (used by `yt-dlp` to solve JavaScript challenges on YouTube):
```bash
sudo pacman -S ffmpeg deno git
```

### 2. Python Mutagen (For Thumbnail Embedding)
Install the `mutagen` library to embed video/audio thumbnails into your media:
```bash
sudo pacman -S python-mutagen
```

### 3. uv & yt-dlp (Recommended Tool Manager Setup)
The script expects `yt-dlp` to be managed via `uv` so it can auto-update seamlessly:
```bash
sudo pacman -S uv
uv tool install --with mutagen --upgrade yt-dlp
```
*Note: If you install `yt-dlp` via `pacman -S yt-dlp`, make sure it is in your `PATH`. The auto-update check at startup will run `uv tool upgrade` if `uv` is installed, or fallback gracefully.*

---

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/brnakblut/indir.git
   cd indir
   ```

2. Make the script executable:
   ```bash
   chmod +x indir
   ```

3. Move the script to a folder in your `PATH` (such as `~/.local/bin/`):
   ```bash
   mkdir -p ~/.local/bin
   cp indir ~/.local/bin/
   ```

4. Configure your YouTube cookies file:
   The script loads cookies from `/home/baran/Documents/www.youtube.com_cookies.txt`. Ensure your Netscape cookies file is exported there.

---

## Usage

Simply run:
```bash
indir [URL] [options]
```

### Examples:
- Download a single song or video interactively:
  ```bash
  indir
  ```
- Pass the URL directly:
  ```bash
  indir "https://www.youtube.com/watch?v=..."
  ```
- Keep intermediate files (e.g. video and audio tracks separate before merge) by passing `-k`:
  ```bash
  indir -k "https://www.youtube.com/watch?v=..."
  ```

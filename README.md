# recompress

*version 2025.04*<img src="icon.svg" width="128" align="right" alt="An icon featuring a woodworking clamp">

A utility for recompressing video files to x265 (HEVC) 10-bit format with optimized multi-core encoding.

## Overview

`recompress` automatically detects system resources and optimizes encoding settings for the best balance of quality and performance. It intelligently preserves all streams from the original file, including audio, subtitles, chapters, and metadata.

Key features:
- Automatic detection and utilization of all available CPU cores
- High-quality x265 (HEVC) 10-bit encoding with customizable quality settings
- Automatic resolution scaling for videos exceeding specified dimensions
- Preservation of all streams (audio, subtitles, chapters, metadata, etc.)
- Smart detection of already-encoded HEVC files to avoid re-encoding

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/EvanEdwards/recompress.git
   ```

2. Make the script executable:
   ```bash
   chmod +x recompress
   ```

3. Optionally, install to your PATH:
   ```bash
   sudo ln -s $(pwd)/recompress /usr/local/bin/recompress
   ```

4. Install the manpage (optional):
   ```bash
   recompress -M
   ```

## Requirements

- ffmpeg (with libx265 support)
- ffprobe
- pandoc (for help pages only)
- h2 utility (for formatted output)

## Basic Usage

Recompress a single video file:
```bash
recompress video.mp4
```

Recompress multiple video files:
```bash
recompress video1.mp4 video2.mp4 video3.mp4
```

Force recompression of already HEVC encoded files:
```bash
recompress -f video.mp4
```

By default, processed files are saved to the "_recompressed" directory in the current working directory.

## Options

| Option | Description |
|--------|-------------|
| `-f, --force` | Force encoding even if the file is already in HEVC format |
| `-q, --quality VALUE` | Set the CRF quality value (18-35, lower is higher quality). Default is 26 |
| `-s, --speed PRESET` | Set the encoding speed preset. Options include: ultrafast, superfast, veryfast, faster, fast, medium, slow, slower, veryslow. Default is "slower" |
| `-x, --width WIDTH` | Set the maximum width for output videos. Videos wider than this will be scaled down while preserving aspect ratio. Default is 1920 |
| `-y, --height HEIGHT` | Set the maximum height for output videos. Videos taller than this will be scaled down while preserving aspect ratio. Default is 1080 |
| `-h, --help` | Display help information |
| `-M, --installmanpage` | Install the manpage to your local user manpage directory |
| `--, --` | Signal the end of options; treat all subsequent arguments as files |

## Examples

Set custom quality (lower values = higher quality) and speed preset:
```bash
recompress -q 22 -s medium video.mp4
```

Limit resolution to 720p:
```bash
recompress -x 1280 -y 720 video.mp4
```

## Notes

- The script automatically utilizes all available CPU cores for encoding
- Audio, chapters, subtitles, and other streams are preserved in the output file
- Videos exceeding the maximum resolution (default 1920x1080) are scaled down while preserving aspect ratio
- The script skips files that are already in HEVC format unless -f/--force is used

## License

MIT License

Copyright (c) 2025 Evan A. Edwards (@EvanEdwards)

## See Also

For more details, see the manpage:
```bash
man recompress  # If installed via -M
```

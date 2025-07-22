# Subtitle Service for Raspberry Pi

This project provides two fast, efficient ways to generate subtitles from video files on a Raspberry Pi. Both methods are optimized for performance and ease of use.

---

## 1. auto-subtitle-plus (Whisper-based)

A powerful tool that uses OpenAI's Whisper for transcription and FFmpeg for audio extraction.

**Why it's great for Raspberry Pi:**
- Supports GPU acceleration (if available) for faster processing
- Can generate `.srt` files or overlay subtitles directly onto video
- Offers language forcing, parallel audio extraction, and consistency enhancements

### Installation
```bash
pip install git+https://github.com/Sectumsempra82/auto-subtitle-plus.git
sudo apt install ffmpeg
```

### Usage Example
Generate subtitles:
```bash
auto_subtitle_plus video.mp4 --output-srt --model medium
```

Embed subtitles directly into the video:
```bash
auto_subtitle_plus video.mp4 --output-video
```

For more details, see the [auto-subtitle-plus GitHub](https://github.com/Sectumsempra82/auto-subtitle-plus).

---

## 2. whisper.cpp with tiny.en Quantized Model

[whisper.cpp](https://github.com/ggerganov/whisper.cpp) is a pure C++ port of OpenAI’s Whisper, optimized for CPU. Using the smallest English-only model delivers the fastest throughput.

### Installation & Build
```bash
git clone https://github.com/ggerganov/whisper.cpp.git
cd whisper.cpp && make
```

Download the tiny English model:
```bash
wget https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml-tiny.en.bin
```

### Extract Audio and Transcribe
```bash
ffmpeg -i input.mp4 -ar 16000 -ac 1 -f wav audio.wav
./main -m ggml-tiny.en.bin -f audio.wav --output-srt subtitles.srt
```

### Expected Speed
- **On a Pi 4:** ~0.5× real time
- **On a Pi 5:** ~1× real time

---

## References
- [auto-subtitle-plus GitHub](https://github.com/Sectumsempra82/auto-subtitle-plus)
- [whisper.cpp GitHub](https://github.com/ggerganov/whisper.cpp)
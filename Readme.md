https://github.com/Sirozha1337/faster-auto-subtitle

1. auto-subtitle-plus (Whisper-based)
A powerful tool that uses OpenAI's Whisper for transcription and FFmpeg for audio extraction.

Why it's great for Raspberry Pi:

Supports GPU acceleration (if available) for faster processing

Can generate .srt files or overlay subtitles directly onto video

Offers language forcing, parallel audio extraction, and consistency enhancements

Install:

bash
pip install git+https://github.com/Sectumsempra82/auto-subtitle-plus.git
sudo apt install ffmpeg
Usage example:

bash
auto_subtitle_plus video.mp4 --output-srt --model medium
You can also embed subtitles directly into the video:

bash
auto_subtitle_plus video.mp4 --output-video
More details on auto-subtitle-plus GitHub


1. whisper.cpp with tiny.en quantized model
whisper.cpp is a pure C++ port of OpenAI’s Whisper optimized for CPU. Using the smallest English-only model delivers the fastest throughput.

Install and build

git clone https://github.com/ggerganov/whisper.cpp.git

cd whisper.cpp && make

Download tiny English model

bash
wget https://huggingface.co/ggerganov/whisper.cpp/resolve/main/models/ggml-tiny.en.bin
Extract audio and transcribe

bash
ffmpeg -i input.mp4 -ar 16000 -ac 1 -f wav audio.wav
./main -m ggml-tiny.en.bin -f audio.wav --output-srt subtitles.srt
Expected speed

On a Pi 4: ~0.5× real time

On a Pi 5: ~1× real time
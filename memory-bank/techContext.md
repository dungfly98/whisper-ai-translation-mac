# Technical Context: Free Local Audio Translation Stack

## Core Technology Stack

### Audio Capture
- **BlackHole**: Open-source virtual audio driver for macOS
  - Purpose: Capture system audio (Zoom/Meet output)
  - Setup: Multi-Output Device configuration
- **sounddevice/pyaudio**: Python libraries for audio I/O
  - Purpose: Record from microphone and BlackHole simultaneously

### Speech Recognition
- **Whisper.cpp**: Native C++ implementation of OpenAI Whisper
  - Advantages: Optimized for Apple Silicon (M1/M2/M3)
  - Performance: Much faster than Python Whisper
  - Models: Use 'base' or 'small' for real-time performance
  - Memory: Efficient on 16GB RAM

### Translation
- **MarianMT (Helsinki-NLP)**: Open-source neural machine translation
  - Models: opus-mt-en-vi (English→Vietnamese), opus-mt-vi-en (Vietnamese→English)
  - Library: HuggingFace transformers
  - Trade-off: Lower quality than cloud services but completely free

### UI Framework
- **Tkinter**: Built-in Python GUI library
- **Alternative**: PyQt6 for more modern interface

## System Requirements
- **OS**: macOS (tested on Apple Silicon)
- **RAM**: 16GB (sufficient for models + processing)
- **Python**: 3.8+ with pip
- **Disk**: ~2GB for models

## Development Environment
- **Primary Language**: Python 3.x
- **Audio Processing**: Real-time buffering (1-2 second chunks)
- **Threading**: Async processing for multiple audio streams
- **Model Loading**: One-time initialization to minimize latency

## Performance Expectations
- **STT Latency**: ~500ms-1s with Whisper.cpp base model
- **Translation Latency**: ~200-500ms with MarianMT
- **Total Delay**: ~1-2 seconds end-to-end
- **Memory Usage**: ~4-6GB total (models + processing)

## Limitations of Free Stack
- Translation quality lower than Google Translate
- No context awareness across sentences
- Limited handling of idioms/slang
- No built-in spell correction 
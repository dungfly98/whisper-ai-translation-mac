# Project Brief: Whisper AI Real-time Translator

## Project Goal
Build a real-time audio translation software that runs locally on macOS (MacBook M3) to translate English to Vietnamese and vice versa.

## Core Requirements
- **Platform**: macOS (MacBook M3 - 16GB RAM)
- **Cost**: Completely free solution
- **Privacy**: Runs entirely local (no cloud services)
- **Audio Sources**: 
  - System audio (from Zoom/Meet/videos) - English → Vietnamese
  - Microphone input (user speech) - Vietnamese → English
- **Real-time**: Live translation with minimal delay

## Technical Constraints
- No paid APIs or cloud services
- Must work with headphones during video calls
- All processing must be local
- Python-based solution preferred

## Success Criteria
- Can capture both system audio and microphone simultaneously
- Provides real-time speech-to-text using Whisper
- Translates between English and Vietnamese
- Shows results in a simple UI
- Works during Zoom/Google Meet calls with headphones

## Non-Goals (for now)
- Perfect translation quality (acceptable trade-off for free solution)
- Multi-language support beyond English/Vietnamese
- Advanced UI/UX features
- Text-to-speech output 
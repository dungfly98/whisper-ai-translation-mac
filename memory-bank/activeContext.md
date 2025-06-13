# Active Context: Implementation Roadmap

## Current Phase: Setup & Foundation
Starting with completely free, local solution as requested by user.

## Implementation Steps (Priority Order)

### Phase 1: Audio Infrastructure (Current Focus)
1. **Install BlackHole** - Virtual audio driver
2. **Configure Multi-Output Device** - Route system audio to both speakers and capture
3. **Test audio capture** - Verify both microphone and system audio work
4. **Python audio libraries** - Install and test sounddevice/pyaudio

### Phase 2: Speech Recognition Setup
1. **Install Whisper.cpp** - Native implementation for Apple Silicon
2. **Download models** - Base/small models for optimal speed
3. **Test STT pipeline** - Verify real-time speech recognition
4. **Optimize buffer sizes** - Find sweet spot for latency vs accuracy

### Phase 3: Translation Integration
1. **Install HuggingFace transformers** - For MarianMT models
2. **Download translation models** - EN→VI and VI→EN
3. **Test translation pipeline** - Verify model outputs
4. **Optimize model loading** - Pre-load to reduce latency

### Phase 4: Application Integration
1. **Create basic UI** - Tkinter interface for displaying translations
2. **Implement dual audio streams** - Parallel processing of mic + system audio
3. **Connect all pipelines** - STT → Translation → Display
4. **Test end-to-end** - Full workflow with real audio sources

### Phase 5: Optimization & Polish
1. **Performance tuning** - Reduce latency where possible
2. **Error handling** - Graceful failures and recovery
3. **User experience** - Clear indicators of what's being translated
4. **Documentation** - Setup instructions and troubleshooting

## Next Immediate Actions
- Start with BlackHole installation and configuration
- Test basic audio capture before moving to ML components
- Focus on getting foundation right before adding complexity

## Key Decisions Made
- Prioritizing completely free solution over translation quality
- Using Whisper.cpp over Python Whisper for performance
- Starting with Tkinter for simplicity
- Accepting 1-2 second latency as reasonable for free solution

## User Preferences Noted
- Wants everything free and local
- Has MacBook M3 with 16GB RAM
- Needs to work with headphones during video calls
- Prefers to start simple and build up 
# Whisper AI Real-time Translator

A completely free, local real-time audio translation software for macOS that translates between English and Vietnamese. Captures both system audio (from Zoom/Meet/videos) and microphone input simultaneously.

## 🎯 Features

- **Real-time Translation**: English ↔ Vietnamese with ~1-2 second delay
- **Dual Audio Capture**: System audio + Microphone simultaneously
- **100% Free & Local**: No cloud services, no API costs, complete privacy
- **Works with Headphones**: Compatible with video calls (Zoom, Google Meet)
- **Apple Silicon Optimized**: Built for MacBook M1/M2/M3 performance

## 🔧 System Requirements

- **OS**: macOS (Apple Silicon recommended)
- **RAM**: 8GB minimum, 16GB recommended
- **Disk**: ~2GB for models
- **Python**: 3.8+
- **Internet**: Only for initial setup (downloading models)

## 📦 Installation

### Step 1: Install BlackHole (Audio Driver)
```bash
# Install virtual audio driver
brew install blackhole-2ch

# ⚠️ IMPORTANT: Reboot your MacBook after installation
sudo reboot
```

### Step 2: Install Python Dependencies
```bash
# Install audio libraries
pip install sounddevice pyaudio numpy

# If pyaudio fails, install PortAudio first:
brew install portaudio
pip install pyaudio
```

### Step 3: Install Whisper.cpp (Speech Recognition)
```bash
# Clone and build Whisper.cpp
git clone https://github.com/ggerganov/whisper.cpp.git
cd whisper.cpp
make

# Download speech recognition model
bash ./models/download-ggml-model.sh base

# Test installation
./main -m models/ggml-base.bin -f samples/jfk.wav
```

### Step 4: Install Translation Models
```bash
# Return to project directory
cd /Users/$(whoami)/Desktop/Workspace/whisper-ai

# Install HuggingFace transformers
pip install transformers torch sentencepiece protobuf

# Test model download
python -c "
from transformers import MarianMTModel, MarianTokenizer
print('Downloading English → Vietnamese model...')
MarianMTModel.from_pretrained('Helsinki-NLP/opus-mt-en-vi')
print('Downloading Vietnamese → English model...')
MarianMTModel.from_pretrained('Helsinki-NLP/opus-mt-vi-en')
print('✅ All models downloaded successfully!')
"
```

### Step 5: Project Setup
```bash
# Create project structure
mkdir -p src models tests
pip install -r requirements.txt
```

## ⚙️ Audio Configuration

### Configure Multi-Output Device (for System Audio Capture)

1. **Open Audio MIDI Setup** (Applications → Utilities → Audio MIDI Setup)
2. **Create Multi-Output Device**:
   - Click "+" → "Create Multi-Output Device"
   - Check both "BlackHole 2ch" and your speakers/headphones
   - Right-click → "Use This Device For Sound Output"
3. **Set as Default Output** in System Preferences → Sound

### Verify Audio Setup
```bash
# List available audio devices
python -c "
import sounddevice as sd
print('Available audio devices:')
print(sd.query_devices())
"
```

## 🚀 Usage

### Basic Usage
```bash
# Run the translator
python src/main.py
```

### During Video Calls
1. Set "Multi-Output Device" as default audio output
2. Join your Zoom/Meet call normally with headphones
3. Run the translator - it will capture both:
   - System audio (other participants) → Translate to Vietnamese
   - Your microphone → Translate to English

## 📁 Project Structure

```
whisper-ai/
├── README.md
├── requirements.txt
├── memory-bank/           # Project documentation
│   ├── projectbrief.md
│   ├── techContext.md
│   └── activeContext.md
├── src/
│   ├── main.py           # Main application
│   ├── audio_capture.py  # Audio recording logic
│   ├── translation.py    # Translation pipeline
│   └── ui.py            # User interface
├── models/              # Downloaded AI models
├── tests/               # Test files
└── whisper.cpp/         # Whisper.cpp installation
```

## 🔄 How It Works

```
┌─────────────┐    ┌─────────────┐
│ Microphone  │    │System Audio │
│(Your Voice) │    │(Others/Apps)│
└──────┬──────┘    └──────┬──────┘
       │                  │
       ▼                  ▼
┌─────────────────────────────────┐
│        Whisper.cpp STT          │
│   (Speech-to-Text Engine)       │
└──────┬──────────────────┬───────┘
       │                  │
       ▼                  ▼
┌─────────────┐    ┌─────────────┐
│Vietnamese   │    │English      │
│→ English    │    │→ Vietnamese │
│(MarianMT)   │    │(MarianMT)   │
└──────┬──────┘    └──────┬──────┘
       │                  │
       └──────┬───────────┘
              ▼
      ┌─────────────┐
      │     UI      │
      │  Display    │
      └─────────────┘
```

## ⚡ Performance Tips

- **Use 'base' model** for balanced speed/accuracy
- **Use 'small' model** for maximum speed
- **Close other apps** to free up RAM during translation
- **Adjust buffer size** in code for lower latency

## 🐛 Troubleshooting

### Audio Issues
- **No system audio captured**: Verify BlackHole installation and Multi-Output Device setup
- **Permission denied**: Check microphone permissions in System Preferences → Security & Privacy

### Model Issues
- **Models not found**: Re-run the model download commands
- **Out of memory**: Try smaller Whisper model ('small' instead of 'base')

### Performance Issues
- **High latency**: Reduce audio buffer size or use smaller models
- **CPU overload**: Close other applications, ensure adequate cooling

## 📊 Model Sizes & Performance

| Whisper Model | Size | Speed | Accuracy | Memory |
|---------------|------|-------|----------|---------|
| tiny          | 39MB | Fastest | Good | 1GB |
| base          | 142MB | Fast | Better | 2GB |
| small         | 244MB | Medium | Best | 3GB |

## 🔐 Privacy & Security

- **100% Local Processing**: No data sent to cloud services
- **No Network Access**: Works completely offline after setup
- **Open Source**: All components are open source and auditable

## 🤝 Contributing

This is a learning project. Feel free to:
- Report issues
- Suggest improvements
- Submit pull requests
- Share your experience

## 📝 License

This project uses multiple open-source components:
- **Whisper.cpp**: MIT License
- **MarianMT**: MIT License  
- **BlackHole**: GPL-3.0 License

## ⚠️ Limitations

- **Translation Quality**: Lower than commercial services (Google Translate)
- **Context Awareness**: Limited cross-sentence context
- **Language Support**: Only English ↔ Vietnamese
- **Latency**: 1-2 second delay is normal for free solution

## 🆘 Support

For issues:
1. Check troubleshooting section above
2. Verify all installation steps completed
3. Test each component individually
4. Check system requirements

---

**Made with ❤️ for the Vietnamese developer community** 
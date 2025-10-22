# VLC Integration with Auto-Subtitle Tool - Discussion Summary

## Project Overview
- **Tool**: Auto-subtitle tool using OpenAI Whisper for video transcription
- **Goal**: Integrate subtitle generation with VLC video player
- **Location**: `/Users/akpmohan/Documents/Workspace/tools/auto-subtitle/`

## Current Setup Status
✅ **Completed**:
- Auto-subtitle tool is working
- Virtual environment activated: `subtitle_env/`
- Dependencies installed: `openai-whisper`, `ffmpeg-python`
- FFmpeg binary installed via Homebrew

## Key Commands Learned

### Basic Usage
```bash
# Activate environment
source /Users/akpmohan/Documents/Workspace/tools/auto-subtitle/subtitle_env/bin/activate

# Generate subtitles without burning into video (VLC-friendly)
auto_subtitle /path/to/video.mp4 -o /path/to/output_dir --srt_only true

# Generate both video with burned subtitles AND separate SRT file
auto_subtitle /path/to/video.mp4 -o /path/to/output_dir --output_srt true

# Use larger model for better accuracy
auto_subtitle /path/to/video.mp4 --model medium -o /path/to/output_dir

# Translate non-English to English
auto_subtitle /path/to/video.mp4 --task translate -o /path/to/output_dir
```

### Available Models
- `tiny`, `tiny.en` - Fastest, ~1GB VRAM
- `base`, `base.en` - Good balance, ~1GB VRAM  
- `small`, `small.en` - Better accuracy, ~2GB VRAM
- `medium`, `medium.en` - High accuracy, ~5GB VRAM
- `large` - Best accuracy, ~10GB VRAM
- `turbo` - Optimized large model, ~6GB VRAM, ~8x faster

## VLC Integration Options Discussed

### 1. **VLC Extensions** (Recommended)
- **Type**: Lua-based scripts
- **Pros**: Lightweight, built into VLC, easy distribution
- **Cons**: Limited functionality
- **Use Case**: Simple subtitle generation trigger

### 2. **VLC Addons**
- **Type**: External applications with VLC integration
- **Pros**: More powerful, advanced features
- **Cons**: Heavier, separate installation
- **Use Case**: Complex functionality, GUI integration

### 3. **Direct Integration**
- **Type**: Python scripts using VLC Python bindings
- **Pros**: Full control, real-time integration
- **Cons**: More complex development
- **Use Case**: Custom applications

## Real-Time Limitations
❌ **Not Possible**: Real-time subtitle generation with current tool
- Whisper models are designed for batch processing
- Audio extraction + transcription takes time
- Processing happens after entire audio is extracted

## Next Steps for VLC Integration

### Immediate Options:
1. **Manual Workflow**: Generate SRT files, load in VLC manually
2. **VLC Extension**: Create Lua script to trigger auto-subtitle tool
3. **Batch Processing**: Process multiple videos for VLC library

### Development Path:
1. **Start Simple**: VLC Extension calling existing auto-subtitle tool
2. **Enhance**: Add GUI, batch processing, automatic subtitle loading
3. **Advanced**: Real-time alternatives using streaming speech recognition

## Technical Notes
- **SRT Format**: VLC natively supports SRT subtitle files
- **File Naming**: VLC auto-loads subtitles if SRT has same name as video
- **Whisper API**: Can be used directly via Python for custom integration
- **Performance**: First run downloads model (~100MB-3GB depending on model)

## Resources
- [OpenAI Whisper GitHub](https://github.com/openai/whisper#)
- Current tool: `auto_subtitle/cli.py`
- Requirements: `requirements.txt` (currently: `openai-whisper`)

## Files Modified
- `requirements.txt` - Added `ffmpeg-python` dependency

---
*Generated: $(date)*
*Status: Ready for VLC integration development*

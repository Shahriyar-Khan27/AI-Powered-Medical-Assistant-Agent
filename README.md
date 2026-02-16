# AI-Powered Medical Assistant

An AI-powered medical assistant that analyzes medical images using voice interaction. Patients describe their symptoms via voice, the AI examines uploaded medical images using a multimodal LLM, and responds with a spoken diagnosis.

## How It Works

```
Patient speaks       -->  Speech-to-Text (Whisper)  -->  Text query
                                                            |
Medical image        -->  Image encoding (base64)   --------+
                                                            |
                                                     Groq Vision LLM
                                                            |
                                                     Doctor's response
                                                            |
                                                     Text-to-Speech (ElevenLabs / gTTS)
                                                            |
                                                     Audio playback
```

## Project Structure

```
AI-Powered-Medical-Assistant/
├── src/
│   ├── __init__.py
│   ├── brain.py              # Image analysis with Groq multimodal LLM
│   ├── stt.py                # Speech-to-Text (mic recording + Whisper)
│   ├── tts.py                # Text-to-Speech (gTTS + ElevenLabs)
│   └── app.py                # Gradio web UI entry point
│
├── assets/
│   └── samples/
│       ├── images/            # Sample medical images for testing
│       └── audio/             # Sample audio files for testing
│
├── output/                    # Generated audio responses
├── .env.example               # API key template
├── .gitignore
├── requirements.txt
├── Pipfile
├── Pipfile.lock
└── README.md
```

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Vision LLM | Groq (Llama 4 Scout) |
| Speech-to-Text | Groq Whisper Large V3 |
| Text-to-Speech | ElevenLabs / gTTS |
| Web UI | Gradio |
| Audio Processing | FFmpeg, PortAudio, PyAudio |

## Prerequisites

- Python 3.10+
- [Groq API Key](https://console.groq.com/)
- [ElevenLabs API Key](https://elevenlabs.io/) (optional, gTTS works as fallback)
- FFmpeg and PortAudio installed on your system

### Installing FFmpeg & PortAudio

<details>
<summary><strong>macOS</strong></summary>

```bash
brew install ffmpeg portaudio
```
</details>

<details>
<summary><strong>Linux (Debian/Ubuntu)</strong></summary>

```bash
sudo apt update
sudo apt install ffmpeg portaudio19-dev
```
</details>

<details>
<summary><strong>Windows</strong></summary>

**FFmpeg:**
1. Download from [FFmpeg Downloads](https://ffmpeg.org/download.html)
2. Extract to a folder (e.g., `C:\ffmpeg`)
3. Add `C:\ffmpeg\bin` to your system PATH

**PortAudio:**
1. Download from [PortAudio Downloads](http://www.portaudio.com/download.html)
2. Follow the installation instructions on the website
</details>

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Shahriyar-Khan27/AI-Powered-Medical-Assistant-.git
cd AI-Powered-Medical-Assistant-
```

### 2. Set up environment variables

```bash
cp .env.example .env
```

Edit `.env` and add your API keys:

```
GROQ_API_KEY=your_groq_api_key_here
ELEVEN_API_KEY=your_elevenlabs_api_key_here
```

### 3. Install dependencies

**Using pip:**
```bash
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows
pip install -r requirements.txt
```

**Using Pipenv:**
```bash
pip install pipenv
pipenv install
pipenv shell
```

**Using Conda:**
```bash
conda create --name medical-ai python=3.11
conda activate medical-ai
pip install -r requirements.txt
```

### 4. Run the application

```bash
python src/app.py
```

Open [http://127.0.0.1:7860](http://127.0.0.1:7860) in your browser.

## Usage

1. Click the microphone button and describe your symptoms
2. Upload a medical image (skin condition, rash, etc.)
3. Click **Submit**
4. The AI doctor will analyze the image, and you'll receive:
   - Your transcribed speech
   - A text diagnosis
   - A spoken audio response

## Architecture

The project is built in 4 modular phases:

| Phase | Module | Description |
|-------|--------|-------------|
| 1 | `src/brain.py` | Encodes images and queries the Groq vision model for medical analysis |
| 2 | `src/stt.py` | Records audio from the microphone and transcribes it using Whisper |
| 3 | `src/tts.py` | Converts the doctor's text response into speech with autoplay |
| 4 | `src/app.py` | Ties everything together in a Gradio web interface |

## License

This project is for **educational purposes only**. It is not intended to provide real medical advice.

## Contact & Support

- **Author**: Shahriyar Khan
- **GitHub**: [@Shahriyar-Khan27](https://github.com/Shahriyar-Khan27)
- **Issues**: [Open an issue](https://github.com/Shahriyar-Khan27/AI-Powered-Medical-Assistant-Agent/issues)

If you find this project helpful, please give it a star on GitHub!

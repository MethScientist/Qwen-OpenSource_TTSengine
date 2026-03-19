# Qwen-OpenSource_TTSengine
This is a TTS engine for the qwen model that come out recently. 

# Custom TTS Engine

This project is a Python-based Text-to-Speech (TTS) engine using Qwen models. It converts text into high-quality speech and supports real-time streaming. The engine can be accessed via an API, allowing users or bots to generate speech dynamically.

## Features

- Convert text to speech with customizable voice parameters.
- Stream audio in chunks for faster playback.
- Users can select model, device, dtype, speaker, and voice instructions.
- Works locally, in Colab, or via a public API endpoint.
 
## API Usage Example (Python Client)
import requests
import numpy as np
import soundfile as sf

response = requests.get(
    "http://localhost:8000/tts",
    params={"text": "Hello world", "speaker": "Ryan"},
    stream=True
)

pcm_data = b""
for chunk in response.iter_content(4096):
    pcm_data += chunk

audio = np.frombuffer(pcm_data, dtype=np.int16).astype(np.float32)/32767
sf.write("output.wav", audio, 24000)

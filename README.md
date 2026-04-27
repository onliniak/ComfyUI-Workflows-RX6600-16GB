# ComfyUI-Workflows-RX6600-16GB

Przypięte:
- Jeśli chodzi o LTX 2.3 to mogę polecić: https://civitai.com/models/2339823/ltx23-gguf-low-vram-video-generation-i2v-t2v (129 klatek 720p w 1.5 godziny)
- Przeciętny czas generowania 480p to 15-20 minut na każde 16 klatek (1 sekunda).
    - 7+7 kroków w wersji FSampler i 4+4 kroki w wersji lightx2
    - Plik stronicowania na dysku SSD SATA
- 832x480 polecam ograniczyć do 33 klatek, a 1280x720 do 17 klatek.
- Jedynie pierwszy klip powinien mieć shift na wysokim modelu i noise na niskim modelu. Kolejne muszą mieć noise_seed fixed 0.

Instalacja:
1. Zainstaluj https://pinokio.co/
2. Wybierz oficjalny pakiet instalacyjny dla ComfyUI (https://github.com/pinokiofactory/comfy).
3. Przełącz się na zakładkę dev i wybierz terminal python/conda ze środowiskiem venv (czy jakoś tak).
4. pip uninstall torch torchaudio torchvision torch-directml
5. pip install --pre torch torchaudio torchvision rocm[devel] --index-url https://rocm.nightlies.amd.com/v2-staging/gfx103X-dgpu/
6. pip install triton-windows
7. Jeśli przy starcie ComfyUI pisze 
    ```
    AMD arch: gfx1032
    ROCm version: (7, 2)
    Set vram state to: NORMAL_VRAM
    Device: cuda:0 AMD Radeon RX 6600 XT : native
    ``` 
    To jest dobrze.

Co nie działa ?

- Zaawansowane rozszerzenia jak SeedVR2
  - Zwłaszcza takie, które zależą od Flash Attention, Sage Attention i innych attention
  - Ta wersja działa **bez** instalowania sterowników PRO (stąd 10 GB więcej pobranych plików)
- Modele z iq w nazwie

Potrzebne rozszerzenia:
- Wymagane
   - GGUF autorstwa GGUF-ORG https://github.com/calcuis/gguf (wymagane do uruchomienia plików .gguf i pig*.gguf)
- Opcjonalne:
  - https://github.com/onliniak/ComfyUI-SaveAndLoadPromptCondition (opcjonalnie, możesz zastąpić zwykłym load clip)
  - https://github.com/obisin/ComfyUI-FSampler (alternatywnie udostępniłem wersję Lightx2 bez bong_tangent_2)

Potrzebne modele:
  - Text To Image:
    - Z-Image Turbo: https://huggingface.co/gguf-org/z-image-gguf
    - Flux Klein 9B Distill:
      - Unet: https://huggingface.co/unsloth/FLUX.2-klein-9B-GGUF
      - VAE: https://huggingface.co/dummy9996/FLUX.2-small-decoder-bf16/blob/main/small_decoder-comfyui-bf16.safetensors
      - Text Encoder: https://huggingface.co/Comfy-Org/vae-text-encorder-for-flux-klein-9b/blob/main/split_files/text_encoders/qwen_3_8b_fp8mixed.safetensors
  - Image To Video:
    - WAN 2.2: https://huggingface.co/calcuis/wan2-gguf
      - LoRA: https://huggingface.co/jayn7/WAN2.2-I2V_A14B-DISTILL-LIGHTX2V-4STEP-GGUF

Opcjonalne:
  - https://huggingface.co/fofr/comfyui/tree/main/upscale_models
  - https://github.com/kijai/ComfyUI-MMAudio (Video To Sound)
  - ACE Step 1.5 (Text to Music)

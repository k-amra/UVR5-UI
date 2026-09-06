<h1 align="center"><b> 🎵 UVR5 UI 🎵 </b></h1>
<div align="center">

[![madewithlove](https://img.shields.io/badge/made_with-%E2%9D%A4-red?style=for-the-badge&labelColor=orange)](https://github.com/Eddycrack864/UVR5-UI)

![cutecounter](https://count.nett.moe/get/uvr5_ui_colab/img?theme=rule34)

[![Open In Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/github/Eddycrack864/UVR5-UI/blob/main/UVR_UI.ipynb)
[![Open In Kaggle](https://img.shields.io/badge/Kaggle-20BEFF?style=for-the-badge&logo=Kaggle&logoColor=white)](https://www.kaggle.com/code/eddycrack864/uvr5-ui)
<a target="_blank" href="https://lightning.ai/new?repo_url=https%3A%2F%2Fgithub.com%2FEddycrack864%2FUVR5-UI%2Fblob%2Fmain%2FUVR_UI.ipynb">
<img src="https://pl-bolts-doc-images.s3.us-east-2.amazonaws.com/app-2/studio-badge.svg" alt="Open in Studio"/></a>
[![Licence](https://img.shields.io/badge/LICENSE-MIT-green.svg?style=for-the-badge)](https://github.com/Eddycrack864/UVR5-UI/blob/main/LICENSE)
[![Discord](https://img.shields.io/badge/Community-Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/aihub)

This project is based on [python-audio-separator](https://github.com/karaokenerds/python-audio-separator) (a CLI version of UVR5). This project was originally created for the [AI ​​HUB](https://discord.gg/aihub) community.

</div>
<div align="center">
  
[![Hugging Face](https://huggingface.co/datasets/huggingface/badges/resolve/main/open-in-hf-spaces-xl-dark.svg?download=true)](https://huggingface.co/spaces/TheStinger/UVR5_UI)

You can also try it on HuggingFace Spaces running with Zero GPU (A100)!

</div>
 
<div align="center">

**[Docs](https://github.com/Eddycrack864/UVR5-UI/blob/main/info/docs.md) / [Troubleshooting](https://github.com/Eddycrack864/UVR5-UI/blob/main/info/troubleshooting.md)**

</div>

## Features: 
* User Friendly Interface
* All VR Arch Models
* All MDX-NET Models
* Demucs v4 Models
* MDX23C Models
* Mel-Band Roformer Models
* BS Roformer Models
* Music Source Separation Models
* VIP Models
* Separation of an audio/video from all sites supported by [yt_dlp](https://github.com/yt-dlp/yt-dlp). Check the complete list [here](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md).
* Batch Separation
* Available in multiple languages
* Colab/Kaggle/Lightning.ai support
* Windows/Linux support

## Changes in this fork

This repository is a fork of [Eddycrack864/UVR5-UI](https://github.com/Eddycrack864/UVR5-UI) with the following changes on top of upstream. Check the upstream repo for the latest base changes and official support.

### Extra models
* **BS Roformer | HyperACE V2 Voc by pcunwa** — uses a SegmModel-based mask estimator that stock audio-separator cannot load. A vendored implementation ships in `assets/bs_roformer_hyperace/` and is selected automatically via the model config's `arch` flag (or "hyperace" in the checkpoint name).
* **MelBand Roformer | Deux by becruily** (dual vocals/instrumental)
* **BS Roformer | LEAP-XE Voc by unwa**
* **MelBand Roformer | Bleed Suppressor V1 by unwa-97chris** (download URLs added)

### Auto-download for fork-added models
Models added by this fork are not in audio-separator's own download registry, so on a clean install they failed with "not found in supported model files" even after a manual download. The UI now downloads the model and its config from `assets/models.json` before separation and registers them with audio-separator, so first use works out of the box.

### Fixed audio streaming of separated stems
The pinned gradio/starlette stack has two off-by-one bugs in ranged HTTP file responses that break or hang audio playback of results ("h11 ... Content-Length" errors). This fork patches both and asserts the pinned versions (gradio 5.27.1 / starlette 0.47.3). Starting with different versions fails loudly with instructions; the check can be bypassed with `UVR_SKIP_PATCH_VERSION_CHECK=1`.

### Robustness fixes
* Batch separation loads the model once per batch instead of per file, continues after a failed file (with a per-file error report), and no longer shares global state between concurrent runs
* The updater scripts back up and restore `assets/config.json`, so updates no longer wipe language, theme and Discord Rich Presence settings
* Leaderboard validates the filter selection and HTML-escapes its output
* yt-dlp downloads use collision-safe output names; wget/curl model downloads get timeouts, retries and partial-file cleanup
* `sage_attention` configs fail with a clear error instead of a `NameError` (not supported in the vendored HyperACE build)
* Misc: Discord Rich Presence starts only when the app actually runs, single-stem None guard, i18n fixes (de_DE, ar_AR, `fr-FR.json` renamed to `fr_FR.json`), i18n scanner compatible with Python 3.12+, Kaggle notebook file-tunnel fix

## Requirements

### Hardware Requirements:
* Nvidia Series 2000 (RTX) or higher.
* At least 10Gb of disk space. 

> [!NOTE]  
> Older NVIDIA GPUs will be very slow. CPU will be insanely slow. If you don't meet the hardware requirements use our [Colab](https://colab.research.google.com/github/Eddycrack864/UVR5-UI/blob/main/UVR_UI.ipynb)/[Kaggle](https://www.kaggle.com/code/eddycrack864/uvr5-ui)/[Lightning.ai](https://lightning.ai/eddycrack864/studios/uvr5-ui)/[Hugging Face](https://huggingface.co/spaces/TheStinger/UVR5_UI).

### Prerequisites:
- Git. You can download Git [here](https://git-scm.com/downloads).
- FFmpeg. You can download FFmpeg [here](https://www.ffmpeg.org/download.html) or you can use my [automated installation script](https://github.com/Eddycrack864/UVR5-UI/blob/main/info/ffmpeg-installer.bat) (for Windows).
- For linux users, run this command on an terminal: (Debian and Ubuntu users): `sudo apt install ffmpeg git` (For Arch linux users): `sudo pacman -S ffmpeg git` (For Fedora users): `sudo dnf install ffmpeg git`
(Some distributions already come with Git and FFmpeg preinstalled so this step may be optional.)

> [!IMPORTANT]  
> FFmpeg has to be added to the PATH. (only needed on Windows)

## Getting Started

Clone the repository (git needed) or download the source code of the latest release [here](https://github.com/Eddycrack864/UVR5-UI/releases)

```
git clone https://github.com/Eddycrack864/UVR5-UI.git
```

Then continue with the steps described below

### 1. Installation

Run the installation script based on your operating system:

- **Windows:** Double-click `UVR5-UI-installer.bat` (DONT RUN AS ADMINISTRATOR 🚧).
- **Linux:** Run `UVR5-UI-installer.sh` with `chmod +x UVR5-UI-installer.sh` and `./UVR5-UI-installer.sh`.

### 2. Running UVR5 UI

Start UVR5 UI using:

- **Windows:** Double-click `run-UVR5-UI.bat`.
- **Linux:** Run `run-UVR5-UI.sh` with `chmod +x run-UVR5-UI.sh` and `./run-UVR5-UI.sh`.

### 3. Update UVR5 UI (If you want/need it)

Update UVR5 UI using (git needed):

- **Windows:** Double-click `UVR5-UI-updater.bat`.
- **Linux:** Run `UVR5-UI-updater.sh` with `chmod +x UVR5-UI-updater.sh` and `./UVR5-UI-updater.sh`.

If you find an error when installing or running the program please consult [this troubleshooting file](https://github.com/Eddycrack864/UVR5-UI/blob/main/info/troubleshooting.md) first, if your error is not described there please create an [issue](https://github.com/Eddycrack864/UVR5-UI/issues)

### 4. Debug (If you want/need it)

Check the status of audio-separator core:

- **Windows:** Double-click `status-checker.bat`.
- **Linux:** Run `status-checker.sh` with `chmod +x status-checker.sh` and `./status-checker.sh`.

## Precompiled Version
1. Get the precompiled version (.zip) for your PC:
   - **[Windows](https://huggingface.co/Eddycrack864/UVR5-UI/tree/main/Windows)**
   - **[Linux](https://huggingface.co/Eddycrack864/UVR5-UI/tree/main/Linux)**

2. Extract the .zip file, I recommend using the "extract here" option.
3. You can now use all the features of the normal installation.

> [!NOTE]  
> Still, to update UVR5 UI you need to install Git.

## Docker Instance

A more technical level is required for this type of use. You can use this Jupyter notebook to initialize UVR5 on virtual machines with GPU. This will install the entire UVR5 from the main branch of GitHub.

### Requirements/Recommendations
- Use the docker image `>= ubuntu/ubuntu:20.04`
- At least `20 GB of storage minimum.` (Add more space for your models/training)
- Use Jupyter `>= 7.3.1`
- Configure port forwarding `9999 (UVR5-UI GUI)`
- Install necessary drivers to use the GPU

You can get the notebook here: [Jupyter Notebook](https://github.com/Eddycrack864/UVR5-UI/blob/main/UVR_UI_Jupyter.ipynb) by iroaK


## Contributions
If you want to participate and help me with this project feel free to create an [issue](https://github.com/Eddycrack864/UVR5-UI/issues) if something goes wrong or make a [pull request](https://github.com/Eddycrack864/UVR5-UI/pulls) to improve this project.

Any type of contribution is welcome 💖

If you like this project you can star this repository. I will appreciate a lot 💖💖💖

You can donate to the original UVR5 project here:

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/uvr5)

## TO-DO
* Add more models
* Add more output formats

## Credits
* python-audio-separator by [beveradb](https://github.com/beveradb).
* Special thanks to [Ilaria](https://github.com/TheStingerX) for hosting this space and help 💖
* Thanks to [Mikus](https://github.com/cappuch) for the help with the code.
* Thanks to [Nick088](https://github.com/Nick088Official) for the help to fix roformers.
* Thanks to [yt_dlp](https://github.com/yt-dlp/yt-dlp) devs.
* Separation by link source code and improvements by [NeoDev](https://github.com/TheNeodev).
* Thanks to [ArisDev](https://github.com/aris-py) for porting UVR5 UI to Kaggle and improvements.
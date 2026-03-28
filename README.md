# 🔧 JUL14Ns Audio Mods

<div align="center">

  [![GitHub license](https://img.shields.io/github/license/Gamer92000/JUL14Ns-Audio-Mods.svg)](https://github.com/Gamer92000/JUL14Ns-Audio-Mods/blob/main/LICENSE)
  [![GitHub commits](https://badgen.net/github/commits/Gamer92000/JUL14Ns-Audio-Mods/main)](https://GitHub.com/Gamer92000/JUL14Ns-Audio-Mods/commit/)
  [![Github stars](https://img.shields.io/github/stars/Gamer92000/JUL14Ns-Audio-Mods.svg)](https://GitHub.com/Gamer92000/JUL14Ns-Audio-Mods/stargazers/)
  <br>
  <h3>If you like this project, please consider giving it a star ⭐️!</h3>
</div>

## 📖 Description

*JUL14Ns Audio Mods* is a plugin for TeamSpeak 3 that adds a few features to the audio system.
It allows you to filter background noise using the [RNNoise](https://jmvalin.ca/demo/rnnoise/) library, adds a configurable voice activation detection, and a compressor that does not lift noise to infinity.

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📦 3rd Party Libraries

This plugin uses the [Qt](https://www.qt.io/) framework and the [RNNoise](https://jmvalin.ca/demo/rnnoise/) library.

## 🧠 RNNoise integration notes

- RNNoise denoising is called in `src/plugin.cpp` via `rnnoise_process_frame(...)`.
- The current build links directly against sources inside `3rdParty/rnnoise/src`, including `rnn_data.c` (the embedded model payload).
- Per-channel RNNoise state is managed with `FixedSizeMap<int, DenoiseState*>` so each audio channel has its own denoiser state.

## 🔄 Sync RNNoise model from upstream (`xiph/rnnoise`)

This repository tracks RNNoise as a submodule at `3rdParty/rnnoise`. To update to the newest upstream model/code:

```bash
git submodule sync -- 3rdParty/rnnoise
git submodule update --init --remote 3rdParty/rnnoise
git add 3rdParty/rnnoise .gitmodules
git commit -m "chore(rnnoise): sync submodule to latest upstream model"
```

> Note: the model is compiled from `3rdParty/rnnoise/src/rnn_data.c` as part of this project.

## ⚠️ Disclaimer

This plugin is not supported by TeamSpeak Systems GmbH. It is provided as-is and without any warranty. You are free to use it as a starting point for your own plugins, but you are responsible for any issues that may arise from using it.

## 📝 Contributing

If you want to contribute to this project, feel free to open a pull request. I will try to review it as soon as possible.

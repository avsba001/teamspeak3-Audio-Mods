# 🔧 音频增强插件

<div align="center">

  [![GitHub license](https://img.shields.io/github/license/Gamer92000/JUL14Ns-Audio-Mods.svg)](https://github.com/Gamer92000/JUL14Ns-Audio-Mods/blob/main/LICENSE)
  [![GitHub commits](https://badgen.net/github/commits/Gamer92000/JUL14Ns-Audio-Mods/main)](https://GitHub.com/Gamer92000/JUL14Ns-Audio-Mods/commit/)
  [![Github stars](https://img.shields.io/github/stars/Gamer92000/JUL14Ns-Audio-Mods.svg)](https://GitHub.com/Gamer92000/JUL14Ns-Audio-Mods/stargazers/)
  <br>
  <h3>如果你喜欢这个项目，请考虑点一个 Star ⭐️！</h3>
</div>

## 📖 项目简介

*Audio Mods* 是一个用于 TeamSpeak 3 的插件，为音频系统增加了一些功能。

它允许你使用 [RNNoise](https://jmvalin.ca/demo/rnnoise/) 库对背景噪声进行过滤，同时提供可配置的语音激活检测（VAD），以及一个不会将噪声无限放大的压缩器。

## 📝 许可证

本项目基于 MIT 许可证发布 —— 详情请参阅 [LICENSE](LICENSE) 文件。

## 📦 第三方库

该插件使用了 [Qt](https://www.qt.io/) 框架以及 [RNNoise](https://jmvalin.ca/demo/rnnoise/) 库。

## 🧠 RNNoise 集成说明

- RNNoise 降噪在 `src/plugin.cpp` 中通过 `rnnoise_process_frame(...)` 调用。
- 当前构建直接链接 `3rdParty/rnnoise/src` 中的源码，包括 `rnn_data.c`（内嵌模型数据）。
- 每个音频通道的 RNNoise 状态通过 `FixedSizeMap<int, DenoiseState*>` 管理，使每个通道拥有独立的降噪状态。

## 🔄 从上游同步 RNNoise 模型（`xiph/rnnoise`）

该仓库通过子模块在 `3rdParty/rnnoise` 跟踪 RNNoise。要更新到最新的上游模型/代码：

```bash
git submodule sync -- 3rdParty/rnnoise
git submodule update --init --remote 3rdParty/rnnoise
git add 3rdParty/rnnoise .gitmodules
git commit -m "chore(rnnoise): 同步子模块到最新上游模型"

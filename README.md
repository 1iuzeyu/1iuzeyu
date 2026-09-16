<h1 align='left'>刘泽宇</h1>

**Speech restoration** · postdoc at the Institute of Acoustics, Chinese Academy of Sciences · Beijing

`1iuzeyu` · he/him

---

I'm Zeyu Liu, and my daily problem is simple to state and hard to do well: take speech that has been through noise, reverberation or packet loss, and give back something a person can listen to without wincing.

## Two questions I keep circling

Most of my work orbits two questions. First: how do you make a restoration model behave when the degradation is not the clean kind we simulate? Real packet loss arrives in bursts, codecs switch, and the room changes between training and deployment. A model that only knows random dropout on clean files tends to panic in the field.

Second: how much should a model know about the speaker? If restoration is too aggressive, it strips away the prosody that carries meaning. If it is too cautious, it leaves the noise in. I am trying to find a middle ground where the model understands what speech should sound like without flattening the person behind it.

## How I got here

This was not a straight path. I started out at a campus radio station during my undergrad years in Changsha, editing late-night talk shows recorded on cheap microphones. The audio was full of chair squeaks, air-conditioner hum and the occasional door slam. I spent hours trying to clean it up with a script I barely understood, and I never got it quite right. That frustration stuck with me.

Later, during a master's project on audio effects, I realized the same problem showed up in hearing aids, voice assistants and phone calls. I moved to Beijing for a PhD in speech processing, spent a long time staring at spectrograms, and eventually ended up as a postdoc at the Institute of Acoustics, Chinese Academy of Sciences. The chair squeaks are gone, but the basic wonder is still there: our ears are remarkably good at ignoring noise, and machines are not.

## Tools I actually use

A short list, tied to what I do each week:

- **Python** — the main language for experiments, data wrangling and quick spectrogram checks. I probably write more Python than Chinese in a day.
- **PyTorch + torchaudio** — for model prototyping and for audio transforms that work on batches without me hand-rolling the same STFT code.
- **ffmpeg and sox** — for building degraded speech pairs. I know these tools look ancient, but they are reliable and scriptable, which matters more.
- **Slurm** — for queuing GPU jobs on our cluster. I have learned to write batch scripts that fail loudly instead of failing quietly after three hours.
- **WebRTC traces** — when I want packet loss that behaves like real packet loss, not just uniform random drops.

## Next steps

Nothing glamorous, but each one moves the work forward:

- Turn my packet-loss simulation into a small benchmark that other people can run without needing our internal data.
- Write up the current dereverberation experiments as a technical report, mostly so the details stop living in my head.
- Improve the listening test setup so that subjective results are easier to reproduce and compare.
- Open-source the degraded-speech data pipeline, with clear documentation for the parts that are still messy.

## A typical restoration run

```
degraded.wav -> VAD / packet-loss mask -> denoise -> dereverb -> decoder -> restored.wav
```

The tricky step for me is the mask. It tells the downstream stages which time-frequency bins are probably reliable. If the mask is too conservative, we discard recoverable speech. If it is too confident, the model starts hallucinating clean content over noise. Getting that one step right often matters more than the choice of decoder architecture.

## What I'm exploring now

I have been reading more about self-supervised speech representations and how they handle degraded input. It feels promising that a pretrained model can carry a lot of acoustic knowledge into a restoration system, but I want to understand why small changes in the frontend sometimes improve objective scores yet make the output sound worse to human listeners.

I am also curious about simpler things: why certain room impulse responses are much harder to invert than others, and whether we can predict difficulty from the impulse response itself. No big conclusions yet. I am still at the stage of asking better questions.

<details>
<summary>中文简介</summary>

我在中国科学院声学研究所做博士后，研究方向是语音恢复：把混入噪声、混响或丢包的语音还原成清晰信号。平时主要用 Python 和 PyTorch 做实验，也喜欢折腾命令行工具。这个主页记录一些还在进行中的工作，欢迎交流。

</details>

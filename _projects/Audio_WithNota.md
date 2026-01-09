---
title: Audio Language Model Lightweight Project
featured_image: "images/projects/Audio_WithNota/Audio_Overview_2.png"
start_date: '2025-01-02'
end_date: '2025-02-12'
last_modified_at: '2026-01-09 22:00:00'
---
![Overview](../images/projects/Audio_WithNota/Audio_Overview_2.png)
<p align="center" style="font-size:0.9em; color:#555;">
  <b> Overview of the proposed model architecture.</b>
</p>

👉 [Code](https://github.com/boostcampaitech7/level4-cv-finalproject-hackathon-cv-16-lv3/tree/main)
<br>
👉 [Report](../images/projects/Audio_WithNota/Audio_Report.pdf)





## Objective
With the integration and pretraining of audio adapters, large language models have become capable of understanding diverse audio signals—such as speech, music, and environmental sounds—and performing a wide range of downstream tasks. However, in typical device environments with limited VRAM, **lightweight modeling of audio language models is essential**.

The objective of this hackathon is to establish a practical recipe for building **smaller and faster audio language models** that preserve the baseline accuracy on standard audio understanding benchmarks. In particular, we focus on maintaining the performance of the [SALMOON](https://github.com/bytedance/SALMONN?tab=readme-ov-file) model—an audio-centric multimodal LLM capable of processing general audio, speech, and music inputs—while significantly reducing **memory usage** and **inference latency**.

To guide our design choices, we target deployment on mobile GPUs that are suitable for on-device inference, with the following approximate constraints: **ASR latency ≈ 0.05 s, memory usage ≈ 6 GB, time-to-first-token (TTFT) ≈ 1 s, and time-per-output-token (TPOT) ≈ 0.1 s**.
For **audio captioning (AAC)**, since no explicit benchmark threshold is provided, our goal is to avoid noticeable performance degradation while optimizing efficiency.
<br/>

## Method
We adopt SALMONN as the base audio language model and redesign its architecture with a focus on memory efficiency and low-latency inference.
Our approach combines parameter-efficient fine-tuning, sparse activation, and model compression techniques to meet on-device deployment constraints.

The overall architecture of the redesigned model is illustrated below.
<!-- 예시: 동일 높이 220px, 비율 유지 -->
<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 18px;
  margin: 28px 0;
">

  <figure style="margin:0; text-align:center;">
    <img src="../images/projects/Audio_WithNota/Audio_Method_1.png"
         alt="Overall architecture of the proposed audio-language model"
         style="
           width:100%;
           aspect-ratio: 16 / 9;
           object-fit: contain;
           background:#fafafa;
           border-radius:10px;
         ">
    <figcaption style="margin-top:8px; font-size:0.9em; color:#555;">
      <b>QLoRA</b> 
    </figcaption>
  </figure>

  <figure style="margin:0; text-align:center;">
    <img src="../images/projects/Audio_WithNota/Audio_Method_2.png"
         alt="Lightweight optimization strategies applied to the model"
         style="
           width:100%;
           aspect-ratio: 16 / 9;
           object-fit: contain;
           background:#fafafa;
           border-radius:10px;
         ">
    <figcaption style="margin-top:8px; font-size:0.9em; color:#555;">
      <b>MoE</b>
    </figcaption>
  </figure>

  <figure style="margin:0; text-align:center;">
    <img src="../images/projects/Audio_WithNota/Audio_Method_3.png"
         alt="Final deployed model configuration"
         style="
           width:100%;
           aspect-ratio: 16 / 9;
           object-fit: contain;
           background:#fafafa;
           border-radius:10px;
         ">
    <figcaption style="margin-top:8px; font-size:0.9em; color:#555;">
      <b>Model Distillation</b>
    </figcaption>
  </figure>

</div>


### (1) QLoRA
We apply QLoRA to enable parameter-efficient fine-tuning under limited VRAM.
By fine-tuning low-rank adapters on quantized base weights, we significantly reduce memory usage while preserving the baseline performance of the model.

### (2) MoE
To further improve inference efficiency, we incorporate a Mixture of Experts (MoE) architecture.
During inference, only a small subset of experts is activated for each input, which reduces the number of active parameters and leads to lower latency and memory consumption.

### (3) Distillation
We perform knowledge distillation using DeepSeek-R1 as the teacher model.
This allows the compact student model to retain strong reasoning and audio understanding capabilities while operating with substantially fewer parameters.

### (4) Audio Augmentation
To improve robustness and training stability, we apply simple yet effective audio augmentations, including noise injection and gain control.
These augmentations help the model generalize across diverse audio conditions without increasing computational overhead.

<br/>


## Result
### (1) Encoder & Decoder
<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
  margin: 24px 0;
">

  <!-- Left image -->
  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Audio_WithNota/Audio_Experiment_1.png"
           alt="Encoder"
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      Encoder Experiment
    </p>
  </div>

  <!-- Right image -->
  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Audio_WithNota/Audio_Experiment_2.png"
           alt="Decoder "
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      Decoder Experiment
    </p>
  </div>

</div>

Some models were trained up to Stage 2 but excluded from ASR and AAC evaluation due to limited inference time.
**Whisper-large-v3 turbo** improved ASR by approximately **30%** over Whisper-large-v2 with no significant increase in latency or memory, and was selected as the final encoder.
Removing BEATs reduced latency but severely degraded ASR, while EAT showed abnormal results and was excluded; therefore, **the original BEATs module was retained**.

### (2) LLM & Final Result

<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
  margin: 24px 0;
">

  <!-- Left image -->
  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Audio_WithNota/Audio_Experiment_3.png"
           alt="Encoder"
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      LLM Experiment
    </p>
  </div>

  <!-- Right image -->
  <div style="text-align: center;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      background: #fff;
    ">
      <img src="../images/projects/Audio_WithNota/Audio_Experiment_4.png"
           alt="Decoder "
           style="
             width: 100%;
             height: 100%;
             object-fit: contain;
           ">
    </div>
    <p style="
      margin-top: 8px;
      font-size: 0.9rem;
      color: #555;
    ">
      Final Experiment
    </p>
  </div>

</div>

LLM experiments reveal a clear trade-off between latency, memory usage, ASR, and AAC as model size increases.
Applying QLoRA reduces memory usage by nearly 50% while improving ASR by approximately 30%, and the Unsloth-based LLaMA 3.2 1B model achieves the best efficiency when considering both latency and memory. Accordingly, LLaMA 3.2 1B with QLoRA is selected as the final LLM.

<br>
<div style="background-color: #f8f9fa; border-left: 5px solid #007bff; padding: 15px; border-radius: 4px;">
  <strong>Based on these results, we select Whisper as the audio encoder, BEATs as the audio decoder, and LLaMA 3.2 1B with QLoRA as the final LLM.</strong>
</div>

Compared to the 3B lightweight SALMONN model provided by NOTA, the final model is trained using approximately 1.06M Stage 1 samples and 1.15M Stage 2 samples. In a server environment, it achieves <strong>a 16% decrease in ASR, a 27% increase in AAC, a 55% reduction in memory usage, and a 23% reduction in latency</strong>, successfully improving overall efficiency across all metrics.

## Demo 
<p align="center">
  <img src="../images/projects/Audio_WithNota/audio_demo.gif" alt="Audio Language Model Demo" style="max-width: 1080px; border-radius: 8px; box-shadow:0 4px 12px rgba(0,0,0,0.10);" />
</p>
<p align="center" style="font-size:0.95em; color:#555;">
  <b>Demo:</b> Example of the AI model analyzing and responding to audio input based on a given prompt.
</p>


# UI-R1: Enhancing **Efficient** Action Prediction of GUI Agents by Reinforcement Learning

<font size=4><div align='center' > [[📖 Paper](https://arxiv.org/abs/2503.21620)] [[🤗 UI-R1-3B](https://huggingface.co/LZXzju/Qwen2.5-VL-3B-UI-R1)] [[🤗 UI-R1-E-3B](https://huggingface.co/LZXzju/Qwen2.5-VL-3B-UI-R1-E)][[🤗 Datasets](https://huggingface.co/datasets/LZXzju/UI-R1-3B-Train)] [[🤗 Daily Paper](https://huggingface.co/papers/2503.21620)]</div></font>

## 🔥 Overview

We propose **UI-R1**, the first framework to explore how rule-based RL can enhance the reasoning capabilities of multimodal large language models (MLLMs) for GUI action prediction tasks.
<a href="">
  <img src="assets/method.png" alt="Logo" >
</a>


Experimental results demonstrate that our proposed **UI-R1-3B** achieves significant improvements over the base model (i.e. Qwen2.5-VL-3B) on both in-domain (ID) and out-of-domain (OOD) tasks, with average accuracy gains of **22.1%** on ScreenSpot, **6.0%** on ScreenSpot-Pro, and **12.7%** on AndroidControl. Furthermore, UI-R1-3B delivers competitive performance compared to larger models (e.g., OS-Atlas-7B) trained via supervised fine-tuning (SFT) on 76K samples.

<a href="">
  <img src="assets/radar.png" alt="Logo" >
</a>

## Grounding Leaderboard: [UI-I2E-Bench](https://colmon46.github.io/i2e-bench-leaderboard/)
|     Model      | ScreenSpot | UI-I2E-Bench Avg | ScreenSpot-Pro | Average  |
| :------------: | :--------: | :--------------: | :------------: | :--: |
| UI-TARS-1.5-7B |    88.1    |       73.2       |      42.2      | 67.8 |
| Uground-V1-72B |    89.7    |       76.3       |      34.3      | 66.8 |
|  UI-TARS-72B   |    88.4    |       73.7       |      38.1      | 66.7 |
|   **UI-R1-E-3B**   |    89.2    |       69.1       |      33.5      | 63.9 |
| Uground-V1-7B  |    87.1    |       70.3       |      31.1      | 62.8 |
|   InfiGUI-R1   |    87.5    |       69.7       |      29.6      | 62.3 |
|   UI-TARS-7B   |    89.5    |       61.4       |      35.7      | 62.2 |
| Qwen2.5-VL-72B |    87.1    |       51.4       |      43.6      | 60.7 |
| UI-I2E-VLM-7B  |    82.5    |       69.5       |      23.6      | 58.5 |
|   UI-TARS-2B   |    82.3    |        62        |      27.7      | 57.3 |
| Qwen2.5-VL-7B  |    84.7    |       53.8       |       29       | 55.8 |
| OmniParser-V2  |     72     |       54.8       |      39.6      | 55.5 |
| Uground-V1-2B  |    78.8    |       57.4       |      26.6      | 54.3 |
|  OS-Atlas-7B   |    82.5    |       58.6       |      18.9      | 53.3 |
|     **UI-R1-3B**      |    83.3    |       58.5       |      17.8      | 53.2 |
|   UGround-7B   |    74.1    |       54.2       |      16.5      | 48.3 |
| UI-I2E-VLM-4B  |    70.4    |       53.4       |      12.2      | 45.3 |
|   OmniParser   |    73.9    |       53.1       |      8.3       | 45.1 |
|   ShowUI-2B    |    76.8    |       41.5       |      7.7       |  42  |
| Qwen2.5-VL-3B  |    55.5    |       41.7       |      23.9      | 41.3 |
|   Aguvis-7B    |    84.4    |       53.2       |      22.9      | 40.4 |
|  OS-Atlas-4B   |    70.1    |       44.3       |      3.7       | 39.4 |
|  Qwen2-VL-7B   |    42.6    |       48.7       |      1.6       |  31  |
|    Seeclick    |    55.8    |       26.4       |      1.1       | 27.8 |
|  InternVL2-4B  |    4.2     |       0.9        |      0.3       | 1.8  |

## 🔥Insight 1 : Fast Grounding

> **Thinking is not needed for GUI grounding.**

Inspired by concurrent works studying efficient LRM, we realize efficient reasoning by RFT training. UI-R1-3B-E's training consists of two steps:

1. DAST (Difficulty-Adaptive Slow-Thinking): Add difficulty-adaptive length reward to make reasoning from slow to fast.
2. Nothinking: Not output reasoning process.

Note: UI-R1-3B (v2) and UI-R1-3B-E both train on larger dataset (2K grounding data in [GUI-R1-3K](https://huggingface.co/datasets/ritzzai/GUI-R1)) compared to UI-R1-3B (v1).

#### Benchmark 1: ScreenSpotV2

| ScreenSpotV2  | inference mode | Mobile-T | Mobile-I | Desktop-T | Desktop-I | Web-T    | Web-I    | Avg↑ / Len↓        |
| ------------- | -------------- | -------- | -------- | --------- | --------- | -------- | -------- | ----------------- |
| OS-ATLAS-7B   | w/o thinking   | 95.2     | 75.8     | 90.7      | 63.6      | 90.6     | 77.3     | 84.1 /            |
| UI-TARS-7B    | w/o thinking   | 95.2     | 79.1     | 90.7      | 68.6      | 90.6     | 78.3     | 84.7 /            |
| UI-R1-3B (v1) | w/ thinking    | 96.2     | **84.3** | 92.3      | 63.6      | 89.2     | 75.4     | 85.4 / 67         |
| GUI-R1-3B     | w/ thinking    | 97.6     | 78.2     | 94.3      | 64.3      | 91.0     | 72.4     | 85.0 / 80         |
| UI-R1-3B (v2) | w/ thinking    | 97.6     | 79.6     | 92.3      | 67.9      | 88.9     | 77.8     | 85.8 / 60         |
| UI-R1-E-3B    | w/o thinking   | **98.2** | 83.9     | **94.8**  | **75.0**  | **93.2** | **83.7** | **89.5** / **28** |

#### Benchmark 2: ScreenSpot-Pro

| ScreenSpot-Pro | inference mode | Average Length↓ | Average Accuracy↑ |
| -------------- | -------------- | --------------- | ---------------- |
| UGround-7B     | w/o thinking   | -               | 16.5             |
| OS-ATLAS-7B    | w/o thinking   | -               | 18.9             |
| UI-R1-3B (v1)  | w/ thinking    | 102             | 17.8             |
| GUI-R1-3B      | w/ thinking    | 114             | 26.6             |
| UI-R1-3B (v2)  | w/ thinking    | 129             | 29.8             |
| UI-R1-E-3B     | w/o thinking   | **28**          | **33.5**         |

##### Analysis

1. Our UI-R1-3B-E achieves **SOTA** with **least** answer tokens in 3B/7B Open-source methods, demonstrating GUI grounding needs no reasoning.

##### Todo

- [ ] Performance on 7B may be opposite.
- [ ] Performance on Planning may be opposite. The author predicts that Fast Grounding, Slow Planning.
- [X] The checkpoints of UI-R1-3B-E will be released soon.
- [X] The updated paper will come soon.
- [X] The efficient training code will come soon. (in src/script/train_e.sh)
## Setup

```shell
conda create -n ui-r1 python=3.10
conda activate ui-r1
bash setup.sh
```

## Data

Our training mobile data is a subset from AndroidControl and ScreenSpot.

You can also prepare your training or inference data like:

```
images/:
	image1.png
	image2.png
```

```
test.json:
[
	{
	"img_filename": "image1.png",
        "bbox": [
            825,
            72,
            1673,
            149
        ],
        "instruction": "search bar"
     },
     {
	"img_filename": "image2.png",
        "bbox": [
            123,
            732,
            334,
            812
        ],
        "instruction": "check weather"
     }
]
```

where bbox : [x1,y1,x2,y2] is the coordinate of the left top and the right bottom of the ground truth bbox

## Inference

We provide an example here

```shell
cd evaluation/
bash test.sh
```

Please fill the MODEL_PATH, IMG_PATH, TEST_JSON with your real checkpoint path and data path.
## Training

```shell
cd src/script/
bash train.sh
# efficient training
bash train_e.sh
```




## 🗞️ News
- **`2025-11-08`**: Our paper was accepted by **AAAI-2026**.
- **`2025-05-14`**: We update the [paper](https://arxiv.org/abs/2503.21620) with UI-R1-E-3B.
- **`2025-05-12`**: We release the [checkpoints](https://huggingface.co/LZXzju/Qwen2.5-VL-3B-UI-R1-E) of the UI-R1-E-3B model.
- **`2025-05-12`**: We fix the bug of scales when batch_size > 1.
- **`2025-05-11`**: We release the efficient training code of the UI-R1-E-3B model.
- **`2025-04-02`**: We release the [datasets](https://huggingface.co/datasets/LZXzju/UI-R1-3B-Train) of the UI-R1-3B (v1) model.
- **`2025-03-30`**: We release the [checkpoints](https://huggingface.co/LZXzju/Qwen2.5-VL-3B-UI-R1) of the UI-R1-3B (v1) model.
- **`2025-03-30`**: We release the UI-R1 repository.
- **`2025-03-27`**: We release our [paper](https://arxiv.org/abs/2503.21620).





## ⭐️ Citation

If you find this project useful, welcome to cite us.

```bit
@article{lu2025ui,
  title={UI-R1: Enhancing Action Prediction of GUI Agents by Reinforcement Learning},
  author={Lu, Zhengxi and Chai, Yuxiang and Guo, Yaxuan and Yin, Xi and Liu, Liang and Wang, Hao and Xiong, Guanjing and Li, Hongsheng},
  journal={arXiv preprint arXiv:2503.21620},
  year={2025}
}
```



## 🤝 Acknowledgements

We sincerely thank projects [R1-V](https://github.com/Deep-Agent/R1-V), [Open-R1](https://github.com/huggingface/open-r1), and [Open-r1-multimodal](https://github.com/EvolvingLMMs-Lab/open-r1-multimodal), [VLM-R1](https://github.com/om-ai-lab/VLM-R1) for providing their open-source resources.

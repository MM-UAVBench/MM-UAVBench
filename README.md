
<div align="center" style="font-family: charter;">
  <h1><i>MM-UAVBench</i>:<br>How Well Do Multimodal Large Language Models See, Think, and Plan in Low-Altitude UAV Scenarios?</h1>
  <br>
  <a href='https://mm-uavbench.github.io/'><img src='https://img.shields.io/badge/Project-Page-Green'></a>
  <a href='https://mm-uavbench.github.io/static/pdfs/mm-uavbench.pdf'><img src='https://img.shields.io/badge/Paper-PDF-orange'></a>
  <a href='https://arxiv.org/abs/2512.23219'><img src='https://img.shields.io/badge/Arxiv-Page-purple'></a>
  <a href='https://huggingface.co/datasets/daisq/MM-UAVBench'><img src='https://img.shields.io/badge/Data-HuggingFace-red'></a>
  <br><br>
  <img src="assets/teaser.png" width="100%"/>
</div>

## 🎉 News 
- **[2026.01]** 📢 We released the dataset and corresponding evaluation code. Note that for tasks labeled with the data type "video_frames", only key frames are included in the current release; the full video clips will be released soon.
- **[2025.12]** 🚀 We released the arXiv paper.

## Contents
- [News](#🎉-news)
- [Benchmark Overview](#benchmark-overview)
- [Results](#results)
- [Evaluation Pipeline](#evaluation-pipeline)
- [Citation](#citation)

## Benchmark Overview
We introduce <strong>MM-UAVBench</strong>, a comprehensive benchmark designed to evaluate the perception, cognition, and planning abilities of MLLMs in low-altitude UAV scenarios. It features three main characteristics:
<ul style="list-style-type: square;  margin-left: 2rem;">
<li><strong>Comprehensive Task Design.</strong> It includes <strong>19</strong> tasks across three key capability dimensions and incorporates UAV-specific considerations, specially
including <strong>multi-level cognition</strong> (object, scene, and event) and <strong>planning </strong>that involves both aerial and ground agents.</li>
<li><strong>Diverse Real-World Scenarios.</strong> We collect real-world UAV videos and images from diverse data sources, 
encompassing <strong>1549 video clips</strong> and <strong>2873 images</strong> with an average resolution of <strong>1622 × 1033</strong>.</li>
<li><strong>High-quality Human Annotations.</strong> We manually annotate 16 tasks, while 3 additional tasks come from rule-based transformation of manual labels, yielding <strong>5702 multiple-choice QA</strong> in total.</li>
</ul>
<img src="assets/cmp.png" width="100%"/>

## Results
<img src="assets/results.png" width="100%"/>

## Evaluation Pipeline
### Step 1: Install Dependencies

```bash
git clone https://github.com/MM-UAVBench/MM-UAVBench.git 
cd MM-UAVBench
git clone https://github.com/open-compass/VLMEvalKit.git
cd VLMEvalKit
pip install -e .
```

### Step 2: Configure Evaluation Dataset
Copy the dataset file to the VLMEvalKit directory:
```bash
cp ~/MM-UAVBench/mmuavbench.py ~/MM-UAVBench/VLMEvalKit/vlmeval/dataset
```
Edit `~/MM-UAVBench/VLMEvalKit/vlmeval/dataset/__init__.py` and add the following content:
```python
from.mmuavbench import MMUAVBench_Image, MMUAVBench_Video

IMAGE_DATASET = [
    # Existing datasets
    MMUAVBench_Image,
]

VIDEO_DATASET = [
    # Existing datasets
    MMUAVBench_Video,
]
```


### Step 3: Download Dataset
Download the dataset from [huggingface](https://huggingface.co/datasets/daisq/MM-UAVBench) and put it in `~/MM-UAVBench/data`. 

Set the dataset path in `~/MM-UAVBench/VLMEvalKit/.env`：
```
LMUData="~/MM-UAVBench/data"
```
### Step 4: Run Evaluation
Modify the model checkpoint path in `~/MM-UAVBench/VLMEvalKit/vlmeval/config.py` to your target model path.

Run the evaluation command:
```bash
python run.py \
    --data MMUAVBench_Image MMUAVBench_Video \
    --model Qwen3-VL-8B-Instruct \
    --mode all \
    --work-dir ~/MM-UAVBench/eval_results \
    --verbose
```

## Citation
 If you find MM-UAVBench useful in your research tasks or applications, please consider to give **star⭐** and kindly cite:
```
@article{dai2025mm,
  title={MM-UAVBench: How Well Do Multimodal Large Language Models See, Think, and Plan in Low-Altitude UAV Scenarios?},
  author={Dai, Shiqi and Ma, Zizhi and Luo, Zhicong and Yang, Xuesong and Huang, Yibin and Zhang, Wanyue and Chen, Chi and Guo, Zonghao and Xu, Wang and Sun, Yufei and others},
  journal={arXiv preprint arXiv:2512.23219},
  year={2025}，
  url={https://arxiv.org/abs/2512.23219}
}
```
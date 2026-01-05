# MM-UAVBench
Code for "MM-UAVBench: How Well Do Multimodal Large Language Models See, Think, and Plan in Low-Altitude UAV Scenarios?"

## Environment and Setup
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


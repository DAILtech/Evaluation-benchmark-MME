## Clone the Required Repositories for MME Evaluation Benchmark

To streamline the use of the MME Benchmark, we have consolidated all the necessary repositories and configured them for one-button deployment. Follow the steps below to get started. We take LVLM LLaVA as an example.

### Step 1: Directory Setup

Begin by creating the required directory structure inside your LLaVA workspace:  

```bash
mkdir -p LLaVA/playground/data/eval/MME
```

This ensures all evaluation data is well-organized. We strongly recommend placing the `MME` folder inside eval for better clarity and separation.

### Step 2: Clone the MME Evaluation Benchmark

Now, clone the benchmark repository:    
```
git clone https://github.com/DAILtech/Evaluation-benchmark-MME/
```
This repository contains everything needed for running the MME Benchmark in one go.

### Step 3: Run evaluation command 
(your should in `LLaVA` folder)
```bash
#!/bin/bash
# cd LLaVA

python -m llava.eval.model_vqa_loader \
    --model-path /root/autodl-tmp/LLaVA/llava-v1.5-7b \
    --question-file ./playground/data/eval/MME/llava_mme_test.jsonl \
    --image-folder ./playground/data/eval/MME/MME_Benchmark_release_version \
    --answers-file ./playground/data/eval/MME/answers/llava-v1.5-7b.jsonl \
    --temperature 0 \
    --conv-mode vicuna_v1 \

cd ./playground/data/eval/MME

python convert_answer_to_mme.py --experiment llava-v1.5-7b

cd eval_tool

python calculation.py --results_dir answers/llava-v1.5-7b

# Do this after cloning the repo

## Command line examples

```shell
wget https://ml-site.cdn-apple.com/datasets/fastvlm/llava-fastvithd_0.5b_stage2.zip -P checkpoints
unzip checkpoints/llava-fastvithd_0.5b_stage2.zip -d checkpoints
rm checkpoints/llava-fastvithd_0.5b_stage2.zip
cd -
```

```bash
brew install anaconda
# From Anaconda gui create a new env named fastvlm with python 3.10
. /opt/homebrew/anaconda3/bin/activate && conda activate /opt/homebrew/anaconda3/envs/fastvlm
pip install -e .
```

```bash
python3 predict.py --model-path checkpoints/llava-fastvithd_0.5b_stage2 \
                  --image-file describe-images/camphoto_351212254.png \
                  --prompt "Describe the image."
```

```bash
python3 predict.py --model-path checkpoints/llava-fastvithd_0.5b_stage2 \
                  --image-file describe-images/camphoto_1804928587.png \
                  --prompt "Describe in russian. How the meat is cooked?"
```

```bash

python3 predict.py --model-path checkpoints/llava-fastvithd_0.5b_stage2 \
                  --image-file "describe-images/Screenshot 2025-09-06 at 01.08.09.png" \
                  --prompt "How many sticks?. ?"
```

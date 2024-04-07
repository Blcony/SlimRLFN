## SlimRLFN: Making RLFN Smaller and Faster Again

### Usage

To obtain the results of our SlimRLFN, please conduct the following commands:
```shell
CUDA_VISIBLE_DEVICES=0 python test_demo.py --data_dir [path to your data dir] --save_dir [path to your save dir] --model_id 21
```

To obtain the results of our SlimRLFN-pruned, please conduct the following commands:
```shell
CUDA_VISIBLE_DEVICES=0 python test_demo.py --data_dir [path to your data dir] --save_dir [path to your save dir] --model_id 21 --use_prune
```

- Be sure the change the directories `--data_dir` and `--save_dir`.


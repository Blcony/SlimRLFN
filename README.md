## SlimRLFN: Making RLFN Smaller and Faster Again

### Usage

```shell
CUDA_VISIBLE_DEVICES=0 python test_demo.py --data_dir [path to your data dir] --save_dir [path to your save dir] --model_id 21
```

- Be sure the change the directories `--data_dir` and `--save_dir`.
- It is worth mentioning that 59 line and 68 line in the test_demo.py should be carefully check to match the real dataset name. (PS: Original codes `LSDIR_DIV2K_test_HR/*.png` is changed to `DIV2K_LSDIR_test_HR/*.png`)

--------------------------------------------------

### *Notice*

As proposed by other participants in the [official website](https://codalab.lisn.upsaclay.fr/forums/17491/2434/), we also notice that the inference time in the official test scripts does not consider the influence of GPU warm-up, thus the results fluctuate often. 

In other words, **we think the inference time without GPU warm-up may not reflect the true efficiency of models, especially for the pruned models**.

In our experiments, through iterative pruning, our model size is further shrunk while maintaining the requested performance. However, due to the influence of the absence of GPU warm-up, our model's inference time is even longer than the non-pruned model (For more explanation details, please refer to the "Performance" section).

In fact, we have sent an email to you to clarify the inference time calculation rule, but have not received a response (maybe the time is too short between the email time and the challenge end time).

Therefore, **if you choose to maintain the inference time calculation rule in the original version (which does not consider the GPU warm-up)**, please refer to the shell command in section 'usage' above and ignore the following contents. 

**If you choose to consider the GPU warm-up such as calculating the average of last several times,** you can also execute our pruned model by adding `--use_prune` as follows, to obtain a lighter SR model.

```shell
CUDA_VISIBLE_DEVICES=0 python test_demo.py --data_dir [path to your data dir] --save_dir [path to your save dir] --model_id 21 --use_prune
```

Thank you again for organizing such an excellent challenge, and if you have any questions or requests, please drop me an email (slzhou96@mail.ustc.edu.cn) without any hesitation.

-----------------

### *Performance*

| Model          | PSNR(val) | PSNR(test) | Runtime[ms] | Runtime*[ms] | Params[M] | Flops[G] |
| -------------- | --------- | ---------- | ----------- | ------------ | --------- | -------- |
| RLFN_baseline  | 26.955    | 27.070     | 16.9637     | 10.6497      | 0.317     | 19.675   |
| SlimRLFN       | 26.9136   | 27.026     | 13.7024     | 8.6071       | 0.208     | 11.991   |
| SlimRLFN-prune | 26.9016   | 27.020     | 15.1777     | 8.5421       | 0.197     | 11.295   |

- The inference speeds were obtained from testing on a V100-32G GPU.
- `Runttime[ms]` represents the average of the last 4 results, **which means the inference time without considering the GPU warm-up.** Specifically,  we run the test_demo.py script 5 times separately (outside of test_demo.py)）
- `Runttime*[ms]` represents the average of the last 4 results, **which means the inference time considering the GPU warm-up.** Specifically, we run the test_demo.py script 5 times consecutively (within test_demo.py).

Due to the significant impact of GPU warm-up on inference speed, which can severely affect the inference speed of pruned models, we list a comparison of inference speeds under two scenarios:  and running it 5 times separately (outside of test_demo.py):

| Model           | 1       | 2       | 3       | 4       | 5       |
| --------------- | ------- | ------- | ------- | ------- | ------- |
| RLFN_baseline   | 17.2096 | 16.6265 | 17.0407 | 17.3653 | 16.8221 |
| RLFN_baseline*  | 17.2944 | 10.6083 | 10.6145 | 10.7650 | 10.6108 |
| SlimRLFN        | 13.6977 | 13.5549 | 13.4250 | 13.7798 | 14.0500 |
| SlimRLFN*       | 13.5337 | 8.5398  | 8.5532  | 8.6928  | 8.6423  |
| SlimRLFN-prune  | 15.1199 | 14.9460 | 15.4287 | 14.8240 | 15.5120 |
| SlimRLFN-prune* | 14.8473 | 8.5788  | 8.4831  | 8.5738  | 8.5327  |


# AlignDiff

### Environment
```shell
conda env create -f aligndiff.yaml
conda activate aligndiff
```

### Data
The dataset follows [TargetDiff](https://arxiv.org/abs/2303.03543). For more details, please refer to [the repository of TargetDiff](https://github.com/guanjq/targetdiff?tab=readme-ov-file#data).

### Pretrained Model
The pretrained model follows [IPDiff](https://openreview.net/forum?id=qH9nrMNTIW). To download the model checkpoint, please refer to [the repository of IPDiff](https://github.com/YangLing0818/IPDiff/tree/main?tab=readme-ov-file#%EF%B8%8F%EF%B8%8Fpretrained-ipdiff).
```shell
./pretrained_models
```

### Train
```shell
python train.py
```

### Sampling
Sample 100 ligands per protein.
```shell
python sample_split.py --start_index 0 --end_index 99 --batch_size 25
```

### Evaluation
Evaluate 100 samples and calculate metrics.
```shell
python eval_split.py --eval_start_index 0 --eval_end_index 99
python cal_metrics_from_pt.py
```


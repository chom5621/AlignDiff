# AlignDiff

| Package           | Version   |
|-------------------|-----------|
| Python            | 3.8       |
| PyTorch           | 1.13.1    |
| CUDA              | 11.6      |
| PyTorch Geometric | 2.2.0     |
| RDKit             | 2022.03.2 |

### Environment
```bash
conda env create -f aligndiff.yaml
conda activate aligndiff
```

### Data
The dataset download follows [TargetDiff](https://arxiv.org/abs/2303.03543). For more details, please refer to [the repository of TargetDiff](https://github.com/guanjq/targetdiff?tab=readme-ov-file#data).
```bash
./datasets
```

### Pretrained Model
The pretrained model download follows [IPDiff](https://openreview.net/forum?id=qH9nrMNTIW). To download the model checkpoint, please refer to [the repository of IPDiff](https://github.com/YangLing0818/IPDiff/tree/main?tab=readme-ov-file#%EF%B8%8F%EF%B8%8Fpretrained-ipdiff).
```bash
./pretrained_models
```

### Train
```bash
python train.py
```

### Sampling
Sample 100 ligands per protein.
```bash
python sample_split.py --start_index 0 --end_index 99 --batch_size 25
```

### Evaluation
Evaluate 100 samples and calculate metrics.
```bash
python eval_split.py --eval_start_index 0 --eval_end_index 99
python cal_metrics_from_pt.py
```


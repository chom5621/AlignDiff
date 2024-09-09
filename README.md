# AlignDiff

### 가상환경 설치
```bash
conda env create -f aligndiff.yaml
conda activate aligndiff
```

| Package           | Version   |
|-------------------|-----------|
| Python            | 3.8       |
| PyTorch           | 1.10.1    |
| CUDA              | 11.3      |
| Pyg               | 2.0.4     |
| RDKit             | 2022.3.5  |

- Metric 중 하나인 vina 계산에 실패하는 경우, /opt/conda/lib/python3.9/site-packages/vina/vina.py 파일의 line 260를 다음과 같이 바꿉니다: astype(np.int64)


### 데이터 다운로드
- 데이터는 [TargetDiff](https://arxiv.org/abs/2303.03543) 논문의 데이터셋을 사용했습니다. 다운로드는 다음 깃헙에서 받을 수 있습니다: [TargetDiff repository](https://github.com/guanjq/targetdiff?tab=readme-ov-file#data).
```bash
./datasets/crossdocked_v1.1_rmsd1.0
```


### 사전학습 모델 다운로드
- 베이스라인 모델은 [IPDiff](https://openreview.net/forum?id=qH9nrMNTIW) 논문의 체크포인트를 사용했습니다. 다운로드는 다음 깃헙에서 받을 수 있습니다: [IPDiff repository](https://github.com/YangLing0818/IPDiff/tree/main?tab=readme-ov-file#%EF%B8%8F%EF%B8%8Fpretrained-ipdiff).
```bash
./pretrained_models/ipnet
```


### 학습
- Contribution: 연속형 변수인 position을 학습하는 mse_loss_pos과 align되도록, 이산형 변수인 atom type과 aromatic을 학습할 때 crossentropy_loss_v 대신 새로운 mse_loss_v 제안
- Result: Validation step에서 atom type과 aromatic에 대한 예측률 향상 (AUROC 98.6% 달성)
```bash
python train_align.py
```


### 샘플링
- 테스트셋의 프로틴 100개에 대해, 각 프로틴 당 100개의 분자 샘플들을 생성합니다.
```bash
python sample_split.py --start_index 0 --end_index 99 --batch_size 25
```


### 평가
- 샘플링한 10,000개의 샘플들을 evaluate하고 metric들을 계산합니다.
```bash
python eval_split.py --eval_start_index 0 --eval_end_index 99
```

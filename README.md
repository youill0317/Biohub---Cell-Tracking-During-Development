# Biohub - Cell Tracking During Development

- 대회: [Biohub - Cell Tracking During Development](https://www.kaggle.com/competitions/biohub-cell-tracking-during-development) (Kaggle, 2026, 코드 대회)
- 지표: adjusted edge Jaccard + 0.1 × division Jaccard (노드 매칭 7 µm)
- 최종 결과: Private 0.917 · 1057위 / 4020팀 (Public 0.957 · 257위)

## 최종 제출

| 노트북 | 제출 ID | Kaggle 커널 | Public | Private |
|---|---|---|---|---|
| `notebooks/x138-steal-prot10-sm05-fastcommit-v1.ipynb` | 56631035 | youill0317/x138-steal-prot10-sm05-fastcommit-v1 v1 | 0.957 | 0.917 |
| `notebooks/x138-prot10-fastcommit-v1.ipynb` | 56540178 | youill0317/x138-prot10-fastcommit-v1 v1 | 0.954 | 0.917 |

- 노트북: Kaggle 제출 버전 원본(출력 없음)
- 기반 노트북: [anvithpothula/biohub-x138](https://www.kaggle.com/code/anvithpothula/biohub-x138) (Public 0.953 / Private 0.917로 재제출 확인)
- 변경(공통): protection10 — flow relink 전 고신뢰 단일 ILP 링크 보존
- 변경(56631035 추가): safe-division steal — 이미 다른 부모가 가진 딸 노드 탈취 허용, 탈취 여유 1.0 → 0.5 µm (`BIOHUB_SAFE_DIV_ALLOW_STEAL=1`, `BIOHUB_SAFE_DIV_STEAL_MARGIN_UM=0.5`)
- fast commit: visible test(공개 영상 4개) 커밋 실행은 placeholder `submission.csv`만 기록, 제출 재실행 시 hidden test 전체 추론

## 실행

- 학습: 없음 (외부 공개 가중치 그대로 사용)
- 추론 재실행: Kaggle에 노트북 업로드 → 아래 입력 연결 → GPU T4, 인터넷 끔 → 대회 제출
- 전체 재실행: 미실행 (포트폴리오 정리 시점)

## 입력

- 대회 데이터: `biohub-cell-tracking-during-development` (대회 규칙상 재배포 불가, Kaggle에서 참가 후 획득)
- 가중치 (Kaggle 공개 데이터셋, 제출 시점 최신 버전):
  - [pilkwang/biohub-deepcenter-unet3d-center-prior-v1](https://www.kaggle.com/datasets/pilkwang/biohub-deepcenter-unet3d-center-prior-v1) — DeepCenter 3D U-Net 중심 prior
  - [pilkwang/biohub-temporal-unet3d-seed314159-v1](https://www.kaggle.com/datasets/pilkwang/biohub-temporal-unet3d-seed314159-v1) — temporal 3D U-Net 검출기
  - [pilkwang/biohub-tracking-support-pack-50ep-v1](https://www.kaggle.com/datasets/pilkwang/biohub-tracking-support-pack-50ep-v1) — 링크 모델·패키지 묶음
  - [anvithpothula/biohub-v1284-head-s075](https://www.kaggle.com/datasets/anvithpothula/biohub-v1284-head-s075) — `v1284_head.pt`

## 환경

- Kaggle notebook, Python 3.12.13, GPU NVIDIA Tesla T4, 인터넷 끔
- Docker: `gcr.io/kaggle-private-byod/python@sha256:37c64f7dd9c54116ecd1bcc88817c5469b88387388fade02bfa8bf3fc647d461`
- 추가 패키지: 노트북 3번 셀에서 입력 데이터셋의 wheel로 오프라인 설치 (tracksdata, zarr, pyscipopt 등)

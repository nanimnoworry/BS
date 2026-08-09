<div align="center">

# 🧬 BS — Fertility PSP Research Workspace

### 난임 환자 대상 임신 성공 여부 예측 · 3안 관련 모델링 연구 기록

<p>
  <img src="https://img.shields.io/badge/Task-Binary%20Classification-2563EB?style=flat-square" alt="Binary Classification" />
  <img src="https://img.shields.io/badge/Metric-ROC--AUC-7C3AED?style=flat-square" alt="ROC-AUC" />
  <img src="https://img.shields.io/badge/Validation-5--Fold%20OOF-0891B2?style=flat-square" alt="5-Fold OOF" />
  <img src="https://img.shields.io/badge/Models-CatBoost%20%7C%20LightGBM%20%7C%20XGBoost-059669?style=flat-square" alt="Models" />
</p>

</div>

이 저장소는 `nanimnoworry` 난임 예측 프로젝트에서 진행한 **모델 비교·OOF 검증·앙상블 연구 Notebook**을 보존하는 contributor workspace입니다.

발표자료에서는 박빛샘 연구원과 연결된 작업 공간으로 사용되었고, 현재 Notebook의 Colab 실행 기록에도 박빛샘 계정의 실행 흔적이 남아 있습니다. 다만 이 저장소를 **개인 단독 연구 결과로 해석하지 않습니다.** 프로젝트의 실험 설계, 모델링, 검증, 결과 해석은 팀 협업으로 진행되었으며, 공식 최종 제출·발표 계보의 기준점은 [`nanimnoworry/PSP`](https://github.com/nanimnoworry/PSP)입니다.

---

## 🎯 Repository Role

현재 이 저장소에는 다음 연구 Notebook이 보존되어 있습니다.

```text
3안 모델.ipynb의 사본
```

원본 GitHub 경로는 Unicode 조합 방식과 파일명이 그대로 보존되어 있으며, 현재 Git blob은 다음과 같습니다.

```text
5f3352bcf8ff1d326e6cbb532e5fc4d4b78285b6
```

파일명에 `3안 모델`이 포함되어 있지만, **파일명만으로 이 Notebook을 공식 최종 3안의 canonical artifact와 동일하다고 단정하지 않습니다.** 이 저장소의 역할은 3안과 연결되는 모델링 아이디어와 실험 흐름을 보존하는 것입니다.

---

## 🔬 What This Notebook Explores

이 Notebook은 단순한 단일 모델 실행 파일이라기보다, 여러 모델과 검증 방식을 단계적으로 비교한 **의미 있는 모델링 연구 기록**에 가깝습니다.

### 1. 데이터 및 결측 구조 확인

Notebook에서 확인한 데이터 규모는 다음과 같습니다.

```text
Train : 256,351 rows × 69 columns
Test  :  90,067 rows × 68 columns
Target: 임신 성공 여부
Metric: ROC-AUC
```

난자 해동 경과일, PGS/PGD 여부, 착상 전 유전 검사 여부 등 결측률이 높은 변수를 직접 확인하고 시각화하는 단계가 포함되어 있습니다.

### 2. 조합·비율 Feature Engineering

시술 맥락을 단순 개별 변수로만 사용하지 않고 조합·비율 신호를 추가로 실험합니다.

대표 예시는 다음과 같습니다.

```text
treatment_x_specific_proc
age_x_specific_proc
transfer_per_created_embryo
stored_per_created_embryo
mixed_per_fresh_oocyte
icsi_oocyte_rate
```

특히 배아 생성·이식·저장, 난자 혼합·미세주입처럼 **시술 과정의 상대적인 효율이나 맥락**을 표현하려는 시도가 포함되어 있습니다.

### 3. 서로 다른 모델군 비교

단일 boosting 모델만 보는 대신 다음 모델을 같은 연구 흐름 안에서 비교합니다.

```text
Logistic Regression
Decision Tree
Random Forest
CatBoost
LightGBM
XGBoost
```

초기 hold-out 비교 뒤에는 주요 boosting 모델을 5-Fold OOF 구조로 다시 평가합니다.

### 4. 5-Fold OOF 검증

Notebook에 기록된 5-Fold OOF 결과는 다음과 같습니다.

| Model | OOF ROC-AUC | LogLoss |
|---|---:|---:|
| CatBoost | `0.740085` | `0.586472` |
| LightGBM | `0.739635` | `0.586282` |
| XGBoost | `0.740039` | `0.586374` |

이 값들은 **이 Notebook 내부 실험 계약의 결과**이며, 공식 발표의 제출 AUC 또는 다른 Notebook의 OOF와 동일 조건이라고 가정하지 않습니다.

### 5. Weighted / Rank Ensemble 탐색

세 boosting 모델의 OOF prediction을 이용해 단일 모델을 넘어선 앙상블도 비교합니다.

Notebook에서 확인되는 대표 결과는 다음과 같습니다.

| Strategy | Weight | OOF ROC-AUC |
|---|---|---:|
| 3-model weighted | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740377` |
| 3-model rank | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740384` |

Rank Average와 raw probability ensemble을 다시 혼합하는 hybrid 실험까지 이어지며, 현재 출력에서는 Rank 기반 조합이 가장 높은 OOF ROC-AUC를 기록합니다.

---

## 🧭 Relationship to the Official Plan 3

공식 프로젝트의 최종 발표 기록은 다음과 같이 구분합니다.

```text
Highest submitted AUC : Plan 2 — 0.74232
Final adopted model   : Plan 3 — 0.74231
```

공식 최종 3안은 `OOF + Multi-Seed` 기반 일반화 전략으로 정리되어 있습니다. 이 BS Notebook은 **OOF 기반 CatBoost/LightGBM/XGBoost 비교와 Weighted/Rank Ensemble 연구라는 점에서 3안 계보를 이해하는 데 의미가 있는 자료**입니다.

다만 현재 Notebook에서 확인되는 내부 최고 OOF는 약 `0.740384`이고, Notebook 자체만으로는 공식 최종 3안 artifact와의 byte-level identity 또는 완전한 실행 계보를 증명할 수 없습니다.

따라서 이 저장소에서는 다음 원칙을 사용합니다.

```text
3안 관련 연구 기록
≠
공식 Final 3안 canonical artifact
```

공식 결론과 artifact identity는 반드시 [`nanimnoworry/PSP`](https://github.com/nanimnoworry/PSP)를 기준으로 확인합니다.

---

## 🤝 Research Credit & Collaboration

이 저장소는 발표자료상 **박빛샘 연구원의 작업 공간**과 연결되어 있으며 Notebook 실행 metadata에서도 해당 작업 흔적을 확인할 수 있습니다.

그러나 난임 프로젝트의 연구는 역할별로 완전히 독립된 세 개의 연구를 합친 형태가 아니라, 팀이 아이디어·실험·검증·발표를 함께 발전시킨 협업 연구였습니다.

따라서 credit은 다음처럼 해석합니다.

- **Workspace association**: 박빛샘 연구원
- **Research context**: 난임걱정마삼조 팀 프로젝트
- **Modeling / validation / interpretation**: 팀 협업
- **Official final SSOT**: `nanimnoworry/PSP`

개별 저장소의 위치나 Notebook 실행 계정이 전체 연구의 단독 저작권·단독 기여를 의미하지 않습니다.

---

## 🗂️ Related Repositories

| Repository | 역할 |
|---|---|
| **[`PSP`](https://github.com/nanimnoworry/PSP)** | **공식 프로젝트 허브 · 최종 제출/발표 SSOT** |
| **`BS`** | 박빛샘 연구원과 연결된 모델링 contributor workspace · 3안 관련 연구 기록 |
| [`planB`](https://github.com/nanimnoworry/planB) | 공식 제출 이후의 추가 모델 연구 · robustness / falsification |
| [`Research-Papers`](https://github.com/nanimnoworry/Research-Papers) | 임상·문헌 근거 · reference · 발표자료 archive |

### Recommended reading order

1. [`PSP`](https://github.com/nanimnoworry/PSP) — 프로젝트 전체와 공식 최종 결과
2. 이 저장소의 `3안 모델.ipynb의 사본` — 모델 비교·OOF·앙상블 연구 흐름
3. [`PSP/docs/model_lineage.md`](https://github.com/nanimnoworry/PSP/blob/main/docs/model_lineage.md) — 공식 1안 → 2안 → 3안 계보
4. [`planB`](https://github.com/nanimnoworry/planB) — post-submission 연구
5. [`Research-Papers`](https://github.com/nanimnoworry/Research-Papers) — 임상·문헌·발표 근거

---

## 📐 Record Policy

- 파일명보다 **artifact identity와 실행 계보**를 우선합니다.
- hold-out, OOF, Public 제출 AUC를 같은 지표처럼 섞지 않습니다.
- 서로 다른 split·seed·feature contract의 작은 점수 차이를 직접 순위로 해석하지 않습니다.
- 개인 workspace와 팀 전체 연구 contribution을 구분합니다.
- 모델의 feature importance나 예측 결과를 임상적 인과관계로 과도하게 해석하지 않습니다.
- 이 저장소의 결과는 연구·교육 목적이며 실제 의료 판단이나 임상 의사결정을 대체하지 않습니다.

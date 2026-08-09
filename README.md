<div align="center">

# 🧬 BS — Fertility PSP Research Workspace

### 난임 환자 대상 임신 성공 여부 예측 · 3안 관련 모델링 연구

<p>
  <img src="https://img.shields.io/badge/Task-Binary%20Classification-2563EB?style=flat-square" alt="Binary Classification" />
  <img src="https://img.shields.io/badge/Metric-ROC--AUC-7C3AED?style=flat-square" alt="ROC-AUC" />
  <img src="https://img.shields.io/badge/Validation-5--Fold%20OOF-0891B2?style=flat-square" alt="5-Fold OOF" />
  <img src="https://img.shields.io/badge/Models-CatBoost%20%7C%20LightGBM%20%7C%20XGBoost-059669?style=flat-square" alt="Models" />
</p>

</div>

`BS` 리포는 난임 예측 프로젝트의 **모델 비교 · OOF 검증 · 앙상블 연구 기록**을 보존합니다. 공식 최종 제출·발표 계보의 기준은 [`nanimnoworry/PSP`](https://github.com/nanimnoworry/PSP)입니다.

---

## 🎯 Research Scope

현재 핵심 Notebook:

```text
3안 모델.ipynb의 사본
```

주요 연구 범위:

- 데이터 구조 및 결측 패턴 확인
- 시술 맥락 기반 조합·비율 Feature Engineering
- Logistic Regression / Decision Tree / Random Forest 비교
- CatBoost / LightGBM / XGBoost 5-Fold OOF 검증
- Weighted / Rank Ensemble 탐색

---

## 🧪 Data & Modeling

Notebook 기록 기준:

```text
Train : 256,351 rows × 69 columns
Test  :  90,067 rows × 68 columns
Target: 임신 성공 여부
Metric: ROC-AUC
```

대표 파생 변수:

```text
treatment_x_specific_proc
age_x_specific_proc
transfer_per_created_embryo
stored_per_created_embryo
mixed_per_fresh_oocyte
icsi_oocyte_rate
```

배아 생성·이식·저장, 난자 혼합·미세주입 등 시술 과정의 상대적 효율과 맥락을 표현하는 변수를 실험했습니다.

---

## 📊 OOF Results

| Model | OOF ROC-AUC | LogLoss |
|---|---:|---:|
| CatBoost | `0.740085` | `0.586472` |
| LightGBM | `0.739635` | `0.586282` |
| XGBoost | `0.740039` | `0.586374` |

위 값은 **BS Notebook 내부 실험 계약의 결과**이며, 공식 제출 AUC 또는 다른 Notebook의 OOF와 직접 동일 조건으로 비교하지 않습니다.

### Ensemble

| Strategy | Weight | OOF ROC-AUC |
|---|---|---:|
| 3-model weighted | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740377` |
| 3-model rank | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740384` |

Rank Average와 raw probability ensemble을 혼합하는 hybrid 실험도 포함합니다.

---

## 🧭 Official Model Relationship

공식 발표 결과:

```text
Highest submitted AUC : Plan 2 — 0.74232
Final adopted model   : Plan 3 — 0.74231
```

BS 리포는 **OOF 기반 CatBoost / LightGBM / XGBoost 비교와 Weighted / Rank Ensemble 연구**를 통해 3안 계보를 이해하는 자료입니다.

```text
BS 3안 관련 연구 기록
≠
공식 Final Plan 3 canonical artifact
```

공식 artifact identity와 최종 계보는 [`PSP`](https://github.com/nanimnoworry/PSP)를 기준으로 확인합니다.

---

## 🤝 Research Credit

- **Workspace association:** 박빛샘 연구원
- **Research context:** 난임걱정마삼조 팀 프로젝트
- **Modeling / validation / interpretation:** 팀 협업
- **Official final SSOT:** `nanimnoworry/PSP`

---

## 🗂️ Related Repositories

| Repository | 역할 |
|---|---|
| **[`PSP`](https://github.com/nanimnoworry/PSP)** | **공식 프로젝트 허브 · 최종 제출/발표 SSOT** |
| **`BS`** | 모델링 contributor workspace · 3안 관련 연구 기록 |
| [`planB`](https://github.com/nanimnoworry/planB) | 공식 제출 이후의 추가 모델 연구 · robustness / falsification |
| [`Research-Papers`](https://github.com/nanimnoworry/Research-Papers) | 임상·문헌 근거 · reference · 발표자료 archive |

---

## 📐 Record Policy

- 파일명보다 **artifact identity와 실행 계보**를 우선합니다.
- hold-out, OOF, Public 제출 AUC를 구분합니다.
- 서로 다른 split·seed·feature contract의 작은 점수 차이를 직접 순위로 해석하지 않습니다.
- 개인 workspace와 팀 전체 연구 contribution을 구분합니다.
- feature importance나 예측 결과를 임상적 인과관계로 과도하게 해석하지 않습니다.
- 연구 결과는 실제 의료 판단이나 임상 의사결정을 대체하지 않습니다.

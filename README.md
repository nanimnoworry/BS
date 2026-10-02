<picture>
  <source media="(max-width: 640px)" srcset="./docs/assets/readme/hero-mobile.svg" />
  <img src="./docs/assets/readme/hero.svg" width="100%" alt="BS OOF model bench for Fertility PSP research" />
</picture>

<h1 align="center">BS — Fertility PSP Research Workspace</h1>

<p align="center">
  <strong>Plan 3 연계 모델 비교 · 5-Fold OOF · Weighted / Rank Ensemble</strong><br />
  Public modeling workspace · not the official final artifact
</p>

## Start Here

이 저장소는 **Plan 3 연계 모델 비교와 OOF ensemble 연구를 기록하는 public workspace** 입니다.

- **공식 프로젝트 SSOT / 최종 결과** — [nanimnoworry/PSP](https://github.com/nanimnoworry/PSP)
- **Organization overview** — [nanimnoworry](https://github.com/nanimnoworry)
- **이 저장소의 Notebook** — [plan3_model_research.ipynb](plan3_model_research.ipynb)

> 공식 최종 결과·제출 계보를 확인하려면 PSP부터 읽으세요. BS의 Notebook은 공식 final artifact를 대체하지 않습니다.

## Research Scope

주요 연구 범위:

- 데이터 구조와 결측 패턴
- 시술 맥락 기반 조합·비율 변수
- Logistic Regression · Decision Tree · Random Forest
- CatBoost · LightGBM · XGBoost 5-Fold OOF
- 3-model Weighted / Rank Ensemble

Notebook 기준 데이터 구조는 Train **256,351 × 69**, Test **90,067 × 68**, 공식 지표는 ROC-AUC입니다.

## OOF Model Bench

<picture>
  <source media="(max-width: 640px)" srcset="./docs/assets/readme/model-bench-mobile.svg" />
  <img src="./docs/assets/readme/model-bench.svg" width="100%" alt="OOF comparison of CatBoost LightGBM and XGBoost" />
</picture>

개별 모델 결과는 **이 Notebook의 split · seed · 전처리 조건 안에서만 비교**합니다.

- **CatBoost** — OOF ROC-AUC 0.740085 · LogLoss 0.586472
- **LightGBM** — OOF ROC-AUC 0.739635 · LogLoss 0.586282
- **XGBoost** — OOF ROC-AUC 0.740039 · LogLoss 0.586374

## Ensemble Evidence

<picture>
  <source media="(max-width: 640px)" srcset="./docs/assets/readme/ensemble-evidence-mobile.svg" />
  <img src="./docs/assets/readme/ensemble-evidence.svg" width="100%" alt="Weighted and rank ensemble OOF comparison with model weights" />
</picture>

공통 가중치는 CatBoost **0.45** · LightGBM **0.20** · XGBoost **0.35**입니다.

- **3-model weighted ensemble** — OOF ROC-AUC **0.740377**
- **3-model rank ensemble** — OOF ROC-AUC **0.740384**

Rank 기반 조합은 ROC-AUC와 확률 calibration 특성이 다를 수 있으므로 LogLoss 해석과 분리해서 봅니다.

## Feature Work

Notebook에서 다룬 주요 파생 변수 예시:

<pre>
treatment_x_specific_proc
age_x_specific_proc
transfer_per_created_embryo
stored_per_created_embryo
mixed_per_fresh_oocyte
icsi_oocyte_rate
</pre>

구조적 결측과 시술 맥락을 단순한 일괄 대치보다 먼저 해석하는 방향은 PSP의 연구 원칙과 연결됩니다.

## Relationship to Official Result

BS는 **공식 3안과 관련된 모델링 연구 기록**이지만, BS Notebook 자체가 공식 최종 3안 artifact라는 뜻은 아닙니다.

- 공식 최고 제출: **2안 · 0.74232**
- 공식 최종 채택 submission model: **3안 · 0.74231**
- BS: CatBoost / LightGBM / XGBoost OOF 및 Weighted / Rank ensemble 연구 workspace
- 공식 계보와 canonical artifact identity: [PSP](https://github.com/nanimnoworry/PSP)

## Public Notebook Boundary

Default branch의 public Notebook은 code-cell output과 execution count를 제거한 sanitized 상태로 관리합니다. Source/current blob provenance는 [PSP Public Notebook Sanitization Record](https://github.com/nanimnoworry/PSP/blob/main/docs/PUBLIC_NOTEBOOK_SANITIZATION.md)를 기준으로 확인할 수 있습니다.

**Historical filename:** 3안 모델.ipynb의 사본  
현재 public filename: **plan3_model_research.ipynb**

파일명 정리는 내용 정체성을 바꾸기 위한 것이 아니며, 공개 Notebook boundary와 provenance를 명확히 하기 위한 정리입니다.

## Related Repositories

- [PSP](https://github.com/nanimnoworry/PSP) — 공식 프로젝트 · 최종 결과 · 모델 계보 · artifact provenance
- planB *(private)* — 공식 제출 이후 후속 모델 연구
- Research-Papers *(private)* — 임상·문헌 근거 · 발표자료 provenance

**Scope boundary:** 해커톤·연구 결과이며 실제 의료 환경의 임상 검증, 진단 또는 의사결정 성능을 주장하지 않습니다. **Not a clinical diagnostic or medical decision system.**

---

### License and Rights

**Public view · no public reuse license.**  
Notebook 원천 데이터 · 내장 출력 · 의존 라이브러리 · 제3자 자료는 각 권리·조건을 따릅니다.

[LICENSE](LICENSE) · [RIGHTS.md](RIGHTS.md) · [CONTRIBUTORS.md](CONTRIBUTORS.md)

<div align="center">

# BS — Fertility PSP Research Workspace

### 난임 환자 대상 임신 성공 여부 예측 · 3안 관련 모델링 연구

<p>
  <img src="https://img.shields.io/badge/Task-Binary%20Classification-2563EB?style=flat-square" alt="Binary Classification" />
  <img src="https://img.shields.io/badge/Metric-ROC--AUC-7C3AED?style=flat-square" alt="ROC-AUC" />
  <img src="https://img.shields.io/badge/Validation-5--Fold%20OOF-0891B2?style=flat-square" alt="5-Fold OOF" />
</p>

</div>

3안 연계 모델 비교 · OOF 검증 · Weighted/Rank Ensemble  
공식 최종 결과·제출 계보: [`PSP`](https://github.com/nanimnoworry/PSP)

## Notebook

```text
3안 모델.ipynb의 사본
```

**범위**
- 데이터 구조 · 결측 패턴
- 시술 맥락 기반 조합/비율 변수
- Logistic Regression · Decision Tree · Random Forest
- CatBoost · LightGBM · XGBoost 5-Fold OOF
- Weighted / Rank Ensemble

## 데이터와 파생 변수

**Notebook 기준:** Train `256,351 × 69` · Test `90,067 × 68` · ROC-AUC

```text
treatment_x_specific_proc
age_x_specific_proc
transfer_per_created_embryo
stored_per_created_embryo
mixed_per_fresh_oocyte
icsi_oocyte_rate
```

## OOF 결과

| Model | OOF ROC-AUC | LogLoss |
|---|---:|---:|
| CatBoost | `0.740085` | `0.586472` |
| LightGBM | `0.739635` | `0.586282` |
| XGBoost | `0.740039` | `0.586374` |

| Strategy | Weight | OOF ROC-AUC |
|---|---|---:|
| 3-model weighted | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740377` |
| 3-model rank | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740384` |

**비교 범위:** 해당 Notebook의 split · seed · 전처리 조건. 타 Notebook OOF·제출 점수와 직접 비교 제외.

## 공식 3안과의 관계

- 최고 제출: **2안 · `0.74232`**
- 최종 채택: **3안 · `0.74231`**
- BS Notebook: CatBoost · LightGBM · XGBoost OOF 및 Weighted/Rank Ensemble 연구 기록
- BS Notebook ≠ 공식 최종 3안 artifact
- contributor 작업 공간 기반 팀 협업 기록

## Related Repositories

| Repository | 범위 |
|---|---|
| [`PSP`](https://github.com/nanimnoworry/PSP) | 공식 프로젝트 · 최종 제출/발표 · 모델 계보 |
| `planB` | 공식 발표 이후 후속 모델 연구 |
| `Research-Papers` | 임상·문헌 근거 · 발표자료 아카이브 |

**용도 제한:** 임상 의사결정용 모델 아님.

---

## License and Rights

**Public view · no public reuse license.**  
Notebook 원천 데이터·내장 출력·의존 라이브러리·제3자 자료는 각 권리·조건 적용.

[LICENSE](LICENSE) · [RIGHTS.md](RIGHTS.md) · [CONTRIBUTORS.md](CONTRIBUTORS.md)

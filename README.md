<div align="center">

# BS — Fertility PSP Research Workspace

### 난임 환자 대상 임신 성공 여부 예측 · 3안 관련 모델링 연구

<p>
  <img src="https://img.shields.io/badge/Task-Binary%20Classification-2563EB?style=flat-square" alt="Binary Classification" />
  <img src="https://img.shields.io/badge/Metric-ROC--AUC-7C3AED?style=flat-square" alt="ROC-AUC" />
  <img src="https://img.shields.io/badge/Validation-5--Fold%20OOF-0891B2?style=flat-square" alt="5-Fold OOF" />
</p>

</div>

`BS` 리포는 3안과 연결된 모델 비교, OOF 검증, 앙상블 실험을 담고 있습니다. 프로젝트의 공식 최종 결과와 제출 계보는 [`PSP`](https://github.com/nanimnoworry/PSP)를 기준으로 합니다.

## Notebook

```text
3안 모델.ipynb의 사본
```

Notebook에서 다룬 내용은 다음과 같습니다.

- 데이터 구조와 결측 패턴 확인
- 시술 맥락을 반영한 조합·비율 변수 생성
- Logistic Regression, Decision Tree, Random Forest 비교
- CatBoost, LightGBM, XGBoost 5-Fold OOF 검증
- Weighted / Rank Ensemble 비교

## 데이터와 파생 변수

Notebook 기록 기준 데이터 크기는 Train `256,351 × 69`, Test `90,067 × 68`이며 평가지표는 ROC-AUC입니다.

대표적으로 다음 변수를 추가해 시술 과정의 조합과 비율을 표현했습니다.

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

세 모델의 OOF prediction을 이용한 앙상블 결과는 다음과 같습니다.

| Strategy | Weight | OOF ROC-AUC |
|---|---|---:|
| 3-model weighted | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740377` |
| 3-model rank | Cat `0.45` · LGB `0.20` · XGB `0.35` | `0.740384` |

이 점수들은 이 Notebook의 실험 조건에서 계산한 값입니다. 다른 Notebook의 OOF나 제출 점수와 동일 조건이라고 가정하지 않습니다.

## 공식 3안과의 관계

최종 발표 기준 최고 제출 점수는 2안 `0.74232`, 최종 채택 모델은 3안 `0.74231`입니다.

BS Notebook은 CatBoost·LightGBM·XGBoost의 OOF 비교와 Weighted / Rank Ensemble 과정을 담고 있어 3안의 연구 흐름을 이해하는 데 도움이 됩니다. 다만 이 Notebook 자체를 공식 최종 3안 artifact와 동일한 파일로 보지는 않습니다.

발표자료상 contributor별 작업 공간 중 하나였으며, 모델링과 검증은 팀 협업으로 진행했습니다.

## Related Repositories

| Repository | 내용 |
|---|---|
| [`PSP`](https://github.com/nanimnoworry/PSP) | 공식 프로젝트, 최종 제출·발표, 모델 계보 |
| `planB` | 공식 발표 이후의 추가 모델 연구 |
| `Research-Papers` | 임상·문헌 근거와 발표자료 아카이브 |

연구 결과는 실제 의료 판단이나 임상 의사결정을 위한 모델이 아닙니다.

---

## License and Rights

이 공개 저장소는 포트폴리오·연구 검토를 위해 열람할 수 있지만 오픈소스로 배포하지 않습니다. Notebook의 원천 데이터·내장 출력, 의존 라이브러리와 제3자 자료는 이 저장소가 재라이선스하지 않습니다.

자세한 내용은 [LICENSE](LICENSE), [RIGHTS.md](RIGHTS.md), [CONTRIBUTORS.md](CONTRIBUTORS.md)를 확인하세요.

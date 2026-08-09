# BS Public Release Audit

> Reviewed: 2026-08-09  
> Status: **NOT READY TO PUBLISH AS-IS**

This audit reviews the current `nanimnoworry/BS` contributor workspace before any visibility change. The repository is associated with 박빛샘 연구원의 작업 공간, while the project research itself is documented as a team collaboration.

## Scope reviewed

Current repository contents:

```text
3안 모델.ipynb의 사본
README.md
```

Current notebook Git blob:

```text
5f3352bcf8ff1d326e6cbb532e5fc4d4b78285b6
```

The notebook is a meaningful modeling record: it covers model comparison, 5-Fold OOF validation, CatBoost/LightGBM/XGBoost experiments, and weighted/rank ensemble exploration. The issue is not research value; it is public-release hygiene.

## Findings

### Colab account metadata

The notebook contains Colab execution metadata with the display name `박빛샘` and a numeric Colab `userId`. It also contains Colab authorship/execution metadata that is not necessary for a public technical portfolio.

The public version should remove account-linked execution metadata while preserving research credit in human-readable documentation.

### Personal/local data path

The notebook contains a hard-coded Google Drive path similar to:

```text
/content/drive/MyDrive/ai_health_care_5/7. 프로젝트 2/train.csv
```

This is not needed for reproducibility outside the original Colab session. A sanitized notebook should use a generic path contract such as `DATA_DIR` / `../data` and document that the dataset must be supplied separately under its own access terms.

### Rendered competition-data rows

Notebook output includes sample rows from the training dataset, including IDs such as `TRAIN_000000` and associated feature values.

Competition-data redistribution permission has not been verified in this audit. Therefore those rendered outputs should be removed from any public copy unless the official terms explicitly allow redistribution.

### Credentials

Direct inspection did not find obvious `api_key`, `password`, or `sk-`-style credential signatures in the current notebook. This does not replace a full secret scan, but no obvious credential leak was found in the material reviewed.

### License

The repository currently has no declared license. If a sanitized public version is published, the team should choose a license for its own code/documentation without implying rights over the competition dataset or third-party materials.

### Naming and portfolio polish

The current file name `3안 모델.ipynb의 사본` is valuable as historical provenance but is not ideal as a public-facing canonical filename. The private original should stay untouched; a public sanitized copy can use a stable name such as:

```text
plan3_modeling_research.ipynb
```

## Recommended sanitization

For a public copy:

- clear rendered raw/sample training rows
- remove Colab `executionInfo.user`, numeric `userId`, `authorship_tag`, and other account-specific metadata
- replace personal Google Drive paths with a generic data-path contract
- retain aggregate metrics and research methodology where redistribution rules allow
- retain team/contributor credit in README rather than notebook account metadata
- use a clean public-facing notebook filename
- add `.gitignore` and an intentional license
- do not copy the private repository's Git history into the public showcase

## Research-credit boundary

The public documentation should preserve the current credit model:

- **Workspace association:** 박빛샘 연구원
- **Research context:** 난임걱정마삼조 team project
- **Modeling / validation / interpretation:** team collaboration
- **Official final SSOT:** `nanimnoworry/PSP`

The notebook filename or execution account must not be presented as evidence that the whole project was a single-person research effort.

## Official-model boundary

This notebook is meaningful evidence for the Plan 3 research lineage, but it is **not proven to be byte-identical to the official final Plan 3 canonical artifact**.

Keep the distinction:

```text
3안 related modeling research
≠
official Final Plan 3 canonical artifact
```

## Decision

```text
DIRECT_PUBLIC_SWITCH = BLOCKED_FOR_NOW
PRIVATE_PROVENANCE_REPO = KEEP
SANITIZED_PUBLIC_COPY = RECOMMENDED
```

No repository visibility was changed by this audit.

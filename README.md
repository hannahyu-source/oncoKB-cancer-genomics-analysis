# OncoKB™ Cancer Genomics Analysis Dashboard

**OncoKB Cancer Gene List**를 기반으로, 특정 유전자·변이·암종을 입력하면 생성형 AI(Gemini)가 임상적 의의를 정리한 리포트를 생성해 주는 정밀 종양학(Precision Oncology) 분석 대시보드입니다. 순수 프론트엔드(단일 HTML 파일)로 동작하며 별도 서버 없이 GitHub Pages에서 바로 실행됩니다.

🔗 **라이브 데모(GitHub Pages):** https://hannahyu-source.github.io/oncoKB-cancer-genomics-analysis/

> ⚠️ **면책 조항**: 본 프로젝트는 학습·연구 목적의 데모입니다. 생성된 리포트는 AI가 공개된 유전자 목록과 일반 지식을 바탕으로 작성한 참고 자료일 뿐이며, 실제 임상 진단이나 치료 결정에 사용해서는 안 됩니다. OncoKB는 Memorial Sloan Kettering Cancer Center(MSK)가 운영하는 지식 베이스이며, "OncoKB"는 MSK의 상표입니다. 데이터를 활용할 때는 [OncoKB 이용 약관](https://www.oncokb.org)을 확인하세요.

---

## 주요 기능

### I. OncoKB Knowledge Resource
OncoKB가 어떤 지식 베이스인지, 어떤 패널·데이터 소스를 통합하는지 소개하는 섹션입니다.

### II. OncoKB Cancer Gene List
- OncoKB Cancer Gene List에 포함된 **총 1,236개 유전자**를 표로 탐색
- 유전자 기호(Symbol) 또는 별칭(Aliases)으로 검색
- 유전자별 다음 속성 확인 가능
  - `type`: Oncogene(종양유전자) / TSG(종양억제유전자)
  - `annotated`: OncoKB 주석 여부
  - `impact`: MSK-IMPACT 패널 포함 여부
  - `heme`: MSK-HEME 패널 포함 여부
  - `f1` / `f1h`: FoundationOne / FoundationOne Heme 패널 포함 여부
  - `vogelstein`: Vogelstein et al. 암 유전자 목록 포함 여부
  - `cosmic`: COSMIC Cancer Gene Census 포함 여부
  - `sources`: 해당 유전자를 포함하는 데이터 소스 개수
- 전체 유전자 수 / Oncogenic 유전자 수 / Tumor Suppressor 유전자 수 요약 통계 표시

### III. Variant Prioritization Engine
1. 목록에서 유전자를 선택
2. 단백질 변이(Protein Change, HGVSp — 예: `V600E`)와 암종(Tumor Type — 예: `Melanoma`)을 입력
3. 자신의 **Gemini API 키**를 입력해 AI 분석 리포트 생성
4. 아래 구조의 리포트를 마크다운으로 렌더링
   - 유전자의 생물학적 기전
   - 임상 패널 및 OncoKB 주석의 의의
   - Therapeutic Implications (치료적 함의)
   - 추가 DB 교차 분석 및 종합 결론
5. 생성된 리포트를 PDF로 내보내기(export) 가능

## 데이터 및 사용 기술

| 항목 | 내용 |
|---|---|
| 유전자 데이터 | OncoKB Cancer Gene List (유전자 1,236종, `index.html`에 정적으로 임베드) |
| AI 리포트 생성 | Google **Gemini 2.5 Flash** API (`generativelanguage.googleapis.com`) |
| 마크다운 렌더링 | [marked.js](https://github.com/markedjs/marked) |
| PDF 내보내기 | [html2pdf.js](https://github.com/eKoopmans/html2pdf.js) |
| 아이콘 | Font Awesome |
| 배포 | GitHub Actions(`.github/workflows/static.yml`) → GitHub Pages |

## 사용 방법 (로컬/데모 공통)

1. https://hannahyu-source.github.io/oncoKB-cancer-genomics-analysis/ 접속 (또는 `index.html`을 브라우저로 직접 열기)
2. **Gemini API Key** 입력란에 본인의 [Google AI Studio](https://aistudio.google.com/) API 키를 붙여넣기
3. 유전자 검색창에서 분석할 유전자를 선택
4. Protein Change / Tumor Type 입력 후 리포트 생성

> API 키는 브라우저에서 Google Gemini API로 **직접** 전송되며, 별도의 백엔드 서버를 거치지 않습니다. 다만 키가 브라우저(로컬 저장소)에 남으므로, 공용 컴퓨터에서는 사용 후 키를 삭제하는 것을 권장합니다.

## 저장소 구조

```
.
├── index.html                  # 대시보드 전체 (단일 파일, 유전자 데이터 임베드)
├── .github/workflows/static.yml  # GitHub Pages 배포 워크플로우
└── README.md
```

## 출처

- [OncoKB — Precision Oncology Knowledge Base](https://www.oncokb.org) (Memorial Sloan Kettering Cancer Center)
- [MSK-IMPACT](https://www.mskcc.org/msk-impact)
- Vogelstein et al., *Cancer Genome Landscapes*, Science (2013) — [DOI](https://www.science.org/doi/10.1126/science.1235122)
- [COSMIC Cancer Gene Census](https://cancer.sanger.ac.uk/cosmic/login)

---

## AI-Assisted Development

이 프로젝트의 구현(코드 작성, 리팩터링, 디버깅, 문서화)에는 Claude Code의 도움을 받았습니다. 대시보드 내에서 리포트를 생성하는 Gemini API 연동은 최종 사용자가 유전자를 조회할 때 실행되는 애플리케이션 기능이며, 위 개발 지원과는 별개입니다.
연구 질문 설정, 생물학적 해석, 검증 전략, 과학적 한계에 대한 판단은 프로젝트 저자가 직접 검토하고 결정했습니다.

---

## Genomics Portfolio Series

이 저장소는 4부작 유전체 포트폴리오 중 하나입니다.

01. **Family Genome × KEGG Integration** — [kegg-family-genome-analysis](https://github.com/hannahyu-source/kegg-family-genome-analysis)
02. **Genomic Variant Machine Learning** — [genomic-variant-ML-analysis](https://github.com/hannahyu-source/genomic-variant-ML-analysis)
03. **Family-of-Five Genome Dataset** — [family-genome-analysis](https://github.com/hannahyu-source/family-genome-analysis)
04. **OncoKB Cancer Genomics Analysis** — [oncoKB-cancer-genomics-analysis](https://github.com/hannahyu-source/oncoKB-cancer-genomics-analysis) ← 현재 저장소

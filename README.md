# MLB 심판의 스트라이크 판정은 무엇에 흔들리는가

ABS(자동 볼·스트라이크 판정) 도입 이전 MLB 심판의 볼/스트라이크 판정이
투구 위치 외의 요인에 얼마나 좌우되었는지 분석한다. 2024-2025 시즌
Statcast 투구 데이터를 사용한다.

데이터 사이언스 튜토리얼 형식으로, 데이터 수집부터 정제, 탐색적 분석,
가설 검정, 머신러닝, 결론까지 전 과정을 다룬다.

**튜토리얼 보기: https://haeram7.github.io/strikezone-lab/**

---

## 다루는 질문

심판은 같은 위치의 공을 상황에 따라 다르게 판정하는가?

- **상황 요인** — 볼카운트, 아웃 수, 점수 차, 주자 상황
- **선수 요인** — 투수·타자의 평판과 성향

스트라이크 존 경계에 걸친 공만 추려, 투구 위치를 통제한 뒤 두 요인군의
영향을 비교한다.

## 데이터

| | |
|---|---|
| 출처 | [Baseball Savant (Statcast)](https://baseballsavant.mlb.com/statcast_search), [pybaseball](https://github.com/jldbc/pybaseball) |
| 시즌 | 2024-2025 정규시즌 |
| 대상 | 타자가 스윙하지 않은 판정구 |
| 보조 자료 | [Catcher Framing 리더보드](https://baseballsavant.mlb.com/leaderboard/catcher-framing) |

2026년은 ABS 도입으로 스트라이크 존 정의와 측정 기준이 바뀌어 제외했다.

## 구성

```
notebooks/
├── 00_data.ipynb        수집·정제
├── 01_baseline.ipynb    기준 모델, 탐색적 분석
├── 02_situation.ipynb   상황 요인 분석
├── 03_player.ipynb      선수 요인 분석
└── final.ipynb          합본 (index.html의 원본)

data/
├── clean.parquet        정제된 투구 데이터
└── player_groups.csv    선수 그룹 명단

models/
└── baseline.json        기준 모델 계수
```

작업 규칙과 변수 정의는 [GUIDELINE.md](GUIDELINE.md)에 있다.

## 재현 방법

```bash
pip install -r requirements.txt
```

`data/clean.parquet`이 레포에 포함되어 있으므로 `01_baseline.ipynb`부터
바로 실행할 수 있다. 데이터를 처음부터 수집하려면 `00_data.ipynb`를
실행한다 (Statcast 다운로드에 시간이 걸린다).

## 참고 문헌

- Green & Daniels, [*What Does it Take to Call a Strike? Three Biases in Umpire Decision Making*](https://www.sloansportsconference.com/research-papers/what-does-it-take-to-call-a-strike-three-biases-in-umpire-decision-making), MIT Sloan Sports Analytics Conference
- Kim & King, [*Seeing Stars: Matthew Effects and Status Bias in Major League Baseball Umpiring*](https://homepage.divms.uiowa.edu/~dzimmer/sports-statistics/kimandking.pdf), Management Science 60(11), 2014
- [*Bayesian sensory integration explains ball-count bias in MLB umpires*](https://www.nature.com/articles/s44271-026-00534-4), Communications Psychology, 2026
- [*The psychophysics of home plate umpire calls*](https://www.nature.com/articles/s41598-024-52402-y), Scientific Reports, 2024

## 팀

- 이름 — 상황 요인
- 이름 — 선수 요인

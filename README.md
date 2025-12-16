Kyungpook National University July 2024 hlmando indian internship

<img width="1414" height="2000" alt="image" src="https://github.com/user-attachments/assets/99635df5-9a9b-4546-912e-d2a43a756dc0" />

# AUTOSAR LED Blink (S32K146) — AUTOSAR vs Non-AUTOSAR 비교 구현

![LED Blinking with AUTOSAR](LED%20Blinking%20with%20Autosar.png)

- **기간**: 2024.07 ~ 2024.08  
- **구분**: HL만도 인도 인턴십 과제 
- **Repo**: https://github.com/Seoyoungeun/autosar/tree/main  

---

## 프로젝트 요약
차량 SW 환경에서 **Non-AUTOSAR(레지스터 직접 제어)** 방식과 **AUTOSAR(표준화된 설정/코드 생성 기반)** 방식으로  
**LED Blinking 기능을 구현·비교**하며, AUTOSAR의 개발 흐름(**Configure → Generate → Implement → Verify**)을 학습했습니다.

- **요구사항**: 스위치를 **한 번 누르면(토글)** LED가 **5초 간격으로 점멸 시작**, 다시 누르면 점멸 정지

---

## 내 역할
- 제공받은 **샘플 코드**를 요구사항(토글 + 5초 주기 점멸)에 맞게 수정
- **EB tresos**에서 Port/DIO 등 설정을 구성하고 Generate 산출물 기반으로 동작을 검증
- Non-AUTOSAR ↔ AUTOSAR 차이를 비교/정리(왜 AUTOSAR를 쓰는지 포함)

---

## Tech / Tools
- **MCU Board**: NXP **S32K146 EVB**
- **AUTOSAR Tool**: **EB tresos**
- **Non-AUTOSAR**: C (레지스터 직접 제어 기반 샘플 코드 수정)

---

## 하드웨어 설정(예시)
| 구분 | Pin | Device |
|---|---|---|
| Input | **PTC13** | **SW3** |
| Output | **PTD15** | **Red LED** |

---

## 핵심 구현
### Non-AUTOSAR
- 스위치 입력을 기반으로 **토글 상태(state)** 를 유지
- 토글 ON 상태에서 **5초 주기 점멸(LED toggle)** 로직이 동작하도록 샘플 코드 수정

### AUTOSAR
- EB tresos에서 **Port/DIO 설정**으로 LED/Switch 핀 매핑 구성 → **Generate**
- 생성된 구조 위에서 스위치 입력에 따른 **토글 상태 전환 + 5초 점멸** 로직이 동작하도록 샘플 코드 수정
- “표준 설정/생성 + 애플리케이션 로직”으로 역할이 분리되는 구조를 경험

---

## 문제 해결 과정 (Problem → Cause → Fix → Result)
### Problem 1
**코드만 수정해서는 AUTOSAR 프로젝트가 원하는대로 동작하지 않음**

- **Cause**: AUTOSAR는 코드 작성 이전에 **설정(Configure) → 생성(Generate)** 단계가 필수이며, 이 산출물이 런타임 동작을 좌우
- **Fix**: (1) EB tresos 설정 고정 → (2) Generate → (3) 샘플 코드 수정(토글/주기) → (4) 검증 순서로 절차를 단계화
- **Result**: 실패 원인을 단계별로 좁히는 방식으로, **재현 가능한 개발/검증 루틴**을 확보

### Problem 2
**회사/프로젝트마다 규격이 달라지면 재사용/협업 비용이 증가**

- **Fix**: AUTOSAR 표준 구조 위에서 동일 요구사항을 구현·비교하며, “왜 AUTOSAR를 쓰는가”를 개발 관점에서 정리
- **Result**: AUTOSAR는 기능 구현을 넘어, 자동차 회사마다 다른 코드 규격을 **표준으로 통일**해 유지보수성과 협업 효율을 높이기 위한 기반임을 체감

---

## 배운 점
- AUTOSAR의 핵심은 코드 자체보다 **Configure → Generate → Implement → Verify** 흐름
- 임베디드 품질은 “동작”보다 **재현 가능한 검증 절차**가 만든다
- 표준화(AUTOSAR)는 자동차 산업에서 **규격 통일/재사용/유지보수 비용 절감**을 위한 실전 전략

---

## 폴더 구조
- `final/` : 최종 발표 자료(PDF)
- `study/` : 학습/정리 자료(PDF/PPTX)
- `LED Blinking with Autosar.png` : 프로젝트 요약 포스터 이미지

---

## Authors
- Sanghui Ko
- Youngeun Seo
- Yeongjin Jeong

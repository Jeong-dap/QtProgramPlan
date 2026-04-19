# QtProgramPlan

# 🖥️ Qt GUI Program Plan Series

<div align="center">

**Qt C++ 프레임워크를 활용한 데스크탑 GUI 프로그램 기획서 시리즈**

_외부 DB 없이 JSON 파일 기반으로 동작하는 Windows 데스크탑 애플리케이션_

</div>

---

## 📋 프로젝트 개요

|항목|내용|
|---|---|
|**개발 언어**|C++17|
|**프레임워크**|Qt 6.x (또는 Qt 5.15 LTS)|
|**IDE**|Qt Creator|
|**데이터 저장**|JSON 파일 (`QJsonDocument` / `QJsonObject`)|
|**타겟 OS**|Windows 10+ (64-bit)|
|**개발 기간**|2026-04-20 ~ 2026-04-22 (3일)|
|**평가 중점**|GUI 이해도 및 완성도|

---

## 📁 기획서 목록

| #   | 프로그램         | 핵심 기능            | 주요 데이터            |
| --- | ------------ | ---------------- | ----------------- |
| 1   | 🗓️ **일정관리** | 일정 CRUD + 캘린더 뷰  | 제목, 날짜, 시간, 카테고리  |
| 2   | 👥 **고객관리**  | 고객 CRUD + 상세 패널  | 이름, 연락처, 이메일, 등급  |
| 3   | 🏦 **은행관리**  | 계좌 CRUD + 입출금 거래 | 계좌, 예금주, 잔액, 거래내역 |

---

## 🛠️ 공통 기술 스택

```
Qt Widgets
├── QMainWindow       — 메인 윈도우
├── QTableWidget      — 데이터 목록
├── QDialog           — 추가 / 수정 폼
├── QComboBox         — 카테고리 / 유형 선택
├── QLineEdit         — 텍스트 입력
├── QMessageBox       — 확인 / 경고 팝업
└── QSplitter         — 화면 분할 레이아웃

Qt Core
├── QJsonDocument     — JSON 파일 파싱
├── QJsonObject       — JSON 객체 처리
├── QJsonArray        — JSON 배열 처리
└── QFile             — 파일 입출력
```

---

## 🗂️ 프로그램별 비교

|항목|🗓️ 일정관리|👥 고객관리|🏦 은행관리|
|---|---|---|---|
|**핵심 클래스**|`Schedule`|`Customer`|`Account` + `Transaction`|
|**JSON 파일**|`schedules.json`|`customers.json`|`bank.json`|
|**메인 UI**|캘린더 + 목록|목록 + 상세 패널|계좌 목록 + 거래 내역|
|**분류 기준**|카테고리|고객 등급 (신규/일반/VIP)|계좌 유형 (입출금/적금/대출)|
|**특이 기능**|날짜 필터|키워드 검색|잔액 연동 입출금|
|**유효성 검사**|날짜·시간 형식|연락처·이메일 형식|금액 양수, 잔액 부족 차단|

---

## 📅 개발 일정 (공통)

```
Day 1 (4/20 월)  ─  데이터 모델 + JSON 입출력 + 메인 윈도우 골격
Day 2 (4/21 화)  ─  CRUD 다이얼로그 구현 ★ 핵심
Day 3 (4/22 수)  ─  권장 기능 + UI 완성도 + 최종 점검 (17:00 마감)
```

> ⚠️ **평가 기준:** 알고리즘 최적화보다 **동작하는 GUI 완성도** 중심

---

## 🏗️ 공통 설계 원칙

- **MVC 패턴** — Model(JSON), View(Qt 위젯), Controller(비즈니스 로직) 분리
- **Repository 패턴** — JSON 입출력을 Repository 클래스로 캡슐화
- **Signal & Slot** — Qt 이벤트 처리 메커니즘 적극 활용
- **외부 의존성 Zero** — DB 미사용, Qt 기본 모듈만으로 완결

---

<div align="center">

Made with using Qt & C++

</div>
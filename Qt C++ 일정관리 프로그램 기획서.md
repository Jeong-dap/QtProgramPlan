---

---


> **프로젝트명:** Qt Schedule Manager  
> **개발 언어:** C++ / Qt Framework  
> **문서 버전:** v1.2  
> **작성일:** 2026-04-19

---

## 목차

1. [[#1. 프로젝트 개요]]
2. [[#2. 개발 환경]]
3. [[#3. 기능 요구사항]]
4. [[#4. UI/UX 설계]]
5. [[#5. 데이터 구조 설계]]
6. [[#6. CRUD 기능 명세]]
7. [[#7. 화면 흐름도]]
8. [[#8. 개발 일정]]
9. [[#9. 리스크 및 고려사항]]

---

## 1. 프로젝트 개요

### 1.1 배경 및 목적

Qt C++ 프레임워크를 활용하여 데스크탑 환경에서 동작하는 일정관리 프로그램을 개발한다.  
사용자가 일정을 직관적으로 추가·조회·수정·삭제할 수 있는 GUI 기반 애플리케이션을 목표로 한다.

### 1.2 핵심 목표

- Qt Widgets 기반의 직관적인 GUI 제공 (GUI 완성도 중심 평가)
- 일정 데이터의 CRUD(Create, Read, Update, Delete) 기능 완전 구현
- JSON 파일 기반 데이터 영속성 보장 (외부 DB 미사용)
- Windows 10+ 환경에서 안정적으로 동작하는 애플리케이션 완성

### 1.3 평가 기준

본 프로젝트는 **GUI 이해도 및 완성도** 중심으로 평가된다.

- Qt 위젯 레이아웃의 적절한 구성 및 사용성
- CRUD 기능의 UI 흐름이 직관적이고 자연스러운가
- 입력 유효성 처리 및 사용자 피드백 (오류 메시지 등)
- 전체적인 화면 완성도 (깨지는 레이아웃 없이 깔끔하게 동작)

> ⚠️ 알고리즘 최적화나 고급 설계 패턴보다 **동작하는 GUI**를 우선한다.

---

## 2. 개발 환경

|항목|내용|
|---|---|
|**언어**|C++17|
|**프레임워크**|Qt 6.x (또는 Qt 5.15 LTS)|
|**IDE**|Qt Creator|
|**빌드 시스템**|CMake 또는 qmake|
|**데이터 저장**|JSON 파일 (`QJsonDocument` / `QJsonObject`)|
|**버전 관리**|Git|
|**타겟 OS**|Windows 10+ (64-bit)|

---

## 3. 기능 요구사항

### 3.1 기능 목록 (Feature List)

> 📅 **개발 기간: 4/20(월) ~ 4/22(수) 오후 5시** — GUI 완성도 중심으로 기능 범위를 현실적으로 조정

#### ✅ 필수 기능 (Must Have) — 3일 내 반드시 완성

- [ ] 일정 생성 (제목, 날짜, 시간, 설명, 카테고리)
- [ ] 일정 목록 조회 (전체 목록)
- [ ] 일정 수정 (선택 후 수정 다이얼로그)
- [ ] 일정 삭제 (선택 후 삭제 + 확인 팝업)
- [ ] 데이터 로컬 저장 / 불러오기 (JSON 파일)
- [ ] 기본 레이아웃 완성 (메인 윈도우 + 목록 + 버튼)

#### 🔶 권장 기능 (Should Have) — 시간 여유 시 구현

- [ ] 날짜별 필터링 (QCalendarWidget 연동)
- [ ] 카테고리별 색상 구분
- [ ] 완료 여부 체크 및 표시

#### 🔷 선택 기능 (Nice to Have) — 여유 있을 때만

- [ ] 키워드 검색
- [ ] 다크 모드 / 스타일시트 적용

---

## 4. UI/UX 설계

### 4.1 메인 화면 구성

```
┌─────────────────────────────────────────────────────────┐
│  [≡ 메뉴]        Qt Schedule Manager        [검색 🔍]   │
├──────────────┬──────────────────────────────────────────┤
│              │                                          │
│   캘린더 뷰   │           일정 목록 / 상세 패널            │
│  (월간 달력)  │                                          │
│              │  ┌──────────────────────────────────┐    │
│   < 2026.04 >│  │ 📌 제목          날짜     카테고리│    │
│              │  │ ─────────────────────────────────│    │
│  일 월 화 수  │  │ 회의 준비        04/20    업무    │    │
│   ...        │  │ 생일 파티        04/21    개인    │    │
│              │  │ Qt 스터디        04/22    학습    │    │
│              │  └──────────────────────────────────┘    │
│              │                                          │
│              │         [+ 일정 추가]  [🗑 삭제]           │
└──────────────┴──────────────────────────────────────────┘
```

### 4.2 일정 추가/수정 다이얼로그

```
┌───────────────────────────────────┐
│         일정 추가 / 수정           │
├───────────────────────────────────┤
│ 제목:   [________________________]│
│ 날짜:   [2026-04-20] 📅           │
│ 시간:   [09:00] ~ [10:00]         │
│ 카테고리: [업무 ▼]                 │
│ 설명:   [                        ]│
│         [                        ]│
│ 완료여부: [ ] 완료                 │
├───────────────────────────────────┤
│         [취소]        [저장]       │
└───────────────────────────────────┘
```

### 4.3 주요 Qt 위젯 매핑

| UI 요소   | Qt 위젯                                     |
| ------- | ----------------------------------------- |
| 메인 윈도우  | `QMainWindow`                             |
| 캘린더     | `QCalendarWidget`                         |
| 일정 목록   | `QTableWidget` 또는 `QListView`             |
| 추가/수정 폼 | `QDialog`                                 |
| 날짜 선택   | `QDateEdit`                               |
| 시간 선택   | `QTimeEdit`                               |
| 카테고리    | `QComboBox`                               |
| 설명 입력   | `QTextEdit`                               |
| 검색창     | `QLineEdit`                               |
| 버튼      | `QPushButton`                             |
| 레이아웃    | `QSplitter`, `QVBoxLayout`, `QHBoxLayout` |

---

## 5. 데이터 구조 설계

### 5.1 Schedule 클래스 (C++)

```cpp
class Schedule {
public:
    int         id;           // 고유 ID (PK)
    QString     title;        // 제목
    QDate       date;         // 날짜
    QTime       startTime;    // 시작 시간
    QTime       endTime;      // 종료 시간
    QString     category;     // 카테고리
    QString     description;  // 설명
    bool        isCompleted;  // 완료 여부
    QDateTime   createdAt;    // 생성 시각
    QDateTime   updatedAt;    // 수정 시각
};
```

### 5.2 JSON 파일 구조

- **저장 위치:** 앱 실행 경로 또는 사용자 설정 경로 (`schedules.json`)
- **Qt 모듈:** `QJsonDocument`, `QJsonObject`, `QJsonArray`, `QFile`

```json
{
  "schedules": [
    {
      "id": 1,
      "title": "팀 회의",
      "date": "2026-04-20",
      "startTime": "09:00",
      "endTime": "10:00",
      "category": "업무",
      "description": "주간 스프린트 회의",
      "isCompleted": false,
      "createdAt": "2026-04-19T14:00:00",
      "updatedAt": "2026-04-19T14:00:00"
    },
    {
      "id": 2,
      "title": "Qt 스터디",
      "date": "2026-04-22",
      "startTime": "19:00",
      "endTime": "21:00",
      "category": "학습",
      "description": "Qt Widgets 심화 학습",
      "isCompleted": false,
      "createdAt": "2026-04-19T15:00:00",
      "updatedAt": "2026-04-19T15:00:00"
    }
  ],
  "lastId": 2
}
```

> **`lastId`** 필드: DB의 AUTO_INCREMENT를 대체하여 새 일정 생성 시 ID를 순차 부여하는 데 사용

#### JSON 파일 입출력 핵심 코드 패턴

```cpp
// 읽기
QFile file("schedules.json");
file.open(QIODevice::ReadOnly);
QJsonDocument doc = QJsonDocument::fromJson(file.readAll());
QJsonArray arr = doc.object()["schedules"].toArray();

// 쓰기
QJsonDocument saveDoc(rootObject);
file.open(QIODevice::WriteOnly);
file.write(saveDoc.toJson(QJsonDocument::Indented));
```

### 5.3 카테고리 기본값

| 카테고리 | 색상             |
| ---- | -------------- |
| 업무   | `#4A90D9` (파랑) |
| 개인   | `#7ED321` (초록) |
| 학습   | `#F5A623` (주황) |
| 건강   | `#E74C3C` (빨강) |
| 기타   | `#9B9B9B` (회색) |

---

## 6. CRUD 기능 명세

### 6.1 Create (일정 생성)

- **진입점:** 메인 화면 `[+ 일정 추가]` 버튼
- **동작 흐름:**
    1. `AddScheduleDialog` 오픈
    2. 사용자가 제목, 날짜, 시간, 카테고리, 설명 입력
    3. `[저장]` 클릭 → 유효성 검사
    4. `ScheduleRepository::create()` 호출 → JSON 파일에 항목 추가 후 저장
    5. 목록 새로고침
- **유효성 검사 규칙:**
    - 제목: 필수, 최대 100자
    - 날짜: 필수, 유효한 날짜
    - 종료 시간 ≥ 시작 시간

```cpp
// 예시 시그니처
void ScheduleRepository::create(const Schedule& schedule);
```

### 6.2 Read (일정 조회)

- **전체 조회:** 앱 시작 시 또는 날짜 필터 초기화 시
- **날짜별 조회:** 캘린더에서 날짜 선택 시 해당 일 일정만 표시
- **키워드 검색:** 검색창 입력 시 메모리에 로드된 목록에서 제목 포함 검색
- **상세 조회:** 목록 행 더블클릭 시 상세 다이얼로그 오픈

```cpp
QList<Schedule> ScheduleRepository::findAll();
QList<Schedule> ScheduleRepository::findByDate(const QDate& date);
QList<Schedule> ScheduleRepository::search(const QString& keyword);
Schedule        ScheduleRepository::findById(int id);
```

### 6.3 Update (일정 수정)

- **진입점:** 목록에서 항목 선택 후 `[수정]` 버튼 또는 더블클릭
- **동작 흐름:**
    1. 기존 데이터를 `EditScheduleDialog`에 바인딩
    2. 사용자가 항목 수정
    3. `[저장]` 클릭 → 유효성 검사
    4. `ScheduleRepository::update()` 호출 → 메모리 목록 갱신 후 JSON 파일 전체 저장
    5. `updated_at` 자동 갱신

```cpp
void ScheduleRepository::update(const Schedule& schedule);
```

### 6.4 Delete (일정 삭제)

- **단건 삭제:** 항목 선택 후 `[삭제]` 버튼
- **확인 다이얼로그:** `QMessageBox::question` 으로 재확인
- **처리:**
    1. 사용자 확인
    2. `ScheduleRepository::remove(int id)` 호출 → 메모리 목록에서 제거 후 JSON 파일 전체 저장
    3. 목록 새로고침

```cpp
void ScheduleRepository::remove(int id);
void ScheduleRepository::removeSelected(const QList<int>& ids);
```

---

## 7. 화면 흐름도

```
앱 시작
   │
   ▼
메인 화면 (캘린더 + 목록)
   │
   ├──[날짜 클릭]──────► 해당 날짜 일정 필터링
   │
   ├──[+ 일정 추가]────► 일정 추가 다이얼로그
   │                         │
   │                    [저장] → JSON 저장 → 목록 갱신
   │                    [취소] → 닫기
   │
   ├──[항목 더블클릭]──► 일정 수정 다이얼로그
   │                         │
   │                    [저장] → JSON 저장 → 목록 갱신
   │                    [취소] → 닫기
   │
   ├──[삭제 버튼]──────► 확인 다이얼로그
   │                         │
   │                    [확인] → JSON 저장 → 목록 갱신
   │                    [취소] → 닫기
   │
   └──[검색창 입력]────► 키워드 필터링 → 결과 표시
```

---

## 8. 개발 일정

> **전체 기간:** 2026-04-20(월) 09:00 ~ 2026-04-22(수) 17:00 (약 56시간)  
> **전략:** 핵심 CRUD + GUI 골격을 Day 1~2에 완성하고, Day 3은 완성도 다듬기에 집중

|일자|시간대|작업 내용|산출물|
|---|---|---|---|
|**Day 1** (4/20 월)|오전|프로젝트 생성, `Schedule` 클래스 정의, JSON 입출력 구현|`schedule.h`, `jsonrepository.cpp`|
||오후|메인 윈도우 레이아웃 구성 (목록 + 버튼 배치)|`mainwindow.ui` 기본 완성|
|**Day 2** (4/21 화)|오전|일정 추가 다이얼로그 구현 (Create)|`adddialog.cpp`|
||오후|일정 수정 / 삭제 기능 구현 (Update / Delete)|CRUD 핵심 완성|
|**Day 3** (4/22 수)|오전|날짜 필터, 카테고리 색상, 완료 체크 등 권장 기능|UI 완성도 향상|
||~17:00|전체 테스트, 버그 수정, 레이아웃 최종 점검|최종 제출본|

### 8.1 Day별 우선순위 요약

```
Day 1 ─ 기반 구축
  ├─ Schedule 데이터 모델 (클래스 + JSON 직렬화)
  └─ 메인 윈도우 레이아웃 (QTableWidget + 버튼)

Day 2 ─ CRUD 완성 ★ 핵심
  ├─ [추가] AddDialog → JSON 저장 → 목록 갱신
  ├─ [수정] EditDialog → 기존 데이터 바인딩 → 저장
  └─ [삭제] 선택 항목 제거 → QMessageBox 확인

Day 3 ─ 완성도 (17시 마감)
  ├─ 권장 기능 (캘린더 연동, 카테고리 색상 등)
  └─ UI 정돈, 입력값 유효성, 마감 전 최종 점검
```

> ⚠️ **Day 3 오후 2시 이후**에는 새 기능 추가를 중단하고 버그 수정과 UI 점검에만 집중할 것을 권장한다.

---

## 9. 리스크 및 고려사항

### 9.1 기술적 리스크

|리스크|대응 방안|
|---|---|
|Qt 버전 호환성|Qt 5.15 LTS 기준으로 개발 (Windows에서 안정적)|
|JSON 파일 손상|저장 전 임시 파일에 쓰고 교체하는 방식으로 원자적 저장 구현|
|대용량 데이터 성능|앱 시작 시 전체 로드 후 메모리에서 처리, 수백~수천 건 수준에서 충분|
|일정 지연|Day 2 종료 시점에 CRUD 미완성이면 권장 기능 전부 포기하고 핵심만 완성|

### 9.2 설계 원칙

- **MVC 패턴 준수:** Model(데이터/JSON), View(Qt 위젯), Controller(비즈니스 로직) 분리
- **Repository 패턴:** JSON 파일 입출력 코드를 Repository 클래스로 캡슐화
- **Signal & Slot:** Qt의 Signal/Slot 메커니즘을 적극 활용한 이벤트 처리

### 9.3 추후 확장 고려사항

- Windows 배포 패키지 구성 (`windeployqt` 활용)
- 클라우드 동기화 (Google Calendar API 연동)
- 반복 일정 기능 (매일/매주/매월)

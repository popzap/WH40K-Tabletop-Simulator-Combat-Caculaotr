# WH40K Dice Calculator

Warhammer 40,000 보드게임 전투 계산을 보조하기 위한 웹 기반 주사위 기대값 계산기입니다.

Tabletop Simulator에서 저장한 군대 JSON 파일을 불러와 공격 유닛과 방어 유닛을 선택하고, 명중 → 부상 → 방어 → 피해 → 기대 제거 모델 수를 한눈에 확인할 수 있습니다.

> 팬 제작 도구이며 Games Workshop과 공식적으로 관련이 없습니다.

---

## 프로젝트 개요

현재 프로젝트 기준은 다음과 같습니다.

- 게임 데이터 기준: **Warhammer 40K 10th Edition 데이터**
- 주요 입력 방식: **Tabletop Simulator에서 저장한 army JSON 파일**
- 실행 방식: **별도 서버 없이 HTML 파일 실행 가능**

---

## 주요 기능

### 1. 내 군대 / 상대 군대 JSON 불러오기

공격 측과 방어 측에 각각 다른 군대 JSON 파일을 불러올 수 있습니다.

- `My Army JSON`
- `Opponent Army JSON`

Tabletop Simulator에서 저장한 army JSON을 기반으로 유닛, 무기, 방어 수치, 특수 능력을 자동으로 읽어옵니다.

### 2. 공격 / 방어 유닛 선택

공격 측에서는 `팩션 → 유닛 → 무기` 순서로 선택합니다.

방어 측에서는 `팩션 → 유닛` 순서로 선택합니다.

선택한 유닛의 능력치는 자동으로 수동 조정 영역에 반영됩니다.

### 3. 무기 유형 표시

무기 목록에는 근접 무기와 원거리 무기가 구분되어 표시됩니다.

```text
[Ranged] Gauss Flayer
[Melee] Hyperphase Glaive
[Ranged] Tachyon Arrow
```

### 4. 단계별 필요 주사위 표시

공격 유닛과 방어 유닛을 선택하면 전투 과정이 단계별로 표시됩니다.

```text
명중 → 부상 → 방어 실패 → FNP 실패
```

각 단계에서는 필요한 주사위 값과 성공/실패 확률을 확인할 수 있습니다.

### 5. 기대 결과 계산

선택한 공격과 방어 조건을 기반으로 평균 기대값을 계산합니다.

표시되는 결과는 다음과 같습니다.

- 평균 명중
- 평균 부상
- 평균 피해
- 기대 제거 모델 수

### 6. 수동 조정 기능

자동으로 불러온 데이터가 실제 게임 상황과 다르거나, 특정 버프/디버프가 적용되는 경우 직접 값을 수정할 수 있습니다.

공격 측 수동 조정:

- 공격 횟수 `A`
- 명중 스킬 `BS / WS`
- 공격력 `S`
- 관통 `AP`
- 피해량 `D`

방어 측 수동 조정:

- 강인함 `T`
- 방어도 `Sv`
- 무적 방어 `Inv`
- 고통 무시 `FNP`
- 체력 `W`
- 모델 수

### 7. 특수 규칙 토글

자주 사용하는 공격 관련 특수 규칙을 버튼으로 켜고 끌 수 있습니다.

지원하는 규칙:

- Re-roll Hits
- Re-roll Wounds
- Auto-wound on Hit 6
- Ignore Save on Wound 6
- Auto Hit
- Extra Hit on Hit 6
- Twin-linked

각 버튼에 마우스를 올리면 한글 설명이 표시됩니다.

### 8. 유닛 특수 능력 툴팁

공격 유닛과 방어 유닛을 선택하면 해당 유닛이 가진 특수 능력이 버튼 형태로 표시됩니다.

버튼 위에 마우스를 올리면 능력 설명을 확인할 수 있습니다.

- 능력 이름: 가능한 영어 원문 유지
- 설명: 가능한 한 한글 설명 제공
- 번역이 명확하지 않은 경우 영어 원문 함께 표시

### 9. 관전자용 공격 / 방어 스왑

관전자 시점에서 공격 측과 방어 측이 반대로 보일 때 사용할 수 있는 스왑 버튼을 제공합니다.

```text
SWAP SIDES
```

스왑 시 다음 정보가 서로 바뀝니다.

- 공격 측 군대 JSON
- 방어 측 군대 JSON
- 선택된 팩션
- 선택된 유닛
- 선택된 무기
- 입력 수치
- JSON 로드 상태

### 10. 라이트 / 다크 모드

우측 상단의 토글 버튼으로 화면 테마를 변경할 수 있습니다.

- Light Mode
- Dark Mode

---

## 사용 방법

### 1. 프로젝트 실행

가장 간단한 방법은 HTML 파일을 브라우저로 직접 여는 것입니다.

```text
index.html
```

### 2. 군대 JSON 준비

Tabletop Simulator에서 자신의 군대를 구성한 뒤 저장한 JSON 파일을 준비합니다.
다운 받은 군대 JSON파일은 보통 다음의 경로에 있습니다. \Documents\My Games\Tabletop Simulator\Saves\Saved Objects
혹은 Tabletop Simulator에서 군대를 저장후 ` 버튼을 눌러 콘솔을 호출해 저장한 경로를 확인 가능합니다.

예시 파일명:

```text
army_2.json
my_army_01.json
opponent_army.json
```

### 3. 내 군대 JSON 불러오기

공격 측 패널에서 다음 버튼을 클릭합니다.

```text
My Army JSON
```

내 군대 JSON 파일을 선택하면 공격 유닛 목록이 자동으로 생성됩니다.

### 4. 상대 군대 JSON 불러오기

방어 측 패널에서 다음 버튼을 클릭합니다.

```text
Opponent Army JSON
```

상대 군대 JSON 파일을 선택하면 방어 유닛 목록이 자동으로 생성됩니다.

### 5. 공격 유닛과 무기 선택

공격 측에서 다음 순서로 선택합니다.

```text
팩션 → 유닛 → 무기
```

무기를 선택하면 공격 횟수, 명중 스킬, 공격력, AP, 피해량이 자동으로 입력됩니다.

### 6. 방어 유닛 선택

방어 측에서 다음 순서로 선택합니다.

```text
팩션 → 유닛
```

방어 유닛을 선택하면 강인함, 방어도, 체력, 모델 수 등이 자동으로 입력됩니다.

### 7. 상황에 맞게 수동 조정

게임 중 적용되는 버프나 디버프가 있다면 수동 조정 영역에서 값을 변경합니다.

예시:

- 명중 보정으로 `BS/WS` 변경
- 방어 보정으로 `Sv` 변경
- 무적 방어 적용
- FNP 적용
- Rapid Fire, Aura, Command Ability 등 조건부 효과 반영

### 8. 결과 확인

화면 하단의 기대 결과 영역에서 평균 결과를 확인합니다.

```text
평균 명중
평균 부상
평균 피해
기대 제거
```

---

## 주의 사항

### 조건부 능력은 자동 적용되지 않을 수 있음

오라, 거리 조건, 특정 대상 조건, Command Phase 효과처럼 상황에 따라 적용 여부가 달라지는 능력은 자동 계산하지 않습니다.

이 경우 능력 설명을 확인한 뒤 수동으로 값을 조정해야 합니다.

예시:

- Aura 효과
- Command Protocols
- My Will Be Done
- Rapid Fire 거리 조건
- 특정 대상에게만 적용되는 재굴림
- 특정 유닛 타입에게만 적용되는 보너스

### 데이터 원본에 따라 정확도가 달라질 수 있음

Tabletop Simulator 저장 파일에 능력치나 무기 정보가 제대로 들어 있지 않으면 계산기에 정확히 반영되지 않을 수 있습니다.

정상적으로 적용하려면 유닛의 `Description` 또는 `LuaScript` 안에 다음 정보가 있어야 합니다.

- 유닛 이름
- 모델 수
- T
- Sv
- W
- 무기 이름
- 무기 타입
- 공격 횟수
- BS / WS
- S
- AP
- D
- 특수 능력


## 추천 파일 구조

```text
warhammer-dice-calculator/
├─ index.html
├─ README.md
└─ data/
  ├─ sample_my_army.json
  └─ sample_opponent_army.json

```

---

## 개발 목적

이 프로젝트는 Warhammer 40K 보드게임 플레이 중 전투 계산을 빠르게 보조하기 위한 개인/팬 제작 도구입니다.

정확한 공식 판정은 반드시 실제 룰북, 코덱스, 데이터시트, FAQ를 기준으로 확인해야 합니다.

---

## License

Fan-made project.

Warhammer 40,000 and related names are trademarks of Games Workshop.  
This project is not affiliated with or endorsed by Games Workshop.

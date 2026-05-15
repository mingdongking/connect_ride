# Connect: Ride — 디자인 가이드

> **버전** v0.5 · **대상 파일** `connect-ride-prototype.html`  
> 이 문서는 프로토타입에서 실제로 사용된 색상, 타이포그래피, 간격, 모션, 컴포넌트 패턴을 정리합니다.

---

## 목차

1. [디자인 원칙](#1-디자인-원칙)
2. [색상 시스템](#2-색상-시스템)
3. [타이포그래피](#3-타이포그래피)
4. [간격 & 레이아웃](#4-간격--레이아웃)
5. [테두리 & 엘리베이션](#5-테두리--엘리베이션)
6. [모션 & 애니메이션](#6-모션--애니메이션)
7. [컴포넌트 패턴](#7-컴포넌트-패턴)
8. [맵 시각 언어](#8-맵-시각-언어)
9. [아이콘 시스템](#9-아이콘-시스템)
10. [다크 모드](#10-다크-모드)

---

## 1. 디자인 원칙

### 1-1. 스케치 질감 (Sketch Aesthetic)
맵 SVG에 `feTurbulence` + `feDisplacementMap` 필터를 적용해 손으로 그린 듯한 유기적 질감을 부여합니다. 정확한 기계 도면보다 **사람 친화적인 공간 인식**을 유도하는 것이 목적입니다.

### 1-2. 상태 중심 UI (State-Driven UI)
별도의 라우터 없이 단일 `state` 객체의 `mode`, `step` 값으로 모든 화면을 결정합니다. 화면 전환에 별도 트랜지션 라이브러리를 사용하지 않으며, 상태 변경 즉시 화면이 교체됩니다.

### 1-3. 인라인 스타일 우선
모든 컴포넌트 스타일은 React 인라인 스타일로 작성되어 있어, 테마 변수(`theme.core`, `theme.muted` 등)를 JavaScript에서 직접 참조합니다. CSS 클래스는 Tweaks 패널 전용으로만 사용합니다.

### 1-4. 프로토타입 특화 요소
- **PhoneShell**: 392 × 832px 고정 비율의 가상 폰 프레임
- **Tweaks 패널**: 우하단 ⚙ 버튼으로 열리는 실시간 설정 패널 (테마, 다크모드, 로봇 수 등)
- **스케치 강도 슬라이더**: 0.0 ~ 1.2 범위로 맵의 손그림 필터 세기 조절

---

## 2. 색상 시스템

### 2-1. 색상 토큰 역할

| 토큰 | 역할 |
|------|------|
| `deep` | 가장 진한 브랜드 색. 주요 텍스트, 강조 배경에 사용 |
| `core` | 핵심 인터랙션 색. 버튼, 선택 상태, 필터 활성화 |
| `bright` | 보조 강조 색. 도착지, LIVE 뱃지, 완료 상태 |
| `sky` | 배경 틴트. 카드 배경 강조, 뱃지 배경, 선택 하이라이트 |
| `surface` | 앱 전체 배경 (가장 밝음) |
| `bg` | 인터페이스 섹션 배경 |
| `card` | 카드·패널 배경 (흰색 계열) |
| `muted` | 보조 텍스트, 비활성 아이콘, 플레이스홀더 |
| `border` | 구분선, 카드 외곽선 |
| `ink` | 전체 본문 텍스트 기본색 |

### 2-2. 테마별 색상 값

#### Cobalt (기본 테마)

| 토큰 | 헥스 | 미리보기 |
|------|------|---------|
| `deep` | `#002F6C` | 네이비 |
| `core` | `#0047AB` | 코발트 블루 |
| `bright` | `#3B82F6` | 스카이 블루 |
| `sky` | `#BFDBFE` | 아이스 블루 |
| `surface` | `#FAFCFE` | 거의 흰색 |
| `bg` | `#F2F6FB` | 연한 파란 흰색 |
| `card` | `#FFFFFF` | 흰색 |
| `muted` | `#5B6B85` | 슬레이트 그레이 |
| `border` | `#E1E8F2` | 연한 파란 회색 |
| `ink` | `#0E1A33` | 다크 네이비 |

#### Forest

| 토큰 | 헥스 |
|------|------|
| `deep` | `#0F3D2E` |
| `core` | `#1E7A4D` |
| `bright` | `#4CAF50` |
| `sky` | `#C8E6C9` |
| `muted` | `#5B6E62` |
| `border` | `#DDE8DF` |

#### Ember

| 토큰 | 헥스 |
|------|------|
| `deep` | `#5C1E0B` |
| `core` | `#C2410C` |
| `bright` | `#F97316` |
| `sky` | `#FED7AA` |
| `muted` | `#7A6A63` |
| `border` | `#EDE0D8` |

#### Graphite

| 토큰 | 헥스 |
|------|------|
| `deep` | `#1F2937` |
| `core` | `#4B5563` |
| `bright` | `#6366F1` |
| `sky` | `#E5E7EB` |
| `muted` | `#6B7280` |
| `border` | `#E5E7EB` |

### 2-3. 상태 전용 고정 색상

테마와 무관하게 항상 동일하게 사용되는 시맨틱 색상입니다.

| 상황 | 색상 | 용도 |
|------|------|------|
| 사용 중 (riding) | `#22C55E` (도트) / `#DCFCE7` (배경) / `#166534` (텍스트) | 이용 내역 카드 |
| 호출 취소 (cancelled) | `#EF4444` (도트) / `#FEE2E2` (배경) / `#991B1B` (텍스트) | 이용 내역 카드 |
| 매칭 대기 | `#F59E0B` | 로봇 탐색 중 뱃지 도트 |
| 로봇 이용 중 | `#94A3B8` | 맵 위 이용 중 로봇 라벨 |
| 위험 동작 | `#DC2626` | PrimaryButton danger variant |

### 2-4. 배경 그라디언트 (데스크톱 캔버스)
```css
background: radial-gradient(
  1200px 800px at 50% 30%,
  #EAF2FC 0%,
  #DFE9F7 60%,
  #D2DEF0 100%
);
```
배경 위에 `24px × 24px` 도트 패턴 오버레이를 추가합니다.
```css
background-image: radial-gradient(circle at 1px 1px, rgba(0,47,108,0.06) 1px, transparent 0);
background-size: 24px 24px;
```

---

## 3. 타이포그래피

### 3-1. 폰트 패밀리

| 역할 | 폰트 | 용도 |
|------|------|------|
| **본문 (Primary)** | `Pretendard Variable` | 모든 UI 텍스트, 버튼, 레이블 |
| **데이터 (Mono)** | `JetBrains Mono` | 로봇 ID, 노드 코드, 배터리 수치, 카운트 등 |

Fallback 체인:
```
'Pretendard Variable', Pretendard, -apple-system, BlinkMacSystemFont,
system-ui, Roboto, 'Helvetica Neue', 'Apple SD Gothic Neo', Arial, sans-serif
```

### 3-2. 타입 스케일

| 레벨 | 크기 | 두께 | 용도 |
|------|------|------|------|
| Display | 24px | 700 | 화면 전환 알림 (로봇 도착, 완료) |
| Title | 22–24px | 700 | 페이지 제목 (이용 내역, 로봇 현황) |
| Heading | 15–17px | 700 | 카드 제목, 주요 레이블 |
| Body | 13–14px | 400–600 | 본문, 설명 텍스트 |
| Caption | 11–12px | 500–600 | 보조 정보, 시간, 안내 문구 |
| Mono Data | 9–15px | 600–700 | 로봇 ID, 노드 코드, 타이머 |
| Mono Large | 28–32px | 700 | 카운트다운 타이머 (ETA) |

### 3-3. Letter Spacing 규칙

| 상황 | 값 |
|------|-----|
| 제목류 (Pretendard) | `-0.01em` ~ `-0.02em` (자간 줄임) |
| 본문 | `0` (기본) |
| 배지·태그 (Mono) | `+0.04em` ~ `+0.06em` (자간 넓힘) |
| 전체 대문자 레이블 | `+0.06em` |

---

## 4. 간격 & 레이아웃

### 4-1. 기본 간격 단위

| 값 | 사용처 |
|----|--------|
| `4px` | 아이콘-텍스트 사이 미세 간격 |
| `6px` | 뱃지 내부, 탭 아이템 세로 패딩 |
| `8px` | 칩·카드 내부 요소 간격 |
| `10px` | 카드 내 섹션 구분 |
| `12px` | 카드 간 마진, 상단 요소 구분 |
| `14px` | 카드 내부 패딩 (세로) |
| `16px` | 화면 좌우 여백 (표준) |
| `18–20px` | 강조 카드 내부 패딩 |
| `22px` | 폰 상태바 좌우 패딩 |
| `24px` | 데스크톱 스테이지 패딩 |

### 4-2. 화면 레이아웃 구조

```
┌──────────────────────────┐  ← PhoneShell (392 × 832px)
│  StatusBar (38px)        │
├──────────────────────────┤
│  AppHeader               │
│  ┌────────────────────┐  │
│  │ RideBanner         │  │  padding: 12px 16px 0
│  └────────────────────┘  │
│  StepIndicator           │  padding: 14px 14px 10px
│  ┌────────────────────┐  │
│  │ MapContainer       │  │  margin: 10px 16px 0
│  │  (260–340px 높이)  │  │
│  └────────────────────┘  │
│  ActionCard / 버튼 영역  │  margin: 12px 16px 16px
├──────────────────────────┤
│  BottomNav               │
│  NavBar gesture bar(22px)│
└──────────────────────────┘
```

### 4-3. 그리드 & 정렬

- 좌우 여백: 일관되게 **16px** 적용
- 카드 간 마진: **8–12px**
- BottomNav: `grid-template-columns: repeat(3, 1fr)` 균등 분할
- RouteChip: `display: flex` + `flex: 1` 균등 너비

---

## 5. 테두리 & 엘리베이션

### 5-1. 테두리 패턴 — inset box-shadow

CSS `border` 대신 `box-shadow: inset` 방식으로 테두리를 구현합니다. 이렇게 하면 크기 계산에 영향을 주지 않고 테두리를 그릴 수 있습니다.

| 용도 | 값 |
|------|-----|
| 기본 카드 | `inset 0 0 0 1.2px ${theme.border}` |
| 활성 카드 / 선택 상태 | `inset 0 0 0 1.5px ${theme.core}` |
| 필터 버튼 활성 | `inset 0 0 0 1.4px ${theme.core}` |
| StepIndicator 칩 | `inset 0 0 0 1.4px ${stroke}` |
| ghost 버튼 | `border: 1.4px solid ${theme.border}` (실제 border 사용) |
| RouteChip | `inset 0 0 0 1.4px ${color}` |
| 입력 필드 | `1.4px solid ${theme.border}` → 포커스 시 `theme.core` |

### 5-2. Border Radius 체계

| 값 | 사용처 |
|----|--------|
| `999px` | 알약형 뱃지, 필터 버튼, StepIndicator 칩 |
| `44px` | PhoneShell 외곽 (모서리 라운딩) |
| `16px` | MapContainer, RideBanner, 강조 배너 카드 |
| `14px` | 일반 카드 (ActionCard, 정보 패널) |
| `12px` | PrimaryButton, 입력 필드, 내역 카드 |
| `11px` | AppHeader 버튼 |
| `10px` | RouteChip, 소형 패널 |
| `8px` | 강조 카드 내 뱃지, 소형 UI |
| `6px` | 맵 로봇 라벨, 탭 슬라이딩 thumb |
| `50%` | 원형 아바타, 스피너, 노드 |

### 5-3. 그림자 (Box Shadow)

| 레벨 | 값 | 사용처 |
|------|-----|--------|
| 높음 (PhoneShell) | `0 30px 80px rgba(0,47,108,0.28), 0 0 0 1px rgba(0,0,0,0.04)` | 가상 폰 프레임 |
| 중간 (사용 중 카드) | `0 4px 16px ${theme.core}44` | History riding 카드 |
| 낮음 (맵 줌 버튼) | `0 2px 8px ${theme.deep}15` | 맵 위 플로팅 UI |
| 마이크로 (버튼 thumb) | `0 1px 2px rgba(0,0,0,0.12)` | 세그먼트 컨트롤 |

---

## 6. 모션 & 애니메이션

### 6-1. CSS 트랜지션

| 대상 | 속성 | Duration | Easing | 트리거 |
|------|------|----------|--------|--------|
| PrimaryButton 누름 | `transform` | `0.08s` | ease | mouseDown/Up |
| PrimaryButton 색상 | `opacity` | `0.15s` | — | disabled 전환 |
| 필터 버튼 | `all` | `0.18s` | — | 토글 |
| 세그먼트 슬라이딩 thumb | `left`, `width` | `0.15s` | `cubic-bezier(.3,.7,.4,1)` | 선택 변경 |
| 진행 바 | `width` | `0.6s` | linear | routeProgress 증가 |
| 하차 완료 배너 배경 | `background` | `0.6s` | ease | phase 0→1 전환 |
| 노드 원 반지름 | `r` | `0.18s` | ease | 선택/해제 |
| 노드 토글 상태 | `transition` | `0.3s` | — | 필터 ON/OFF |

### 6-2. CSS 키프레임

```css
@keyframes spin {
  to { transform: rotate(360deg); }
}
```
적용: 로봇 탐색 중 스피너 (`animation: spin 1.0–1.2s linear infinite`)

### 6-3. SVG 애니메이션 (SMIL)

| 위치 | 타입 | 속성 | 동작 |
|------|------|------|------|
| 경로 이동 중 파선 | `animate` | `stroke-dashoffset` | `0 → -28` / `1.2s infinite` — 경로 위 빛 흐르는 효과 |
| 추천 노드 점선 원 | `animateTransform` | `rotate` | `0° → 360°` / `14s infinite` — 느린 회전 |
| 현재 위치 pulse | `animate` | `r` | `r+2 → r+9` / `1.8s infinite` |
| 현재 위치 pulse | `animate` | `opacity` | `0.6 → 0` / `1.8s infinite` |
| 매칭된 로봇 pulse | `animate` | `r` | `10 → 18` / `1.2s infinite` |
| 매칭된 로봇 pulse | `animate` | `fill-opacity` | `0.3 → 0` / `1.2s infinite` |

### 6-4. 자동 화면 전환 타이밍

| 전환 | 지연 시간 |
|------|----------|
| 로봇 탐색 시작 → 매칭 단계 | `+1,300ms` |
| 매칭 단계 → 매칭 완료 | `+2,600ms` |
| 매칭 완료 → 이동 화면 자동 전환 | `+800ms` |
| routeProgress=1 → 다음 화면 | `+600ms` |
| 하차 대기 → 완료 상태 | `+3,000ms` |

---

## 7. 컴포넌트 패턴

### 7-1. 카드 (Card)

모든 정보 그룹의 기본 컨테이너입니다.

```
background: theme.card (흰색)
border-radius: 14px
box-shadow: inset 0 0 0 1.2px theme.border
padding: 14–16px
margin: 12–16px (좌우 16px 표준)
```

**강조 카드** (알림 배너, 도착 안내): `background: theme.core`, 텍스트 흰색, `border-radius: 16px`

### 7-2. 뱃지 & 칩

**상태 뱃지** (MapBadge, 이용 내역 상태):
```
padding: 3–4px 8–9px
border-radius: 999px
font-size: 10.5–11px
font-weight: 700
도트 인디케이터: width/height 6–7px, border-radius: 50%
```

**필터 칩 (BottomNav 아이콘 영역 제외)**:
```
비활성: background: theme.card + inset shadow border
활성: background: theme.deep + 텍스트 흰색
```

**RouteChip** (출발/목적지):
```
border-radius: 10px
inset shadow로 색상 테두리
코드: JetBrains Mono 13px Bold
✕ 리셋 버튼: 22×22px 원형, 우측 배치
```

### 7-3. 버튼

**PrimaryButton**

| variant | background | color | border |
|---------|-----------|-------|--------|
| `primary` | `theme.core` | `#fff` | 없음 |
| `ghost` | `transparent` | `theme.core` | `1.4px solid theme.border` |
| `danger` | `#DC2626` | `#fff` | 없음 |
| disabled | `theme.border` | `theme.muted` | 없음 |

공통 스타일:
```
padding: 10–14px 16px
border-radius: 12px
font-size: 15px, font-weight: 700
letter-spacing: -0.01em
transition: transform 0.08s, opacity 0.15s
mouseDown → scale(0.98)
mouseUp/Leave → scale(1)
```

### 7-4. 진행 바 (Progress Bar)

```
height: 6px
border-radius: 3px
background: theme.border (트랙)
fill: linear-gradient(90deg, theme.core, theme.bright)
transition: width 0.6s linear
```

### 7-5. 스피너 (로딩)

SVG 사용 없이 CSS `conic-gradient`로 구현:
```css
width: 32px; height: 32px;
border-radius: 50%;
background: conic-gradient(theme.core 0deg, theme.core 90deg, theme.sky 90deg);
animation: spin 1.2s linear infinite;
```

### 7-6. StepIndicator

- 3단계 고정: 출발 → 도착 → 호출
- 활성 단계: `theme.core` 배경, 숫자 흰 원
- 완료 단계: `theme.sky` 배경, `✓` 체크, 선택된 값 코드 뱃지 표시
- 미도달 단계: 투명 배경, `theme.border` 외곽선

---

## 8. 맵 시각 언어

### 8-1. SVG 캔버스 크기

```
전체 viewBox: 400 × 280
좌우 여백(MARGIN_X): 24px
상하 여백(MARGIN_Y): 28px
```

### 8-2. 스케치 필터 (Sketch Effect)

`feTurbulence` + `feDisplacementMap` 조합으로 손그림 질감 연출:
```xml
<filter>
  <feTurbulence type="fractalNoise" baseFrequency="0.022" numOctaves="2" seed="3"/>
  <feDisplacementMap in="SourceGraphic" scale={intensity * 1.8}/>
</filter>
```
- `intensity` 범위: 0.0 ~ 1.2 (Tweaks 패널 슬라이더)
- scale 0이면 완전 선명, 높아질수록 흔들림 증가

배경 도트 패턴:
```xml
<pattern width="8" height="8">
  <circle cx="1" cy="1" r="0.7" fill={theme.border} opacity="0.7"/>
</pattern>
```

### 8-3. 노드 상태별 시각 처리

| 상태 | 원 반지름 | fill | stroke |
|------|---------|------|--------|
| 기본 | 9px | `theme.card` | `theme.muted` |
| 탭 가능 (hover) | 9px | `#fff` | `theme.core` |
| 출발지 선택 | 11px | `theme.core` | `theme.core` |
| 목적지 선택 | 11px | `theme.bright` | `theme.bright` |
| 추천 노드 | 9px | — | 점선 원 + 14s 회전 애니메이션 |
| 현재 위치 | 9px | — | pulse 애니메이션 (1.8s) |

탭 히트 영역은 실제 원보다 크게 (`r=18`) 설정하여 모바일 터치 UX를 고려합니다.

### 8-4. 경로선 (Route Path)

맨해튼 경로 알고리즘 (직각 꺾임):
```
M dep.cx dep.cy
L dep.cx midY      (수직 이동)
L arr.cx midY      (수평 이동)
L arr.cx arr.cy    (수직 이동)
```
`midY = dep.cy + (arr.cy - dep.cy) * 0.55`

| 모드 | 선 스타일 |
|------|---------|
| `view` (경로 미리보기) | `stroke-dasharray: 5 4` (점선) |
| `enroute` (이동 중) | 실선 위에 파선 오버레이 + `stroke-dashoffset` 애니메이션 |

### 8-5. 로봇 라벨

```
크기: 38 × 15px 라운드 사각형
background: theme.deep (idle), #94A3B8 (in-use), theme.bright (매칭)
폰트: JetBrains Mono 6.5px Bold
로봇 아이콘: SVG 인라인 미니 아이콘 (머리+몸통+바퀴)
선: 로봇 현재 노드 → 라벨 연결선 0.8px opacity 0.4
```

---

## 9. 아이콘 시스템

모든 아이콘은 인라인 SVG로 구현합니다. 외부 아이콘 라이브러리를 사용하지 않습니다.

### 9-1. 네비게이션 아이콘 (22 × 22px viewBox)

| 아이콘 | 설명 |
|--------|------|
| **탑승** | 로봇 실루엣 (원+사각 바디) + 하단 아크 (플랫폼) |
| **로봇 현황** | 태블릿 프레임 + 도트 위치 마커 + 우상단 `+` 원형 뱃지 |
| **내역** | 원형 시계 (원 + 시침) |

비활성: `theme.muted` 단색 / 활성: `theme.core` + 내부 `theme.sky` fill

### 9-2. 기능 아이콘

| 위치 | 크기 | 설명 |
|------|------|------|
| AppHeader 햄버거 | 16 × 16px | 3선 수평 (strokeWidth 1.6) |
| 출발지 힌트 (PointIcon) | 22 × 22px | 손 + 탭 동작 표현 SVG |
| 줌 버튼 | 텍스트 `+` / `−` | 18px 폰트 |

### 9-3. 색상 적용 방식

```jsx
// active 상태
const c = active ? theme.core : theme.muted;

// SVG stroke/fill에 직접 바인딩
<svg ...>
  <path stroke={c} fill={active ? theme.sky : 'none'} .../>
</svg>
```

---

## 10. 다크 모드

### 10-1. 오버레이 방식

다크 모드는 별도 테마가 아니라 라이트 테마 위에 `DARK_OVERLAY`를 병합(`Object.assign`)하는 방식입니다. 색상 토큰 중 배경·표면 관련 6개만 교체됩니다.

```js
const DARK_OVERLAY = {
  surface: '#0B1426',   // 앱 최상위 배경
  bg:      '#070D1A',   // 섹션 배경
  ink:     '#E8EEF8',   // 본문 텍스트
  muted:   '#8597B5',   // 보조 텍스트
  border:  '#1B2843',   // 구분선
  card:    '#0F1C36',   // 카드 배경
};
```

`deep`, `core`, `bright`, `sky`는 테마별 원본 값을 그대로 유지합니다.

### 10-2. 적용 범위

| 영역 | 변화 |
|------|------|
| PhoneShell 테두리 | `#171a22` → `#1a1a1f` |
| 카드 배경 | `#FFFFFF` → `#0F1C36` |
| 맵 배경 | `theme.bg` 토큰으로 자동 적용 |
| 노드 기본 fill | `#fff` → `theme.card` (다크 카드색) |
| 텍스트 | `theme.deep` / `theme.muted` 토큰 자동 적용 |

---

## 부록: 디자인 토큰 빠른 참조

```
── 색상 ──────────────────────────────────
deep     강조 배경, 제목
core     주 인터랙션 (버튼, 선택)
bright   보조 강조 (완료, LIVE)
sky      배경 틴트 (뱃지 bg, 하이라이트)
surface  최상위 배경
bg       섹션 배경
card     카드 배경
muted    보조 텍스트, 비활성
border   외곽선, 구분선

── 타이포 ────────────────────────────────
Pretendard  본문 UI 전반
JetBrains   코드/데이터 (ID, 수치, 타이머)
제목        700 / -0.02em
본문        400–600 / 0
뱃지        700 / +0.04em

── 간격 ──────────────────────────────────
화면 좌우 여백   16px
카드 패딩        14–16px
카드 간 마진     8–12px
섹션 간 마진     10–14px

── 반지름 ────────────────────────────────
알약형 칩        999px
강조 카드        16px
일반 카드        14px
버튼             12px
소형 UI          8–10px

── 모션 ──────────────────────────────────
버튼 누름        scale(0.98) / 0.08s
진행 바          width / 0.6s linear
배경 전환        background / 0.6s ease
SVG 경로 흐름    dashoffset / 1.2s infinite
노드 pulse       r+opacity / 1.8s infinite
```

---

*작성일: 2026-05-16 · Connect: Ride Prototype v0.5*

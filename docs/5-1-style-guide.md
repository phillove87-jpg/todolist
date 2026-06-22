# TodoList 앱 스타일 가이드

## 1. 스타일 방향 요약

첨부된 GitHub 스크린샷의 UI 스타일은 아래 특징을 가진다.

- 거의 검정에 가까운 다크 배경
- 명도 차이가 크지 않은 레이어드 패널 구조
- 얇고 차분한 보더
- 흰색이 아닌 약간 탁한 텍스트 컬러
- 포인트 컬러는 제한적으로 사용
- 라운드는 크지 않고 정돈된 밀도의 컴포넌트 구성

TodoList 앱에는 이 방향을 그대로 복제하지 않고, 아래처럼 재해석해 적용한다.

- 인증 화면과 대시보드 모두 다크 UI를 기본값으로 사용
- 작업 중심 앱이므로 카드와 입력창의 대비를 GitHub보다 약간 더 높게 설정
- 성공/오류 상태를 명확히 보여주기 위해 상태 컬러는 GitHub보다 조금 더 분명하게 사용
- 모바일 터치 영역을 고려해 버튼과 입력 높이를 더 크게 유지

---

## 2. 색상 팔레트

### 2.1 역할별 색상

| 역할 | 색상명 | Hex | 사용 위치 |
| --- | --- | --- | --- |
| Primary | `brand` | `#2F81F7` | 주요 CTA, 링크, 포커스 링 |
| Primary Hover | `brand-strong` | `#1F6FEB` | Primary 버튼 hover |
| Secondary | `accent` | `#30363D` | 보조 버튼, 패널 강조 |
| Neutral Background | `bg-base` | `#0D1117` | 앱 전체 배경 |
| Neutral Surface 1 | `bg-elevated` | `#161B22` | 카드, 패널, 모달 |
| Neutral Surface 2 | `bg-muted` | `#21262D` | hover, 입력 배경, 리스트 hover |
| Neutral Border | `border-subtle` | `#30363D` | 기본 보더 |
| Neutral Text Main | `text-strong` | `#E6EDF3` | 본문, 제목 |
| Neutral Text Secondary | `text-muted` | `#8B949E` | 보조 텍스트 |
| Neutral Text Faint | `text-faint` | `#6E7681` | placeholder, 비활성 텍스트 |
| Success | `success` | `#238636` | 완료 상태, 성공 버튼 변형 |
| Success Soft | `success-soft` | `#2EA043` | 성공 hover, 뱃지 |
| Error | `danger` | `#DA3633` | 삭제 버튼, 오류 상태 |
| Error Soft | `danger-soft` | `#F85149` | 오류 배너 텍스트/아이콘 |
| Warning | `warning` | `#D29922` | 경고 배지, 주의 상태 |

### 2.2 Tailwind 커스텀 색상 설정

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
  darkMode: 'class',
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
  theme: {
    extend: {
      colors: {
        brand: {
          DEFAULT: '#2F81F7',
          strong: '#1F6FEB',
          soft: '#79C0FF',
        },
        accent: {
          DEFAULT: '#30363D',
          hover: '#3D444D',
        },
        surface: {
          base: '#0D1117',
          elevated: '#161B22',
          muted: '#21262D',
          overlay: '#1C2128',
        },
        border: {
          subtle: '#30363D',
          strong: '#484F58',
        },
        text: {
          strong: '#E6EDF3',
          muted: '#8B949E',
          faint: '#6E7681',
        },
        success: {
          DEFAULT: '#238636',
          soft: '#2EA043',
          faint: '#16331D',
        },
        danger: {
          DEFAULT: '#DA3633',
          soft: '#F85149',
          faint: '#30191B',
        },
        warning: {
          DEFAULT: '#D29922',
          faint: '#3B2F14',
        },
      },
      boxShadow: {
        panel: '0 0 0 1px rgba(48,54,61,0.8)',
        focus: '0 0 0 3px rgba(47,129,247,0.35)',
      },
      borderRadius: {
        xl2: '1rem',
      },
    },
  },
  plugins: [],
};
```

### 2.3 기본 배경 적용 기준

- 앱 루트: `bg-surface-base text-text-strong`
- 카드/패널: `bg-surface-elevated border border-border-subtle`
- hover 영역: `hover:bg-surface-muted`
- 보조 텍스트: `text-text-muted`

---

## 3. 타이포그래피

### 3.1 폰트 패밀리

GitHub와 유사한 기술 문서/도구형 톤을 유지하되, 웹앱 가독성을 위해 다음 조합을 권장한다.

- 본문/제목: `"Pretendard Variable", "Pretendard", "Noto Sans KR", sans-serif`
- 숫자/코드/메타 정보: `"JetBrains Mono", "Fira Code", monospace`

### 3.2 사이즈 스케일

| 용도 | Tailwind | 권장 값 |
| --- | --- | --- |
| App Title | `text-2xl md:text-3xl` | 24px / 30px |
| Page Title | `text-xl md:text-2xl` | 20px / 24px |
| Section Title | `text-base md:text-lg` | 16px / 18px |
| Body | `text-sm md:text-base` | 14px / 16px |
| Meta | `text-xs md:text-sm` | 12px / 14px |
| Button Label | `text-sm` | 14px |
| Input Text | `text-sm md:text-base` | 14px / 16px |

### 3.3 굵기

| 용도 | Tailwind |
| --- | --- |
| 브랜드명 / 메인 타이틀 | `font-semibold` 또는 `font-bold` |
| 섹션 제목 | `font-semibold` |
| 본문 | `font-normal` |
| 메타 정보 | `font-normal` |
| 버튼 | `font-medium` |

### 3.4 줄간격

| 용도 | Tailwind |
| --- | --- |
| 큰 제목 | `leading-tight` |
| 일반 본문 | `leading-6` |
| 짧은 메타 텍스트 | `leading-5` |

### 3.5 기본 텍스트 조합

- 페이지 제목: `text-xl md:text-2xl font-semibold tracking-tight text-text-strong`
- 본문: `text-sm md:text-base leading-6 text-text-muted`
- 메타 정보: `text-xs md:text-sm text-text-faint`

---

## 4. 공통 컴포넌트 스타일

## 4.1 버튼

### Primary Button

용도:
- 회원가입
- 로그인
- Todo 추가

권장 클래스:

```text
inline-flex items-center justify-center gap-2 rounded-lg border border-transparent
bg-brand px-4 py-2.5 text-sm font-medium text-white transition-colors
hover:bg-brand-strong focus:outline-none focus:ring-2 focus:ring-brand/50
disabled:cursor-not-allowed disabled:opacity-50
```

### Secondary Button

용도:
- 보조 액션
- 취소, 닫기, 일반 이동 버튼

권장 클래스:

```text
inline-flex items-center justify-center gap-2 rounded-lg border border-border-subtle
bg-surface-elevated px-4 py-2.5 text-sm font-medium text-text-strong transition-colors
hover:bg-surface-muted focus:outline-none focus:ring-2 focus:ring-brand/40
disabled:cursor-not-allowed disabled:opacity-50
```

### Danger Button

용도:
- Todo 삭제

권장 클래스:

```text
inline-flex items-center justify-center gap-2 rounded-lg border border-danger/40
bg-danger-faint px-3 py-2 text-sm font-medium text-danger-soft transition-colors
hover:bg-danger/20 hover:text-white focus:outline-none focus:ring-2 focus:ring-danger/40
disabled:cursor-not-allowed disabled:opacity-50
```

### 버튼 크기 기준

- 모바일 기본 높이: `h-11`
- 데스크톱 기본 높이: `h-10` 또는 `h-11`
- 아이콘 전용 버튼 최소 터치 영역: `h-11 w-11`

## 4.2 입력폼

### 기본 상태

```text
w-full rounded-lg border border-border-subtle bg-surface-base px-3.5 py-2.5
text-sm text-text-strong placeholder:text-text-faint
transition-colors outline-none
```

### 포커스 상태

```text
focus:border-brand focus:ring-4 focus:ring-brand/15
```

### 에러 상태

```text
border-danger text-text-strong focus:border-danger focus:ring-danger/15
```

### 입력 라벨 / 도움말 / 에러 문구

- 라벨: `mb-1.5 block text-sm font-medium text-text-strong`
- 도움말: `mt-1 text-xs text-text-faint`
- 에러: `mt-1 text-xs text-danger-soft`

### 입력 그룹 권장 패턴

```text
space-y-1.5
```

## 4.3 카드 / 리스트 아이템

### 인증 카드

```text
w-full max-w-md rounded-xl border border-border-subtle bg-surface-elevated
p-6 sm:p-7 shadow-panel
```

### 대시보드 패널 카드

```text
rounded-xl border border-border-subtle bg-surface-elevated p-4 md:p-5 shadow-panel
```

### Todo 리스트 아이템

```text
group flex items-start gap-3 rounded-lg border border-border-subtle
bg-surface-elevated px-4 py-3 transition-colors hover:bg-surface-muted
```

### 완료된 Todo 아이템

```text
border-border-subtle bg-surface-base text-text-faint opacity-90
```

추가 스타일:
- 완료 제목: `line-through text-text-faint`
- 생성일: `text-xs text-text-faint`

## 4.4 헤더 / 네비게이션

### 앱 헤더

GitHub 상단 바와 비슷하게 얇고 넓은 헤더를 사용하되, 앱 목적에 맞게 더 단순하게 유지한다.

권장 클래스:

```text
sticky top-0 z-30 border-b border-border-subtle bg-surface-base/95
backdrop-blur supports-[backdrop-filter]:bg-surface-base/80
```

내부 레이아웃:

```text
mx-auto flex h-14 w-full max-w-5xl items-center justify-between px-4 sm:px-6 lg:px-8
```

브랜드 텍스트:

```text
text-base font-semibold tracking-tight text-text-strong
```

보조 네비게이션 / 사용자 메타:

```text
text-sm text-text-muted
```

---

## 5. 반응형 브레이크포인트 적용 기준

### 5.1 기본 기준

- `sm`: 640px 이상
- `md`: 768px 이상
- `lg`: 1024px 이상

### 5.2 적용 원칙

#### 모바일 `< sm`

- 기본 설계 기준
- 단일 컬럼 중심
- 버튼은 가급적 전체 폭 또는 큰 터치 영역 유지
- 인증 카드는 좌우 여백 `px-4`
- Todo 생성 폼은 세로 배치 가능

#### `sm`

- 인증 카드와 대시보드 패널 폭 제한 시작
- 버튼과 입력을 한 줄에 배치하기 시작
- 리스트 여백과 패딩을 소폭 증가

#### `md`

- 페이지 최대 폭을 명확히 제어
- 인증 화면은 중앙 고정 카드
- Todo 헤더, 생성 폼, 리스트의 공간 구분을 더 크게 줌
- 제목 크기 한 단계 확대

#### `lg`

- 대시보드 전체 최대 폭 `max-w-5xl` 또는 `max-w-6xl`
- 진행 중 / 완료됨 섹션을 필요 시 2컬럼으로 확장 가능
- 헤더에서 사용자 정보와 액션 버튼을 여유 있게 노출

### 5.3 화면별 레이아웃 기준

- 인증 화면:
  `min-h-screen flex items-center justify-center px-4 sm:px-6`
- 대시보드:
  `mx-auto w-full max-w-5xl px-4 py-6 sm:px-6 lg:px-8`
- Todo Composer:
  모바일 `flex-col`, `sm` 이상 `flex-row`

---

## 6. 다크모드 지원 여부 및 기준 색상

### 6.1 지원 여부

- 지원: `예`
- 정책: MVP에서는 `다크모드 기본`, 필요 시 추후 라이트모드 확장

이 판단의 이유:

- 참조 스크린샷이 다크 기반이며, 현재 설계 방향과 가장 자연스럽게 맞는다.
- Todo 앱은 장시간 사용하는 화면이므로 저광량 환경에서 다크 테마가 잘 맞는다.
- 인증 화면과 대시보드 모두 동일 톤을 유지하기 쉽다.

### 6.2 다크모드 기준 색상

| 요소 | 클래스 |
| --- | --- |
| 앱 배경 | `bg-surface-base` |
| 카드 배경 | `bg-surface-elevated` |
| hover 배경 | `hover:bg-surface-muted` |
| 메인 텍스트 | `text-text-strong` |
| 보조 텍스트 | `text-text-muted` |
| 보더 | `border-border-subtle` |
| 포커스 | `ring-brand/40` |
| 성공 | `text-success-soft bg-success-faint` |
| 오류 | `text-danger-soft bg-danger-faint` |

### 6.3 라이트모드 확장 시 기준

향후 라이트모드를 추가한다면 아래 원칙을 따른다.

- 레이아웃 구조와 spacing은 유지
- 명암 구조만 반전
- Primary 색상은 동일 계열 유지
- 상태 색상은 대비 기준을 WCAG에 맞게 재조정

현재 단계에서는 다크모드만 구현해도 무방하다.

---

## 7. 컴포넌트별 적용 예시

### 7.1 로그인/회원가입 카드 래퍼

```text
mx-auto w-full max-w-md rounded-xl border border-border-subtle
bg-surface-elevated p-6 shadow-panel sm:p-7
```

### 7.2 Todo 생성 입력 + 버튼

```text
flex flex-col gap-3 sm:flex-row
```

입력:

```text
flex-1 rounded-lg border border-border-subtle bg-surface-base px-3.5 py-2.5
text-sm text-text-strong placeholder:text-text-faint
focus:border-brand focus:ring-4 focus:ring-brand/15
```

버튼:

```text
inline-flex h-11 items-center justify-center rounded-lg bg-brand px-4
text-sm font-medium text-white hover:bg-brand-strong
focus:outline-none focus:ring-2 focus:ring-brand/50
```

### 7.3 Todo 아이템

```text
flex items-start gap-3 rounded-lg border border-border-subtle
bg-surface-elevated px-4 py-3 hover:bg-surface-muted
```

### 7.4 오류 배너

```text
rounded-lg border border-danger/40 bg-danger-faint px-4 py-3
text-sm text-danger-soft
```

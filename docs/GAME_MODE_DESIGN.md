# 대한민국 헌법 타자 연습 - 게임 모드 기획서

## 📋 문서 정보
- **프로젝트명**: 대한민국 헌법 타자 연습
- **문서 버전**: 1.0
- **작성일**: 2025-11-18
- **문서 목적**: 타자 연습 게임화(Gamification)를 통한 사용자 참여도 및 학습 효과 증대

---

## 🎯 기획 목표

### 핵심 목표
1. **재미 요소 추가**: 단순 연습을 넘어 게임적 요소로 동기 부여
2. **지속적 참여 유도**: 진행형 콘텐츠 및 도전 과제로 재방문 유도
3. **학습 효과 극대화**: 헌법 내용을 자연스럽게 학습
4. **성취감 제공**: 기록 갱신, 배지 획득 등 가시적 성과

### 타겟 사용자
- 타자 연습이 필요한 학생 및 직장인
- 헌법 학습이 필요한 수험생
- 타자 게임을 즐기는 캐주얼 게이머
- 자기계발에 관심 있는 일반 사용자

---

## 🎮 게임 모드 상세 기획

### 1. 헌법 마스터 모드 (Constitution Master Mode)

#### 개요
- **장르**: 진행형 챌린지, 컬렉션
- **플레이 시간**: 제한 없음 (누적 플레이)
- **난이도**: 하 (초보자 친화적)

#### 게임플레이
```
[시작] → [제1조 조항 선택] → [타자 입력] → [평가] → [별점 획득] → [다음 조항 해금]
```

1. 헌법 제1조부터 제39조까지 순차적 진행
2. 각 조 내 항(1), (2), (3)... 도 별도 항목으로 구분
3. 총 93개 조항 완성 시 "헌법 마스터" 달성

#### 평가 기준
| 정확도 | 획득 별 | 상태 |
|--------|---------|------|
| 95% 이상 | ⭐⭐⭐ | 완벽 |
| 90-94% | ⭐⭐ | 우수 |
| 85-89% | ⭐ | 통과 |
| 85% 미만 | - | 재도전 필요 |

#### 칭호 시스템
- **0-30점**: 🌱 견습 입법자
- **31-90점**: 📚 헌법 학도
- **91-180점**: ⚖️ 법률 전문가
- **181-240점**: 👨‍⚖️ 헌법 해설가
- **241-279점**: 🏛️ 헌법 마스터

#### 진행률 UI
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
헌법 마스터 진행률: 15/93 (16.1%)
획득 별: 42/279 ⭐⭐⭐
현재 칭호: 📚 헌법 학도
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

#### 데이터 저장 (LocalStorage)
```javascript
{
  "constitutionMaster": {
    "completedArticles": [0, 1, 2, 3, ...],
    "stars": {
      "0": 3,  // 제1조 (1) - 3점
      "1": 2,  // 제1조 (2) - 2점
      ...
    },
    "totalStars": 42,
    "lastPlayedIndex": 15,
    "title": "헌법 학도"
  }
}
```

---

### 2. 60초 스피드 챌린지 (60 Second Speed Challenge)

#### 개요
- **장르**: 타임 어택
- **플레이 시간**: 60초
- **난이도**: 중

#### 게임플레이
```
[난이도 선택] → [카운트다운 3,2,1] → [60초 타이머 시작] → [문장 연속 입력] → [결과 화면]
```

1. 60초 타이머 시작과 동시에 첫 문장 표시
2. 문장 완성 시 즉시 다음 문장으로 자동 전환
3. 오타 발생 시 해당 문자부터 다시 입력 (시간은 계속 흐름)
4. 60초 종료 시 완료한 문장 수 집계

#### 난이도 옵션
- **쉬움**: 15자 이하 짧은 조항만 (예: "제1조 (1) 대한민국은 민주공화국이다.")
- **보통**: 모든 조항 랜덤
- **어려움**: 30자 이상 긴 조항만

#### 점수 계산
```
최종 점수 = (완료 문장 수 × 100) + (평균 WPM × 10) + (정확도 × 5)

예시:
- 완료 문장: 8개 → 800점
- 평균 WPM: 120 → 1200점
- 정확도: 94% → 470점
= 총 2470점
```

#### 결과 화면
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⏱️ 60초 스피드 챌린지 결과
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
완료 문장:        8개
평균 WPM:         120
정확도:           94%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
최종 점수:        2470점
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏆 개인 최고 기록: 2650점
   (2025.11.15 달성)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

#### 기록 저장
```javascript
{
  "speedChallenge": {
    "easy": {
      "bestScore": 2650,
      "bestDate": "2025-11-15",
      "bestSentences": 10,
      "bestWPM": 135
    },
    "normal": { ... },
    "hard": { ... }
  }
}
```

---

### 3. 정확도 퍼펙트 모드 (Perfect Accuracy Mode)

#### 개요
- **장르**: 하드코어 챌린지
- **플레이 시간**: 제한 없음
- **난이도**: 상

#### 게임플레이 룰
```
⚠️ 특별 규칙:
1. 백스페이스 키 사용 불가
2. 오타 발생 시 즉시 실패 (빨간 화면 플래시)
3. 연속 성공 문장 수가 점수
```

#### 긴장감 연출
- 입력 중 화면 테두리가 미세하게 빛남 (집중도 표현)
- 오타 발생 시:
  - 화면 빨간색 플래시
  - 진동 효과 (지원 기기)
  - "실패!" 텍스트 표시
- 연속 성공 시:
  - 5개: "훌륭합니다!" 메시지
  - 10개: "놀라운 집중력!" + 금색 효과
  - 20개: "완벽의 경지!" + 무지개 효과

#### 통계 화면
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 퍼펙트 모드 통계
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
역대 최고 기록:   23문장 연속 성공
오늘의 기록:      12문장
총 도전 횟수:     47회
성공률:           25.5%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

### 4. 헌법 퀴즈 모드 (Constitution Quiz Mode)

#### 개요
- **장르**: 타자 + 퀴즈
- **플레이 시간**: 문제당 30초
- **난이도**: 중

#### 문제 유형

**1. 빈칸 채우기**
```
문제: 대한민국의 주권은 _____에게 있고, 모든 권력은 _____으로부터 나온다.
정답: 국민 / 국민
입력: [          ]
```

**2. 키워드 순서 맞추기**
```
문제: 다음 단어를 순서대로 입력하세요
보기: 민주공화국 / 대한민국
입력: [          ]
```

**3. 조항 번호 맞추기**
```
문제: "대한민국은 민주공화국이다"는 몇 조 몇 항인가?
입력: [     ] (예: 1-1)
```

#### 점수 시스템
- 정답: +100점
- 30초 내 정답: +50점 보너스
- 오답: 다음 문제 (점수 없음)
- 10문제 완료 후 총점 계산

---

### 5. 서바이벌 모드 (Survival Mode)

#### 개요
- **장르**: 아케이드 서바이벌
- **플레이 시간**: 생명 소진까지
- **난이도**: 중상

#### 게임플레이
```
시작: ❤️❤️❤️ (생명 3개)
↓
[문장 표시 + 타이머 시작]
↓
[입력 완료] → 조건 확인:
  - 정확도 80% 이상 + 시간 내: 성공 → 다음 문장
  - 정확도 80% 미만 또는 시간 초과: 생명 -1
↓
생명 0 → 게임 오버
```

#### 시간 제한 계산
```javascript
제한 시간(초) = (문장 글자 수 / 3) + 5

예시:
- "대한민국은 민주공화국이다." (14자) → 9.7초 (약 10초)
- "정당은 그 목적, 조직과 활동이..." (45자) → 20초
```

#### 난이도 증가 메커니즘
```
1-5 문장:   기본 시간
6-10 문장:  시간 -10% (긴장감 상승)
11-15 문장: 시간 -20%
16+ 문장:   시간 -30% (최대)
```

#### 점수 계산
```
최종 점수 = 완료 문장 수 × 평균 WPM × (평균 정확도 / 100)

예시:
- 완료: 18문장
- 평균 WPM: 110
- 평균 정확도: 92%
= 18 × 110 × 0.92 = 1821점
```

#### 부활 아이템 (선택 사항)
- 광고 시청 시 생명 +1 (1회 제한)
- 또는 "연속 5문장 완벽 입력 시 생명 +1" 보상

---

### 6. 데일리 챌린지 (Daily Challenge)

#### 개요
- **장르**: 일일 미션
- **플레이 시간**: 제한 없음 (1일 1회)
- **난이도**: 변동

#### 미션 생성 로직
```javascript
// 날짜 기반 시드로 매일 동일한 문제 생성
const seed = new Date().toISOString().split('T')[0]; // "2025-11-18"
const dailyIndices = seededRandom(seed, 5); // 5개 문장 선택
```

#### 미션 구조
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📅 2025년 11월 18일 데일리 챌린지
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
오늘의 목표: 5개 문장 완성 (정확도 90% 이상)

진행 상황:
✅ 제1조 (1) - 정확도 96% ⭐⭐⭐
✅ 제5조 (2) - 정확도 91% ⭐⭐
⬜ 제12조 (1)
⬜ 제23조 (3)
⬜ 제37조 (1)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

#### 보상 시스템

**일일 완료 보상**
- 🏅 데일리 스탬프 획득
- 개인 통계에 "완료일" 기록

**연속 달성 보상**
```
3일 연속:  🔥 "꾸준함" 배지
7일 연속:  🌟 "일주일 개근" 배지
30일 연속: 👑 "완벽주의자" 배지
```

#### 로컬 순위표
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 오늘의 순위 (내 기기)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1위  오전 9시   평균 WPM 145  정확도 98%
2위  오후 2시   평균 WPM 132  정확도 96%
3위  오후 8시   평균 WPM 128  정확도 94% ← 현재
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 🛠️ 기술 사양

### 데이터 저장 (LocalStorage)

```javascript
// 전체 저장 구조
const gameData = {
  // 헌법 마스터 모드
  constitutionMaster: {
    completedArticles: [0, 1, 2, ...],
    stars: { "0": 3, "1": 2, ... },
    totalStars: 42,
    lastPlayedIndex: 15,
    title: "헌법 학도"
  },

  // 60초 스피드 챌린지
  speedChallenge: {
    easy: {
      bestScore: 2650,
      bestDate: "2025-11-15",
      bestSentences: 10,
      bestWPM: 135,
      playCount: 23
    },
    normal: { ... },
    hard: { ... }
  },

  // 퍼펙트 모드
  perfectMode: {
    bestStreak: 23,
    todayBest: 12,
    totalAttempts: 47,
    totalSuccess: 12
  },

  // 서바이벌 모드
  survivalMode: {
    bestScore: 1821,
    bestSentences: 18,
    bestWPM: 110,
    playCount: 15
  },

  // 데일리 챌린지
  dailyChallenge: {
    completedDates: ["2025-11-15", "2025-11-16", "2025-11-18"],
    currentStreak: 2,
    longestStreak: 7,
    stamps: 15,
    badges: ["꾸준함", "일주일 개근"]
  },

  // 퀴즈 모드
  quizMode: {
    bestScore: 850,
    totalQuestions: 120,
    correctAnswers: 98
  }
};

// 저장 키
localStorage.setItem('koreaConstitutionTyping_gameData', JSON.stringify(gameData));
```

### UI 컴포넌트

#### 모드 선택 화면
```html
<div class="game-mode-selector">
  <div class="mode-card" data-mode="master">
    <div class="mode-icon">🏛️</div>
    <h3>헌법 마스터</h3>
    <p>93개 조항을 순서대로 완성하세요</p>
    <div class="progress">15/93 완료</div>
  </div>

  <div class="mode-card" data-mode="speed">
    <div class="mode-icon">⏱️</div>
    <h3>60초 챌린지</h3>
    <p>제한 시간 내 최대한 많이!</p>
    <div class="best-record">최고: 10문장</div>
  </div>

  <!-- 다른 모드 카드들... -->
</div>
```

#### 게임 중 HUD
```html
<!-- 서바이벌 모드 예시 -->
<div class="game-hud">
  <div class="lives">❤️❤️🖤</div>
  <div class="score">점수: 1245</div>
  <div class="sentences-count">문장: 12</div>
  <div class="timer">⏱️ 15초</div>
</div>
```

### 핵심 함수

```javascript
// 모드별 게임 시작
function startGameMode(mode) {
  switch(mode) {
    case 'master':
      startConstitutionMaster();
      break;
    case 'speed':
      startSpeedChallenge();
      break;
    case 'perfect':
      startPerfectMode();
      break;
    case 'survival':
      startSurvivalMode();
      break;
    case 'daily':
      startDailyChallenge();
      break;
    case 'quiz':
      startQuizMode();
      break;
  }
}

// 게임 데이터 저장
function saveGameData(mode, data) {
  const allData = JSON.parse(localStorage.getItem('koreaConstitutionTyping_gameData') || '{}');
  allData[mode] = { ...allData[mode], ...data };
  localStorage.setItem('koreaConstitutionTyping_gameData', JSON.stringify(allData));
}

// 게임 데이터 로드
function loadGameData(mode) {
  const allData = JSON.parse(localStorage.getItem('koreaConstitutionTyping_gameData') || '{}');
  return allData[mode] || getDefaultGameData(mode);
}

// 칭호 계산
function calculateTitle(totalStars) {
  if (totalStars >= 241) return "🏛️ 헌법 마스터";
  if (totalStars >= 181) return "👨‍⚖️ 헌법 해설가";
  if (totalStars >= 91) return "⚖️ 법률 전문가";
  if (totalStars >= 31) return "📚 헌법 학도";
  return "🌱 견습 입법자";
}

// 시간 제한 계산 (서바이벌)
function calculateTimeLimit(text, sentenceCount) {
  const baseTime = (text.length / 3) + 5;
  const difficultyMultiplier = sentenceCount <= 5 ? 1.0 :
                                sentenceCount <= 10 ? 0.9 :
                                sentenceCount <= 15 ? 0.8 : 0.7;
  return Math.ceil(baseTime * difficultyMultiplier);
}

// 데일리 문장 생성 (시드 기반)
function getDailySentences(dateString) {
  const seed = dateString.split('-').join('');
  const rng = seededRandom(parseInt(seed));
  const indices = [];
  for (let i = 0; i < 5; i++) {
    let index;
    do {
      index = Math.floor(rng() * sentences.length);
    } while (indices.includes(index));
    indices.push(index);
  }
  return indices.map(i => sentences[i]);
}

// Seeded Random 함수
function seededRandom(seed) {
  let state = seed;
  return function() {
    state = (state * 1103515245 + 12345) & 0x7fffffff;
    return state / 0x7fffffff;
  };
}
```

---

## 🎨 UI/UX 설계

### 네비게이션 구조

```
[메인 화면]
├─ [연습 모드] (기존)
│  ├─ 일반 타자 연습
│  └─ 각종 설정
│
└─ [게임 모드] (신규)
   ├─ 🏛️ 헌법 마스터
   ├─ ⏱️ 60초 챌린지
   ├─ 🎯 퍼펙트 모드
   ├─ ❤️ 서바이벌 모드
   ├─ 📅 데일리 챌린지
   └─ 📝 퀴즈 모드
```

### 화면 전환 플로우

```
[메인]
  ↓ (모드 선택 클릭)
[모드 상세 화면]
  - 설명
  - 난이도 선택 (해당 시)
  - 최고 기록
  - [시작하기] 버튼
  ↓ (시작하기 클릭)
[카운트다운: 3, 2, 1]
  ↓
[게임 플레이 화면]
  - 문장 표시
  - 입력란
  - HUD (점수, 생명, 타이머 등)
  ↓ (게임 종료)
[결과 화면]
  - 점수/기록
  - 통계
  - [다시하기] [메인으로]
```

### 반응형 디자인

```css
/* 모바일 우선 */
.mode-card {
  width: 100%;
  margin-bottom: 1rem;
}

/* 태블릿 이상 */
@media (min-width: 768px) {
  .game-mode-selector {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1.5rem;
  }
}

/* 데스크톱 */
@media (min-width: 1024px) {
  .game-mode-selector {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

### 다크모드 지원
- 기존 다크모드 토글 유지
- 게임 모드에서도 동일하게 적용
- 강조 색상:
  - 라이트: 노란색 (#FBBF24)
  - 다크: 금색 (#FCD34D)

---

## 📊 우선순위 및 로드맵

### Phase 1: MVP (최소 기능 제품)
**목표**: 게임 모드 기본 프레임워크 구축
**예상 기간**: 1-2주

- [ ] 모드 선택 화면 UI 구현
- [ ] LocalStorage 기반 데이터 관리 시스템
- [ ] 60초 스피드 챌린지 (보통 난이도만)
- [ ] 기본 통계 화면

### Phase 2: 핵심 모드 구현
**목표**: 가장 재미있는 2-3개 모드 완성
**예상 기간**: 2-3주

- [ ] 헌법 마스터 모드 전체 구현
  - [ ] 진행률 추적
  - [ ] 별점 시스템
  - [ ] 칭호 시스템
- [ ] 서바이벌 모드 구현
  - [ ] 생명 시스템
  - [ ] 동적 난이도 조정
- [ ] 60초 챌린지 난이도 옵션 추가

### Phase 3: 확장 모드
**목표**: 다양성 확보
**예상 기간**: 2주

- [ ] 퍼펙트 모드 구현
- [ ] 데일리 챌린지 구현
- [ ] 퀴즈 모드 구현 (선택)

### Phase 4: 폴리싱
**목표**: 사용자 경험 개선
**예상 기간**: 1-2주

- [ ] 애니메이션 효과 추가
- [ ] 사운드 효과 (선택)
- [ ] 배지 시스템 완성
- [ ] 튜토리얼 추가
- [ ] 성능 최적화

---

## 🔧 기술적 고려사항

### 성능
- LocalStorage 용량 제한 (보통 5-10MB)
  - 압축된 JSON 사용
  - 오래된 데이터 정리 로직
- 60fps 유지를 위한 렌더링 최적화
  - requestAnimationFrame 사용
  - 불필요한 DOM 조작 최소화

### 접근성
- 키보드만으로 모든 모드 플레이 가능
- 스크린 리더 지원 (ARIA 레이블)
- 색맹 모드 (색상만으로 정보 전달하지 않기)

### 브라우저 호환성
- 모던 브라우저 타겟 (ES6+)
- LocalStorage 지원 확인
- Fallback: 비회원 1회성 플레이

### 모바일 대응
- 터치 이벤트 지원
- 가상 키보드 호환
- 화면 크기별 레이아웃 조정

---

## 📈 성공 지표 (KPI)

### 사용자 참여도
- **DAU** (Daily Active Users): 일일 활성 사용자
- **재방문율**: 7일 내 재방문 비율
- **평균 플레이 시간**: 세션당 평균 시간

### 게임 모드별 지표
- **모드별 플레이 횟수**: 어떤 모드가 인기 있는지
- **완료율**: 시작 대비 완료 비율
- **평균 점수 증가율**: 사용자의 실력 향상

### 학습 효과
- **헌법 마스터 진행률**: 평균 완료 조항 수
- **정확도 개선**: 시간 경과에 따른 정확도 향상
- **WPM 증가**: 타자 속도 향상도

---

## 💡 향후 확장 아이디어

### 소셜 기능 (장기)
- 친구 간 점수 비교
- 온라인 리더보드
- 공유 기능 (SNS)

### 추가 콘텐츠
- 다른 법령 추가 (형법, 민법 등)
- 사용자 커스텀 문장 세트
- 역대 대통령 연설문

### 프리미엄 기능 (수익화)
- 광고 제거
- 테마 팩
- 상세 통계 분석

### 교육 기관 연계
- 학교/학원용 대시보드
- 진도 관리 시스템
- 성적표 출력

---

## 📝 참고 자료

### 유사 서비스 벤치마킹
- **한글 타자 연습**: https://taja.neocounter.com/
- **TypeRacer**: 경쟁 요소, 실시간 WPM
- **Keybr**: 진행형 학습, 통계
- **10FastFingers**: 간결한 UI, 순위표

### 게임화 이론
- **옥탈리시스 프레임워크**: 8가지 핵심 동기
  1. Epic Meaning (헌법 마스터 칭호)
  2. Development & Accomplishment (별점, 기록)
  3. Empowerment of Creativity (난이도 선택)
  4. Ownership & Possession (진행률, 배지)
  5. Social Influence (순위표)
  6. Scarcity & Impatience (데일리 챌린지)
  7. Unpredictability (랜덤 문장)
  8. Loss & Avoidance (서바이벌 생명)

---

## ✅ 체크리스트

### 개발 전 준비
- [ ] 기획서 검토 및 승인
- [ ] 기존 코드베이스 분석
- [ ] UI 목업/와이어프레임 작성
- [ ] 데이터 구조 설계 확정

### 개발 중
- [ ] Git 브랜치 전략 수립
- [ ] 코드 리뷰 프로세스
- [ ] 테스트 계획 수립

### 출시 전
- [ ] 크로스 브라우저 테스트
- [ ] 모바일 테스트
- [ ] 성능 테스트
- [ ] 사용자 테스트 (베타)

---

## 📞 연락처 및 피드백
- GitHub Issues: (프로젝트 저장소)
- 문의: (이메일/연락처)

---

**문서 끝**

# 🎨 dev-guide 스타일 HTML 문서 생성 지침

이 지침을 AI에게 제공하면 `dev-guide.html`과 동일한 디자인 언어로 문서를 생성합니다.

---

## 1. 전달할 핵심 컨텍스트

아래 문장을 프롬프트 앞에 붙여서 사용하세요.

```
다음 디자인 시스템을 따르는 HTML 단일 파일 문서를 작성해줘.
다크 테마, 사이드바 네비게이션, 챕터 구조를 갖춘 기술 가이드 형식이야.
```

---

## 2. 디자인 토큰 (CSS 변수)

문서 전체에서 반드시 아래 변수를 사용해야 합니다.

```css
:root {
  --bg:           #00212b;   /* 최외곽 배경 */
  --sidebar-bg:   #002d3b;   /* 사이드바 배경 */
  --surface:      #003347;   /* 카드 배경 */
  --surface2:     #003d54;   /* 강조 카드 / 테이블 헤더 */
  --border:       #0a5068;   /* 구분선 */
  --accent:       #2dd4bf;   /* 청록 — 주 강조색 */
  --accent2:      #34d399;   /* 초록 — 성공/낮음 */
  --accent3:      #fbbf24;   /* 노랑 — 경고/중간 */
  --accent4:      #f87171;   /* 빨강 — 위험/높음 */
  --text:         #daf0f4;   /* 본문 텍스트 */
  --text-muted:   #5fa8b8;   /* 보조 텍스트 */
  --sidebar-width: 260px;
  --code-bg:      #002d3b;
}
```

**추가 컬러** (챕터 번호, 배지 등에 사용):
- 퍼플: `#bc8cff` / 배경 `rgba(188,140,255,.15)`
- 시안: `#38bdf8` / 배경 `rgba(56,189,248,.15)`
- 오렌지: `#fb923c` / 배경 `rgba(251,146,60,.15)`
- 핑크: `#f472b6` / 배경 `rgba(244,114,182,.15)`

---

## 3. 레이아웃 구조

```
body (flex, row)
 ├── #sidebar  (fixed, 260px, 100vh, overflow-y: auto)
 └── #main     (margin-left: 260px, max-width: 960px, padding: 48px 64px)
```

### 3-1. 사이드바 구성 요소

```html
<nav id="sidebar">
  <!-- 로고 영역 -->
  <div class="logo">
    <h1>이모지 문서 제목</h1>
    <span>부제 / 메타 정보</span>
  </div>

  <!-- 네비게이션 섹션 (여러 개 반복) -->
  <div class="nav-section">
    <div class="nav-section-title">섹션명</div>
    <a class="nav-link" href="#anchor">링크 텍스트
      <span class="badge">기간 표시</span>  <!-- 선택 사항 -->
    </a>
  </div>
</nav>
```

### 3-2. 메인 영역 구성 요소

```html
<main id="main">

  <!-- 페이지 헤더 (문서 최상단 1회) -->
  <div class="page-header">
    <div class="tag">태그 레이블</div>
    <h1>문서 제목</h1>
    <p>한 줄 설명</p>
    <div class="meta-pills">
      <span class="meta-pill"><strong>키</strong> 값</span>
    </div>
  </div>

  <!-- 챕터 (반복) -->
  <section class="chapter" id="고유ID">
    <div class="chapter-header">
      <div class="chapter-num ch-COLOR">번호 or 이모지</div>
      <h2>챕터 제목</h2>
      <span class="weeks">기간 표시</span>  <!-- 선택 사항 -->
    </div>
    <!-- 챕터 본문 -->
  </section>

</main>
```

---

## 4. 챕터 번호 색상 클래스

챕터 번호 뱃지(`chapter-num`)에 아래 클래스 중 하나를 조합합니다.

| 클래스 | 색상 | 용도 예시 |
|--------|------|-----------|
| `ch-blue` | `--accent` 청록 | 기획, 개요 |
| `ch-green` | `--accent2` 초록 | 콘텐츠, 완료 |
| `ch-yellow` | `--accent3` 노랑 | UI/UX, 주의 |
| `ch-red` | `--accent4` 빨강 | 테스트, 위험 |
| `ch-purple` | `#bc8cff` 퍼플 | 핵심 시스템, AI |
| `ch-cyan` | `#38bdf8` 시안 | 설정, 일정 |
| `ch-orange` | `#fb923c` 오렌지 | 수익화, 경고 |
| `ch-pink` | `#f472b6` 핑크 | 출시, 마무리 |

---

## 5. 본문 컴포넌트

### 5-1. 콜아웃 (callout)

```html
<div class="callout TYPE">
  <div class="callout-icon">이모지</div>
  <div class="callout-body">
    <div class="callout-title">제목</div>
    <div class="callout-text">
      본문. <code>인라인 코드</code>도 사용 가능.
    </div>
  </div>
</div>
```

| TYPE | 색상 | 용도 |
|------|------|------|
| `info` | 청록 | 팁, 참고 |
| `warn` | 노랑 | 경고, 주의 |
| `danger` | 빨강 | 위험, 금지 |
| `success` | 초록 | 완료, 체크 |
| `purple` | 퍼플 | AI 활용, 특이사항 |

### 5-2. 테이블

```html
<div class="table-wrap">
  <table>
    <thead>
      <tr><th>열1</th><th>열2</th></tr>
    </thead>
    <tbody>
      <tr><td>값</td><td>값</td></tr>
    </tbody>
  </table>
</div>
```

**인라인 뱃지** (테이블 셀 내부에 사용):

```html
<span class="tag-pill tag-high">높음</span>   <!-- 빨강 -->
<span class="tag-pill tag-med">중간</span>    <!-- 노랑 -->
<span class="tag-pill tag-low">낮음</span>    <!-- 초록 -->
<span class="tag-pill tag-info">정보</span>   <!-- 청록 -->
```

### 5-3. 코드 블록 (접기/펼치기 포함)

```html
<div class="code-block">
  <div class="code-header">
    <span class="code-lang">언어명</span>       <!-- C#, JS, Python, Prompt 등 -->
    <span class="code-title">파일명 또는 설명</span>
    <!-- .code-toggle 버튼은 JS가 자동 생성 -->
  </div>
  <pre>코드 내용
<span class="kw">키워드</span>
<span class="ty">타입</span>
<span class="fn">함수</span>
<span class="st">문자열</span>
<span class="cm">// 주석</span>
<span class="at">어트리뷰트</span></pre>
</div>
```

> 코드 블록은 기본값 **접힘** 상태. JS가 자동으로 토글 버튼을 추가합니다.

### 5-4. 마일스톤 카드 그리드

```html
<div class="milestone-grid">
  <div class="milestone-card">
    <div class="m-week" style="color:var(--accent)">N주차</div>
    <div class="m-title">M숫자 · 마일스톤명</div>
    <div class="m-desc">짧은 설명</div>
  </div>
</div>
```

### 5-5. 간트 차트

```html
<div class="gantt">
  <!-- 주차 레이블 헤더 -->
  <div class="gantt-weeks">
    <div></div>
    <div class="gantt-week-labels">
      <span class="gwl">W1</span>
      <span class="gwl">W4</span>
      <!-- ... -->
    </div>
  </div>

  <!-- 행 (반복) -->
  <div class="gantt-row">
    <div class="gantt-label">작업명</div>
    <div class="gantt-track">
      <!-- left: 시작%, width: 기간% -->
      <div class="gantt-bar gb-COLOR" style="left:0%;width:25%">레이블</div>
    </div>
  </div>
</div>
```

**간트 바 색상 클래스**: `gb-blue` `gb-green` `gb-yellow` `gb-red` `gb-purple` `gb-cyan` `gb-orange` `gb-pink`

---

## 6. 필수 JavaScript (하단에 삽입)

아래 스크립트를 `</body>` 직전에 반드시 포함시킵니다.

```html
<script>
  // 사이드바 active 추적
  const links = document.querySelectorAll('#sidebar .nav-link[href^="#"]');
  const sections = [...links].map(l => document.querySelector(l.getAttribute('href'))).filter(Boolean);
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        links.forEach(l => l.classList.remove('active'));
        const link = document.querySelector(`#sidebar a[href="#${e.target.id}"]`);
        if (link) link.classList.add('active');
      }
    });
  }, { rootMargin: '-20% 0px -70% 0px', threshold: 0 });
  sections.forEach(s => obs.observe(s));

  // 부드러운 스크롤
  links.forEach(l => {
    l.addEventListener('click', e => {
      e.preventDefault();
      document.querySelector(l.getAttribute('href'))
        ?.scrollIntoView({ behavior: 'smooth', block: 'start' });
    });
  });

  // 코드블록 접기/펼치기
  const chevronSVG = `<svg width="12" height="12" viewBox="0 0 12 12" fill="none">
    <path d="M2 4L6 8L10 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>`;
  document.querySelectorAll('.code-block').forEach(block => {
    const header = block.querySelector('.code-header');
    const pre = block.querySelector('pre');
    if (!header || !pre) return;
    const inner = document.createElement('div');
    inner.className = 'code-body-inner';
    inner.appendChild(pre);
    const body = document.createElement('div');
    body.className = 'code-body';
    body.appendChild(inner);
    block.appendChild(body);
    const toggle = document.createElement('span');
    toggle.className = 'code-toggle';
    toggle.innerHTML = `<span class="toggle-label">펼치기</span>${chevronSVG}`;
    header.appendChild(toggle);
    header.addEventListener('click', () => {
      const isOpen = block.classList.toggle('open');
      toggle.querySelector('.toggle-label').textContent = isOpen ? '접기' : '펼치기';
    });
  });
</script>
```

---

## 7. 반응형 처리

```css
@media (max-width: 800px) {
  #sidebar { display: none; }
  #main { margin-left: 0; padding: 24px 20px 60px; }
}
```

---

## 8. AI 프롬프트 템플릿

아래 템플릿을 복사해 `[대괄호]` 부분만 바꿔서 사용하세요.

```
[주제]에 대한 기술 가이드 HTML 문서를 만들어줘.

## 디자인 요구사항
- 위에서 제공한 디자인 시스템(CSS 변수, 컴포넌트 클래스)을 그대로 사용할 것
- 단일 HTML 파일로 완성할 것 (CSS, JS 모두 인라인)
- 사이드바 네비게이션 + 챕터 구조 유지
- 다크 테마 (#00212b 배경)

## 문서 내용
- 제목: [문서 제목]
- 대상 독자: [타겟]
- 챕터 수: [N개]
- 챕터 목록:
  1. [챕터명] — [기간 또는 분량]
  2. [챕터명] — [기간 또는 분량]
  ...

## 포함할 컴포넌트
- [ ] 페이지 헤더 (meta-pills 포함)
- [ ] 간트 차트
- [ ] 마일스톤 카드
- [ ] 코드 블록 (언어: [C#/Python/JS/...])
- [ ] 콜아웃 (info / warn / danger / success / purple)
- [ ] 테이블 (tag-pill 뱃지 포함)

## 추가 요청
[자유롭게 작성]
```

---

## 9. 자주 쓰는 이모지 조합

| 용도 | 이모지 |
|------|--------|
| 기획 / 문서 | 📋 📝 🗂️ |
| 일정 / 타임라인 | 🗓 ⏱️ 📅 |
| 코드 / 개발 | 💻 🔧 ⚙️ |
| AI / 자동화 | 🤖 ⚡ 🧠 |
| 경고 / 위험 | ⚠️ 🚨 ❌ |
| 완료 / 성공 | ✅ 🚀 🎉 |
| 팁 / 정보 | 💡 📌 🔍 |
| 보안 / 법률 | 🔒 ⚖️ 🛡️ |

---

> **요약**: CSS 변수 → 레이아웃 구조 → 컴포넌트 클래스 → JS 3종 세트.  
> 이 네 가지만 지키면 어떤 주제든 동일한 스타일로 생성됩니다.

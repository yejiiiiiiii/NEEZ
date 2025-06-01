# codereview
셀프 리뷰&피드백

# ✨ NEEZ Clone Project
#### 프로젝트 소개

반응형 웹사이트 모작  
기술 : HTML, SCSS, JavaScript (Vanilla), IntersectionObserver, requestAnimationFrame  
프로그램 : 피그마, 비주얼스튜디오코드  
링크 : https://yejiiiiiiii.github.io/NEEZ/

---

## 🔍 Self Review

### 📁 1. 파일 구조 및 구성
- [x] 역할별 디렉토리 분리 (/css, /js, /images)  
- [x] 인라인 스타일 및 스크립트 제거 → 모든 CSS/JS 외부 파일로 분리  
- [x] SCSS 모듈화 및 파일 네이밍 일관성 유지  
- [ ] CSS 커스텀 프로퍼티 도입 고려 (다크 모드 및 테마 확장 대비)  
---

### 🧱 2. HTML 리뷰
html
<header class="header">
  <a href="index.html" class="header__logo">
    <img src="images/niez-logo.svg" alt="NEEZ 로고">
  </a>
  <nav class="navbar" aria-label="메인 내비게이션">
    <ul class="navbar__list">
      <li class="navbar__item"><a href="#about" class="navbar__link">ABOUT</a></li>
      <!-- 이하 생략 -->
    </ul>
    <button class="navbar__toggle" aria-label="메뉴 열기">
      <span class="icon-hamburger"></span>
    </button>
  </nav>
</header>

<main>
  <section class="main_visual" id="main">
    <h1 class="main_visual__title">Provides Value Beyond the Product</h1>
    <a href="#product" class="btn btn--primary">More Info</a>
  </section>

  <section class="section01" id="product">
    <h2 class="section01__title">PRODUCT</h2>
    <article class="section01__item">
      <img src="images/sofa1.jpg" alt="디에즈 모듈 소파">
      <h3 class="section01__item-name">디에즈 모듈</h3>
      <p class="section01__item-price">
        <span class="original">10,600,000원</span>
        <span class="sale">8,480,000원</span>
        <span class="discount">(20%)</span>
      </p>
    </article>
    <!-- 이하 상품 카드 반복 -->
  </section>
  <!-- 이어서 FEELIV, REVIEW, STORE, FOOTER 등 -->
</main>

<footer class="footer">
  <div class="footer__info">
    <p>(주)피앤엘 | 고객센터 1234-5678 | 부산광역시 수영구 ...</p>
    <p>© 2025 NEEZ. All rights reserved.</p>
  </div>
</footer>

- [ ]  의미론적 태그 사용 강화
- <section>마다 id와 role="region", aria-labelledby 속성 추가 고려
- <aside>나 <figure> 등 적절한 시맨틱 태그 검토
- [ ]  Heading 태그 계층 순차화
- 메인 비주얼에서 <h2> 대신 <h1> 사용
- 섹션별 제목을 <h2> → <h3> → <h4>로 계층 재정리
- [x] 모든 이미지에 alt 속성 적용
- [x] <header>, <nav>, <main>, <footer> 시맨틱 태그 제대로 활용
- [ ] 내비게이션 링크에 aria-current="page" 추가 → 현재 섹션 강조
- [ ] 불필요한 래퍼 <div> 최소화
- 예: 로고 <a> 안에 별도 래퍼 대신 직접 <a class="header__logo">로 관리

---

### 🎨 3. CSS 리뷰
/* _variables.scss */
$primary-color: #156bd8;
$secondary-color: #ff689b;
$text-color-dark: #333;
$bg-color-light: #fff;
$gap-large: 2rem;

/* _mixins.scss */
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* _header.scss */
.header {
  background-color: transparent;
  position: absolute;
  width: 100%;
  padding: 1rem 2rem;
  @include flex-center();

  &__logo img {
    width: 200px;
    transition: width 0.3s ease;
  }

  &--scrolled {
    background-color: $bg-color-light;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);

    & .header__logo img {
      width: 80px;
    }
  }
}

/* _navbar.scss */
.navbar {
  display: flex;
  justify-content: flex-end;
  align-items: center;

  &__list {
    display: flex;
    gap: $gap-large * 0.5;

    @media (max-width: 768px) {
      flex-direction: column;
      position: fixed;
      top: 0;
      right: -100%;
      width: 70%;
      height: 100%;
      background-color: $bg-color-light;
      transition: right 0.3s ease;
    }
  }

  &__link {
    color: $text-color-dark;
    font-size: 1rem;
    text-decoration: none;
    padding: 0.5rem 1rem;
    transition: color 0.2s;

    &:hover,
    &.is-active {
      color: $primary-color;
      font-weight: bold;
    }
  }

  &__toggle {
    display: none;
    background: none;
    border: none;
    cursor: pointer;

    @media (max-width: 768px) {
      display: block;
    }
  }

  &--open {
    & .navbar__list {
      right: 0;
    }
  }
}

/* _section01.scss */
.section01 {
  padding: 4rem 2rem;
  background-color: $bg-color-light;

  &__title {
    font-size: 2rem;
    color: $text-color-dark;
    margin-bottom: 2rem;
  }

  &__item-wrap {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: $gap-large;
  }

  &__item {
    background-color: $bg-color-light;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;

    &:hover {
      transform: scale(1.05);
      box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
    }

    &-name {
      font-size: 1.25rem;
      color: $text-color-dark;
      margin: 1rem;
    }

    &-price {
      font-size: 1rem;
      margin: 0 1rem 1rem;
      display: flex;
      gap: 0.5rem;

      .original {
        text-decoration: line-through;
        color: darken($text-color-dark, 30%);
      }

      .sale {
        font-weight: bold;
        color: $primary-color;
      }

      .discount {
        color: $secondary-color;
      }
    }
  }
}

/* _responsiveness.scss */
@media (max-width: 1024px) {
  html {
    font-size: 90%;
  }
}

@media (max-width: 768px) {
  html {
    font-size: 85%;
  }
}

@media (max-width: 360px) {
  html {
    font-size: 80%;
  }
}

- [x] SCSS 모듈화 및 파일 분리: 역할별로 _variables.scss, _mixins.scss, _header.scss, _navbar.scss, _section01.scss, _responsiveness.scss
- [x] BEM 네이밍 일관성: .header__logo, .navbar__link, .section01__item-wrap, .section01__item-name 등
- [x] 반응형 그리드 & 폰트 크기 조정: auto-fit과 minmax(280px, 1fr) 사용, @media로 폰트 스케일링
- [ ] CSS 커스텀 프로퍼티 미도입: SCSS 변수와 병행해 :root { --primary-color: … } 선언 권장
- [ ] 하드코딩된 색상·폰트 크기 변수화 필요 (color: #333333;, font-size: 1rem; 등)
- [ ] 공통 버튼 클래스 부재: .btn, .btn--primary, .btn--secondary 같은 유틸리티 클래스 생성 필요
- [ ] 중복 스타일 유틸리티 클래스 추출: .section02__cta, .section03__cta 등의 동일한 속성을 공통 클래스로 관리

---

### ⚙️ 4. JavaScript 리뷰
javascript
// main.js

// DOM 요소 캐싱
const header = document.querySelector('.header');
const headerLogo = document.querySelector('.header__logo img');
const navbar = document.querySelector('.navbar');
const mainVisual = document.querySelector('.main_visual');
const navLinks = document.querySelectorAll('.navbar__link');
const toggleBtn = document.querySelector('.navbar__toggle');
const mobileMenu = document.querySelector('.navbar__list');
const topBtn = document.querySelector('.top-btn');

// 모바일 메뉴 토글
function toggleMobileMenu() {
  const isOpen = mobileMenu.classList.toggle('navbar__list--open');
  document.body.style.overflow = isOpen ? 'hidden' : 'auto';
}
toggleBtn.addEventListener('click', toggleMobileMenu);

// 스크롤 시 로고 크기/위치 및 네비게이션 고정
function resizeLogoOnScroll() {
  const scrollY = window.scrollY;
  const mainHeight = mainVisual.offsetHeight;
  if (scrollY >= mainHeight - 50) {
    navbar.classList.add('navbar--fixed');
    header.classList.add('header--scrolled');
    headerLogo.style.width = '80px';
  } else {
    navbar.classList.remove('navbar--fixed');
    header.classList.remove('header--scrolled');
    const ratio = 1 - scrollY / (mainHeight * 0.5);
    const newWidth = Math.max(100, ratio * 200);
    headerLogo.style.width = `${newWidth}px`;
  }
}

// 현재 섹션 메뉴 강조
function highlightCurrentMenu(entries) {
  entries.forEach(entry => {
    const id = entry.target.id;
    const link = document.querySelector(`.navbar__link[href="#${id}"]`);
    if (entry.isIntersecting) {
      link.classList.add('is-active');
      link.setAttribute('aria-current', 'page');
    } else {
      link.classList.remove('is-active');
      link.removeAttribute('aria-current');
    }
  });
}
const observerOptions = { threshold: 0.5 };
const sectionObserver = new IntersectionObserver(highlightCurrentMenu, observerOptions);
document.querySelectorAll('section[id]').forEach(sec => sectionObserver.observe(sec));

// 스크롤 최적화
let ticking = false;
window.addEventListener('scroll', () => {
  if (!ticking) {
    window.requestAnimationFrame(() => {
      resizeLogoOnScroll();
      toggleTopBtn();
      ticking = false;
    });
    ticking = true;
  }
});

// 상단 이동 버튼 토글
function toggleTopBtn() {
  if (window.scrollY > 300) {
    topBtn.classList.add('is-visible');
  } else {
    topBtn.classList.remove('is-visible');
  }
}

// 상단 이동 버튼 클릭 시 부드러운 스크롤
topBtn.addEventListener('click', () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
});

- [x] DOM 요소를 한 번만 탐색해 변수에 저장 → 중복 탐색 최소화
- [x] 의미 있는 함수명 사용: toggleMobileMenu(), resizeLogoOnScroll(), highlightCurrentMenu(), toggleTopBtn()
- [x] IntersectionObserver 사용해 현재 섹션에 해당하는 메뉴 강조
- [x] requestAnimationFrame으로 스크롤 이벤트 최적화
- [ ] 함수 내부 로직을 더 작은 단위로 분리해 재사용성 향상
- 예: fixNavbar(), unfixNavbar() 함수로 분리
- [ ] DOM 요소 존재 여부 검증 추가 필요 (if (headerLogo) { … })
- [ ] 이벤트 리스너 해제 고려 (메모리 누수 방지)
- [ ] ES 모듈 분리 및 번들링(빌드 도구 도입) 검토

---

### 🎯 5. UX/UI 측면
- [x] 모바일 메뉴 토글(햄버거 아이콘) 정상 작동
- [x] 제품 카드 호버 시 확대(scale) 및 그림자 효과 → 명확한 시각적 피드백 제공
- [ ] 상단 이동 버튼(Top Button)
- 현재 즉시 이동 → CSS scroll-behavior: smooth; 적용해 부드럽게 전환
- 스크롤 위치에 따라 버튼 노출/숨김 로직 추가
- [ ] 현재 메뉴 활성화 상태 시각화
- 스크롤 위치에 따라 .is-active, aria-current="page" 토글
- [ ] 모바일 메뉴 열림 시 배경 스크롤 잠금
- 메뉴 오버레이 상태에서는 <body> overflow: hidden; 처리 필요
- [ ] CTA 버튼(“More Info”, “Store”) 대비 강화
- 배경색 대비, 호버 시 컬러 변화 등을 명확히 조정

---

## 🛠️ 개선 계획 (To-Do)
- [ ] HTML
- Heading 계층 재정리: <h1> → <h2> → <h3> 순으로 수정
- <section>마다 role="region" + aria-labelledby 속성 추가
- 내비게이션 링크에 aria-current="page" 토글 로직 보강
- 불필요한 <div> 래퍼 제거
- [ ] CSS/SCSS
- CSS 커스텀 프로퍼티(--primary-color, --text-color-dark, --bg-color-light 등) 도입
- 하드코딩된 색상·폰트 크기를 SCSS 변수로 대체
- 공통 버튼 클래스(.btn, .btn--primary, .btn--secondary) 생성
- 중복 스타일 유틸리티 클래스 추출
- 빌드 과정에서 CSS 압축 및 자동 벤더 프리픽스 적용(write-pfx)
- [ ] JavaScript
- 스크롤 핸들러 내부 로직 함수 분리 (예: fixNavbar(), unfixNavbar())
- DOM 요소 존재 여부 검증 추가
- 이벤트 리스너 해제 로직 고려
- ES 모듈 분리 후 빌드 도구(webpack, Rollup) 도입
- [ ] UX/UI
- 상단 이동 버튼 부드러운 스크롤 (scroll-behavior: smooth;) 적용
- 스크롤 위치에 따른 Top Button 노출/숨김 로직 추가
- 현재 메뉴 활성화 상태 표시 강화 (.is-active, aria-current)
- 모바일 메뉴 열림 시 배경 스크롤 잠금

---

## ✅ 참고 도구
- #VS Code: 코드 작성 및 SCSS 빌드(터미널 연동)
- #브라우저 개발자 도구 (Chrome DevTools):
- 요소 검사(Element Inspector), CSS 수정 실시간 확인
- 네트워크 탭(Network)으로 이미지·스크립트 로딩 상태 점검
- Performance 탭으로 렌더링 병목 확인
- Lighthouse로 기본 성능/접근성 보고서 확인
- #Figma: 원본 Neez 디자인 참조, 레이아웃·폰트·스페이싱 확인
- #GitHub Pages: 정적 파일 호스팅 및 배포 확인

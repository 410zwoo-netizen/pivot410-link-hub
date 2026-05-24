# PIVOT410 STUDIO · 외대점 링크 허브

인스타 프로필 링크용 허브 페이지.  
**도메인:** `link.pivotstudio.kr`  
**호스팅:** Vercel (본부 표준)  
**자산 일관성:** Pretendard + pivotstudio.kr 서브도메인 + 본부 디자인 정책

---

## 파일 구조

```
pivot410-link-hub/
├── index.html        ← 메인 페이지 (전체)
├── README.md         ← 이 파일
├── .gitignore
└── images/
    ├── logo-ink.webp        ← 헤더 로고 (22KB, 우선 로드)
    ├── logo-ink.png         ← 헤더 로고 폴백 (44KB)
    ├── cursor-symbol.png    ← 커스텀 커서 (검정 삼각형)
    ├── cursor-symbol-red.png ← 커스텀 커서 호버 (빨간 삼각형)
    └── cursor-symbol-cream.png ← 예비 (사용 안함)
```

---

## 자주 하는 수정 (본부 운영자용)

`index.html` 한 파일만 수정하면 됨. VS Code 또는 메모장으로 열어서 검색 + 교체.

### 1. 캠페인 마감일 변경

```html
<!-- 검색: data-deadline -->
<a ... data-deadline="2026-06-30">      ← 이 날짜 바꾸면 끝
  ...
  <span class="card-dday" data-dday-target="2026-06-30">   ← 둘 다 같은 날짜로
```

**자동 동작:**
- 8일 이상 남음 → `D-NN` 차분히 표시
- 2~7일 → 노란 박스 + 깜빡임
- 마감 당일 → `TODAY` 빠른 깜빡임
- 마감 후 → `마감` + 카드 자동 비활성화 (운영 사고 방지)

### 2. 카드 추가 (예: 여름 특강 추가)

기존 카드 블록 통째 복사하고 색상만 바꾸기. `index.html`에서 `<a href="https://idol-hufs.pivotstudio.kr" class="card card-idol"` 검색해서 카드 블록 전체 복사 → 색상 클래스만 변경.

**색상 클래스:**
- `card-idol` = 빨강
- `card-entrance` = 파랑
- `card-regular` = 초록
- `card-kids` = 핑크
- 새 색상 추가하려면 `<style>` 안에 `.card-summer { background: #COLOR; }` 추가

### 3. 카피 / URL 교체

`index.html`에서 직접 찾아 바꾸기:
- 전화번호: `tel:050714470733`
- 카톡: `http://pf.kakao.com/_QsUlX/chat`
- 인스타: `https://www.instagram.com/pivot410studio_hufs/`
- 지도: `https://naver.me/FG7ZYJih`
- 캠페인 URL: `https://idol-hufs.pivotstudio.kr`, `https://entrance-hufs.pivotstudio.kr`

### 4. 새 캠페인 알림 (드로어 안 이벤트 추가)

`<!-- TICKER DRAWER -->` 영역에 `<a class="event-item" ...>` 블록 추가.  
드로어 상단 `NOW HOT [2]`의 숫자도 같이 바꿔주기.

### 5. 로고 교체

`images/logo-ink.png` 와 `logo-ink.webp` 두 파일 동시 교체.  
교체 후 Vercel이 자동 재배포.

---

## 수정 후 반영 절차 (Vercel 자동 배포)

본부 표준 워크플로우:

```bash
# 로컬 폴더에서
cd /Users/ijiu/Desktop/피봇\ 외대점/pivot410-link-hub
# index.html 수정 후
git add .
git commit -m "캠페인 마감일 갱신 등 메모"
git push
```

`git push` 하면 Vercel이 자동으로 1~2분 안에 새 버전 배포. 별도 작업 없음.

**Git 없이 수정하고 싶다면:** GitHub 웹사이트(github.com/410zwoo-netizen/pivot410-link-hub) 들어가서 `index.html` 클릭 → 연필 아이콘 → 직접 수정 → "Commit changes" 클릭. Vercel이 자동 감지하고 배포.

---

## 본부 운영 사고 방지 체크리스트

수정 후 반드시 확인:
- [ ] 모바일에서 페이지 로딩 (3초 안에)
- [ ] D-day 카운터 정상 표시
- [ ] 전화번호 자동 연결 (모바일에서 탭 시 통화 앱 뜨는지)
- [ ] 카톡 / 지도 / 인스타 링크 외부 이동
- [ ] HTTPS 자물쇠 표시
- [ ] 외대점 인스타 프로필 링크가 `link.pivotstudio.kr` 가리키는지

---

## 자산 정책

- 폰트: Pretendard CDN
- 색상: 페이지마다 다름 (본부 디자인 정책)
- 도형 색상 시스템: 빨강(아이돌) / 파랑(입시) / 초록(정규/취미) / 핑크(키즈) / 노랑(액센트)
- 다점포 확장 시: 이 레포 통째로 복제 후 지점 정보·색상만 교체

---

## 트러블슈팅

**"카톡 / 지도 링크가 안 열림"**  
→ `http://pf.kakao.com/...` 또는 `https://naver.me/...` 형식 오타 확인. 모바일 앱 미설치 시 웹 브라우저로 폴백됨.

**"D-day가 안 바뀜"**  
→ `data-deadline`과 `data-dday-target` 두 군데 모두 같은 날짜로 변경했는지 확인. 페이지 새로고침 필수.

**"로고가 깨져서 안 보임"**  
→ `images/` 폴더의 `logo-ink.png` + `.webp` 둘 다 같이 푸시했는지 확인.

**"커서가 모바일에서도 보임"**  
→ 발생할 수 없는 상황 (`@media (hover: hover) and (pointer: fine)` 가드 처리됨). 만약 보이면 캐시 클리어 후 재접속.

---

## 본부 자산 연락처

운영: 이지우 (포텐사일공 교육사업부 디렉터)  
도메인: pivotstudio.kr (가비아)  
호스팅: Vercel

# 생성형 AI 기반 스타트업 컨설팅
> 본 프로젝트는 생성형 AI를 활용하여 기업 브랜드 진단 및 네이밍·컨셉·스토리·로고를 단계적으로 도출하는 브랜드 컨설팅 웹 서비스입니다.
사용자는 로그인 후, 단계적으로 컨설팅을 받을 수 있고 그 결과는 마이페이지에서 볼 수 있으며,
투자 게시판에 컨설팅 결과를 등록하여 투자에 도움이 될 수 있도록 설계하였습니다.

## 제작 기간
2025.12.29 ~ 2025.02.20
## 참여 인원
| ‍이름 | 역할 | 담당 업무                                                                                                                                                           |
|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| **김대호** | AI | • 프로젝트 PM <br> • 프로젝트 일관성 검증 개발  |
| **김효성** | Frontend | • 서비스 설계 <br> • UI/UX 개발 <br> • 성능 최적화 <br> • 서버 연동/오류 개선     |
| **이시연** | Frontend | • 서비스 기획 <br> • UI/UX 개발 <br> • JWT 인증/API 연동 <br> • CRUD 구현   |
| **장혁준** | Backend | • RestAPI 개발 <br> • FastAPI기반 서버 워크플로우 설계 <br> • AWS 구성 및 Docker 기반 배포 자동화 |
| **유대영** | AI | • 텍스트, 이미지 Agent 개발 <br> • Prompt 구조화   |
| **정현호** | AI | • 텍스트, 이미지 Agent 개발 <br> • Prompt 구조화




### 메인 화면
<img width="1919" height="944" alt="Image" src="https://github.com/user-attachments/assets/4d35b58d-be44-4185-8f1a-5ed6dd27cf0a" />

### 로그인 화면
<img width="1919" height="942" alt="Image" src="https://github.com/user-attachments/assets/59917b8e-adf8-4ad8-b391-1b4f5c3fb638" />

### 인터뷰 화면
<img width="1917" height="945" alt="Image" src="https://github.com/user-attachments/assets/2df8b381-f3e3-4e8a-b172-ef005772820a" />

### 마이페이지 화면
<img width="1919" height="944" alt="Image" src="https://github.com/user-attachments/assets/232bac7e-79cc-424f-a941-4270055a19e1" />

### 투자 라운지(게시판) 화면
<img width="1919" height="943" alt="Image" src="https://github.com/user-attachments/assets/ee1cf4f9-d0f0-4a1b-9875-29a72bde36f4" />

---

## Frontend 핵심 기능

### 1. 프론트엔드 기본 구조
- **React + Vite 기반 SPA(Single Page Application)** 구성
- React Router를 활용하여  
  `로그인 / 회원가입 / 메인 / 도서 상세 / 도서 등록·수정` 페이지 라우팅 설계
- 공통 AppBar + Container 레이아웃과 **MUI 커스텀 테마** 적용으로  
  일관된 버튼, 카드, 레이아웃 스타일 구현

### 2. 유저별 개인 서재
- 로그인 / 회원가입 화면 및 **기본 입력 검증 로직** 구현
- 로그인 성공 시, 사용자 정보를 `localStorage`에 저장하여 **로그인 상태 유지**
- 도서 데이터에 `ownerId`를 부여해  
  **각 사용자별로 자신의 서재 목록만** 보이도록 필터링 처리

### 3. 도서 관리 UI & CRUD
- **`MainPage`**
    - 도서 카드 목록, 제목/작가/장르 정보 미리보기
    - 제목 / 작가 / 장르 기반 검색 기능
    - 반응형 카드 레이아웃 및 hover 효과로 시각적인 강조
- **`BookRegisterPage`**
    - 제목, 작가, 장르, 줄거리, 표지 프롬프트 입력 후 도서 등록
- **`BookDetailPage`**
    - 선택한 도서의 상세 정보 및 표지 이미지 조회
- **`BookEditPage`**
    - 기존 데이터가 채워진 상태에서 도서 정보 수정 가능
    - 삭제 시 메인 페이지로 자연스럽게 이동하는 흐름 구성

### 4. AI 표지 이미지 생성 UI
- 도서 등록/수정 화면에 **AI 표지 프롬프트 + 옵션(모델, 품질, 스타일, 해상도)** 입력 UI 구성
- `AI 표지 생성` 버튼 클릭 시 OpenAI Images API 호출 →  
  응답으로 받은 이미지 URL을 표지 미리보기(`coverPreview`)로 즉시 표시
- 도서 등록/수정 시 해당 이미지 URL을 `imageUrl` 필드에 함께 담아 저장하도록 설계하여,  
  이후 메인/상세 화면에서 **AI로 생성된 표지 이미지가 그대로 활용**될 수 있도록 기반 마련

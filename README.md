# Library

> 아파트, 동네 작은 도서관에서 사용할만한 도서관 웹 사이트 + 관리자페이지 템플릿 제작 프로젝트

<br/>

## 대표화면
<table>
  <tr>
    <td><b>메인 페이지</b></td>
    <td><b>관리자 페이지</b></td>
  </tr> 
  <tr>
    <td><img src="/readme-file/main.png" alt="메인 페이지"></td>
    <td><img src="/readme-file/adminmain.png" alt="관리자 페이지"></td>
  </tr>
</table>

<br/>

## 어떤 서비스인가요?

- Library는 책 목록을 관리하고 도서 대출을 처리하는 곳으로, 사용자들이 다양한 도서 정보를 확인하고 책을 대출할 수 있는 웹사이트 입니다.

## Contents

Click to scroll to that page

1. How to start? : 시작 가이드
2. Project Info : 프로젝트 소개

- ​Project intention : 프로젝트 기획 의도
- Service : 서비스
- How can use this project?

3. Stacks : 사용 기술 스택
4. WEB MVP & Project tree : 주요 기능 및 프로젝트 구조

- 기능 소개
- ERD
- Architecture

5. Trouble Shooting : 트러블 슈팅
6. END with Members: 프로젝트 멤버 및 역할 소개

## 1. How to start : 시작 가이드

For building and running the application you need :

- [Node.js 18.16.1](https://nodejs.org/en)
- [npm 9.7.2](https://www.npmjs.com/)

Installation

```bash
git clone https://github.com/KJH1225/library.git
cd library
```

Front (library/client/)에서

```
npm install
npm run build
```

DB

```
library/server/database/sqlFile/library.sql 실행
library/server/config/config.json 파일의 development: {} 내용을 자신에 맞게 수정
```

Back (library/)에서

```
npm install
npm start
```

접속

```
http://localhost:8003 접속
```

## 💻 2. Project Info : 프로젝트 소개

### ✔️개발 기간

- 2024.01.08 ~ 2024.01.23 (2주)

- [개발 일정 구글 시트](https://docs.google.com/spreadsheets/d/1R1KUtuODEuizrx0bBrmfxCxtfQW6UtqwfBAnY3XxS_I/edit#gid=205256937)

### ✔️ 배포 서버

- www.i1004902.com/app4

### ✔️ 프로젝트 기획 의도

서비스 소개

- 책 목록: Library는 다양한 주제와 장르의 책을 손쉽게 찾아볼 수 있습니다. 직관적이고 정확한 검색 닝을 통해 사용자들은 자신에게 맞는 도서를 빠르게 찾을 수 있습니다.
- 도서 대출 및 반납: Library는 간편하고 빠른 도서 대출 및 반납 서비스를 제공합니다. 온라인으로 도서를 예약하고 대출 기간을 관리하는 것 뿐만 아니라, 편리한 반납을 통해 이용자들은 무리 없이 도서를 반환할 수 있습니다.
- 이벤트 및 프로모션: Libary에서는 관리자 페이지에서 다양한 도서 이벤트와 강좌를 주기적으로 개최하여 이용자들에게 더 많은 도서를 경험할 수 있는 기회를 제공할 수 있습니다.
  
기능 소개

- 책 목록 조회
- 책 설명 (상세 페이지)
- 도서 카트
- 이벤트
- 회원가입/탈퇴
- 로그인/로그아웃
- FAQ
- 마이페이지
- 대출 및 반납
- 관리자 페이지

### ✔️ 서비스

#### 서비스 설명
1. 웹 서비스의 최종적인 메인 기능과 서브 기능 설명

   1. 책 목록
      - 장르별 주제의 책 목록을 둘러보고 검색
      - 리뷰 평점 평균 확인 가능
      - 현재 대출 가능한지 여부 표시

    2. 책 설명 (상세 페이지)
        - 책 저자, 출판사, 소개 등 책 상세 설명
        - 대출 가능 여부 확인을 통해 예약 및 카트 기능
        - 리뷰를 통해 다른 이용자들의 평가 확인
        - 같은 저자, 출판사인 연관도서 추천
        
    3. 도서 카트
        - 카트에 넣은 책 목록 확인, 삭제
        - 체크 박스 선택을 통해 전체 or 원하는 책들만 대출 신청 기능
    
    4. 이벤트
        - 주기적으로 진행되는 이벤트와 개설 강좌 조회
        - 작가 강연, 도서 모임 등 다양한 기능
        - 신청 및 취소를 통해 인원 관리
    
    5. 회원가입/탈퇴 기능
        - 회원가입을 통해 서비스에 가입 및 이용 가능
        - 마이페이지에서 비밀번호 인증 후 회원 탈퇴
        - 네이버, 카카오, 구글 계정 회원가입과 연동 기능
    
    6. 로그인/로그아웃 기능
        - 네이버, 카카오, 구글 소셜 로그인 기능
        - 등록된 사용자 아이디, 비밀번호를 입력하여 로그인 
        - 서버는 입력된 정보를 검증 후 올바른 경우 accessToken, refreshToken 토큰 생성
        - 로그인이 필요한 서비스는 토큰 확인하여 유효 확인 후 서비스 이용 가능
        - Recoil 상태관리 라이브러리를 사용해 사용자 로그인 상태 관리
        - 서버에 요청을 보낼 때 토큰 유효성 확인 accessToken 만료시 refreshToken기간 확인해 refreshToken이 유효하다면 accessToken 재발급 아니라면 로그아웃 처리 후 로그인 페이지로 리다이렉트
        - 로그아웃 클릭 시 토큰을 지우고 로그아웃 처리
    
    7. FAQ
        - 공지사항 및 고객의 질문 답변
        - 카테고리별 질문 등록과 검색 및 카테고리 버튼을 질문 조회
        - 관리자 답변 시스템
        - 이용자가 작성한 질문 등록 및 관리 기능
   
    8. 마이페이지 기능
        - 마이페이지에서 개인 정보를 확인하고 수정 가능
        - 작성한 FAQ 내역 확인
        - 대출 중인 도서와 반납한 도서 목록 확인
        - 이벤트 신청/참여 내역 확인
          
    9. 대출 및 반납
        - 원하는 책을 도서 카트에 담아 대출
        - 세션 스토리지에 책을 저장 후 대출신청 버튼을 클릭 시 DB에 저장
          
    10. 관리자 페이지
        - 메인 페이지 하단 footer의 “관리자페이지” 버튼을 이용해 접속
        - 관리자 로그인을 후 페이지 관리
        - 책 등록, 조회, 수정, 삭제 기능
        - 배너 등록, 조회, 수정, 삭제 기능
        - Faq 공지사항 등록, 문의글 답변 작성, 수정, 삭제 기능
        - 대출 연장, 반납, 조회, 대출 도서의 정보 및 대출자 조회 기능
        - 사용자 등록, 조회, 관리 기능
        - 매뉴얼 탭에서 관리자 사용설명서 PDF 다운 
      
4. 유저 시나리오
  - WHO 
    - 책을 사랑하고 지식을 탐험하고자 하는 모든 이용자. 독서 애호가부터 새로운 취향을 찾고자 하는 이용자들까지 지적 성장을 추구하는 분들
  - WHAT
    - 다양한 장르와 주제의 도서 목록 제공, 온라인 상에서 손쉽게 책을 찾고 대출 예약을 할 수 있으며, 개설된 이벤트 및 강좌를 신청해 경험을 더욱 풍부하게
  - WHEN
    - 여가시간에 읽을 도서를 짧은 시간을 이용해 찾고 대출 예약, 개설된 강좌와 이벤트 신청
  - WHERE
    - 반응형 웹으로 온라인 플랫폼 어디서든 접속하여 이용. 사용자들은 휴대폰, 태블릿, 노트북 등 다양한 디바이스에서 이용하며 제한 없이 서비스 이용 
  - WHY
    - 도서를 효율적으로 관리하고 다양한 이벤트와 강좌를 통해 책을 더욱 즐겁게 읽고 편리한 온라인 플랫폼을 통해 언제 어디서든 자유롭게 이용 가능


### ✔️ 프로젝트 구조

#### 🧩 front-end

![front-end](/readme-file/front-end.svg)

- [Figma](https://www.figma.com/file/HPMp3fH03gnm2DGoSrhoFp/Untitled?type=design&mode=design&t=ae8A2zEzPWDRUevB-0)

  
> 페이지별 구조

- Main : 페이지 기반으로 구현된 서비스.
* Main : 메인페이지/ 경로 접속 시 라우팅되는 메인 페이지
* Booklist : 장르별 책 리스트 보여주는 페이지
* Bookdetail : 책 상세 정보 보여주는 페이지
* Cart : 원하는 책 선택 후 대출하는 도서카트 페이지
* Event : 진행중인 이벤트, 개설된 강좌를 보여주는 페이지
* Faq : 관리자 공지사항 및 유저 질문 보여주는 페이지
* Login : 로그인 페이지
* Join : 회원가입 페이지
* Mypage: 회원 계정 정보, 대출 및 반납 목록, FAQ, 리뷰 작성 페이지
* Admin : 페이지 관리 페이지
<br/><br/>
#### 🧩 back-end
<br/>

![back-end](/readme-file/back-end.svg)

> 로직 구조

- config : 환경변수 설정
- schemas : DB와 테이블 정의
- sqlFile : 초기 데이터 .sql파일 저장
- routes : 요청 받은 정보를 알맞게 전달
- controllers : 서비스로 요청 전달 및 응답
- services : controllers에서 요청받은 정보를 알맞게 가공하는 로직 수행 후 model에 전달
- model : services 에서 전달 받은 테이터로 DB CRUD 
- utils/token: JWT토큰 생성, 회원 인증
- utils/errorMiddleware: 에러처리 담당 미들웨어

<br/>

#### 🧩 ERD

<br/>

![ERD](/readme-file/ERD.png)

- [ERD 다이어그램](https://dbdiagram.io/d/Library-6597ad0dac844320ae4b51b1)

<br/>

#### 🧩 Architecture

![Architecture](/readme-file/Architecture.png)

<br/>

### ✔️ 페이지 구성

## 💻 3. Stacks

<img alt="Html" src ="https://img.shields.io/badge/HTML5-E34F26.svg?&style=for-the-badge&logo=HTML5&logoColor=white"/> <img alt="JavaScript" src ="https://img.shields.io/badge/JavaScript-F7DF1E.svg?&style=for-the-badge&logo=JavaScript&logoColor=black"/> <img alt="react" src ="https://img.shields.io/badge/react-61DAFB.svg?&style=for-the-badge&logo=react&logoColor=white"/> <img alt="node.js" src ="https://img.shields.io/badge/node.js-339933.svg?&style=for-the-badge&logo=node.js&logoColor=white"/> <img alt="express" src ="https://img.shields.io/badge/express-000000.svg?&style=for-the-badge&logo=express&logoColor=white"/> <img alt="Sequelize" src ="https://img.shields.io/badge/sequelize-52B0E7.svg?&style=for-the-badge&logo=sequelize&logoColor=white"/> <img alt="MySQL" src ="https://img.shields.io/badge/mysql-4479A1.svg?&style=for-the-badge&logo=mysql&logoColor=white"/> <img alt="MUI" src ="https://img.shields.io/badge/mui-007FFF.svg?&style=for-the-badge&logo=mui&logoColor=white"/> 

### 💻 Dependencies

<img alt="npm" src ="https://img.shields.io/badge/npm-CB3837.svg?&style=for-the-badge&logo=npm&logoColor=white"/> <img alt="axios" src ="https://img.shields.io/badge/axios-5A29E4.svg?&style=for-the-badge&logo=axios&logoColor=white"/> <img alt=".env" src ="https://img.shields.io/badge/.ENV-ECD53F.svg?&style=for-the-badge&logo=dotenv&logoColor=white"/> <img alt="multer" src ="https://img.shields.io/badge/multer-000000.svg?&style=for-the-badge&logo=multer&logoColor=White"/> <img alt="jsonwebtokens" src ="https://img.shields.io/badge/jsonwebtokens-000000.svg?&style=for-the-badge&logo=jsonwebtokens&logoColor=white"/>

### 🔗 Cooperation

<img alt="github" src ="https://img.shields.io/badge/github-000000.svg?&style=for-the-badge&logo=github&logoColor=white"/> <img alt="discord" src ="https://img.shields.io/badge/discord-5662F6.svg?&style=for-the-badge&logo=discord&logoColor=white"/>

### 🌏 With Deploy

<img alt="Amazon" src ="https://img.shields.io/badge/Amazon EC2-FF9900.svg?&style=for-the-badge&logo=amazonec2&logoColor=white"/> <img alt="nginx" src ="https://img.shields.io/badge/nginx-009639.svg?&style=for-the-badge&logo=nginx&logoColor=white"/> <img alt="pm2" src ="https://img.shields.io/badge/pm2-2B037A.svg?&style=for-the-badge&logo=pm2&logoColor=white"/>

## 5. 트러블 슈팅
 
 ### 1. Multer 업로드 후 이미지 표시 이슈
 
  - 문제: upload 폴더에 여러 폴더를 만들고 경로에 맞게 업로드 시 이미지가 표시되지 않는 문제
  - 해결책: multer 설정에서 destination 속성을 사용하여 파일 저장될 동적인 폴더 경로를 설정함. 경로 생성 시 업로드된 파일의 속성 등을 활용하여 각각 다른 폴더에 저장하도록 함

```
  const upload = multer({
    storage: multer.diskStorage({
      destination: function (req, file, cb) {
        console.log("멀터 req: ", req);
        console.log("멀터 file: ", file);
        if (file.fieldname == "bannerimg") {
          cb(null, "server/upload/banner/");
        }
        else if (file.fieldname == "bookimg") {
          cb(null, 'server/upload/book/');
        }else {
          cb(null, 'server/upload/');
        }
      },
      filename: function (req, file, cb) {
        cb(null, new Date().valueOf() + path.extname(file.originalname));
      },
    }),
  });
  
  app.post("/api/bannerimg", upload.single("bannerimg"), (req, res) => {
    const file = req.file;
    console.log("post(/image) file:", file);
    res.send({
      imageUrl: "/server/upload/banner/" + file.filename,
    });
  });

  ...
```
    
 ### 2. 반응형 디자인 및 코드 간소화

  - 문제: 다양한 화면 크기에 대응하지 않고 복잡한 코드 구조로 유지보수 어려움 문제
  - 해결책: 미디어 쿼리를 활용하여 화면 크기에 따라 스타일을 동적으로 설정 및 중복 코드를 제거하고 모듈화된 코드 구조를 채택하여 코드의 가독성을 높이고 유지보수를 용이하게 함.

## 6. END

- 한국정보교육원 웹 프론트엔드 클라우드 콘솔 개발자 양성과정 3회차 1조 

## ✔️프로젝트 멤버 구성

|  front-end   | back-end |
| :----------: | :------- |
| 김지환(팀장) | 김지환    |
|    김준녕    | 김준녕   |
|    임헌성    | 임헌성   |
|    박승균    |         |
|    백승준    | 백승준   |
|    김정혁    | 김정혁   |
|    유재혁    | 유재혁    |    
## 팀원별 역할

### 김지환(팀장)
- 네이버 카카오 구글 회원가입, 로그인, 계정 연동 구현 
- 백엔드 Cursor 방식의 페이지네이션 구현
- 이벤트 페이지, 이벤트 상세, 대출 관리 페이지 프론트 제작
- 프론트: 책, 로그인, 회원가입 페이지 
- 백엔드: 관리자 페이지 로그인, 관리자 페이지 회원관리 
- 반응형 디자인 및 UI 스타일링
- AWS EC2, NginX 활용하여 프로젝트 배포 (www.i1004902.com/app4)
- JWT accessToken, refreshToken과 Redis를 사용한 사용자 인증 구현
- Recoil 상태관리 라이브러리를 사용해 사용자 로그인 상태 관리
- 전체 백엔드, API구현 보조 및 DB 구조 설계

### 김준녕

- Faq 페이지
- 관리자 페이지 대시보드 구현
- 관리자 로그인 페이지
- 관리자 회원 관리 페이지
- 관리자 Faq 관리 페이지
- FAQ 백엔드
- 반응형 디자인 및 UI 스타일링


### 유재혁

- 로그인 페이지
- 회원가입 페이지
- 장바구니 페이지
- 장바구니, 대출관리 백엔드
- 반응형 디자인 및 UI 스타일링


### 김정혁

- 헤더, 푸터 컴포넌트
- 마이페이지 프론트엔드
- 관리자 리뷰 관리 페이지
- 마이페이지 백엔드
- 반응형 디자인 및 UI 스타일링

  
### 임헌성

- 메인 페이지
- 책 목록 페이지
- 책 상세 페이지
- 관리자 책 관리 페이지
- 관리자 리뷰 관리 페이지
- 관리자 배너 관리 페이지
- 배너, 책 백엔드
- 반응형 디자인 및 UI 스타일링

### 박승균

- 설명서 작성
- 관리자 사용설명서 페이지


### 백승준

- 이벤트 백엔드
- 관리자 대출 관리 페이지
- 관리자 이벤트 관리 페이지
- 반응형 디자인 및 UI 스타일링

  



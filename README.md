"GPT CODEX"는 Java 21과 Spring Boot 3를 기반으로 구축된 웹 애플리케이션입니다.
주요 기능은 Thymeleaf와 Bootstrap 5를 사용한 웹 페이지를 제공하며, ReactFlow를 사용한 별도의 디자이너(designer) 기능을 포함합니다.

🚀 주요 기술 스택 (Tech Stack)

Backend:

Java 21

Spring Boot 3

Lombok (보일러플레이트 코드 감소)

Frontend (Main):

Thymeleaf

Thymeleaf Layout Dialect (레이아웃 관리를 위함)

Bootstrap 5

Frontend (Designer):

React (ReactFlow)

Build Tool:

Gradle

📁 프로젝트 구조 (Project Structure)

프로젝트는 Spring Boot 백엔드(src)와 ReactFlow 프론트엔드(frontend)의 모노레포(monorepo) 형태로 구성될 수 있습니다.

gpt-codex/
├── frontend/         <!-- ReactFlow (디자이너) 프로젝트 루트 -->
│   ├── public/
│   ├── src/
│   │   └── ... (React components)
│   ├── package.json
│   └── ...
├── src/              <!-- Spring Boot 프로젝트 루트 -->
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── example
│   │   │           └── gptcodex
│   │   │               └── GptCodexApplication.java
│   │   ├── resources
│   │   │   ├── static
│   │   │   │   ├── css
│   │   │   │   ├── js
│   │   │   │   ├── images
│   │   │   │   └── designer/   <-- (ReactFlow 빌드 산출물이 위치할 곳)
│   │   │   ├── templates
│   │   │   │   ├── errors
│   │   │   │   ├── fragments
│   │   │   │   ├── layouts
│   │   │   │   └── pages
│   │   │   └── application.properties
...


Thymeleaf 템플릿 설명

layouts/default.html: Thymeleaf Layout Dialect를 사용하여 애플리케이션의 기본 페이지 구조를 정의합니다. fragments 폴더의 head, navbar, footer 등을 조립합니다.

fragments/: 재사용 가능한 모든 HTML 조각(헤더, 푸터 등)이 위치합니다.

pages/: 실질적인 비즈니스 로직과 콘텐츠를 담는 뷰 파일이 위치합니다. layouts/default.html의 콘텐츠 영역을 동적으로 대체하게 됩니다.

errors/: 404 Not Found, 500 Internal Server Error 등 커스텀 오류 페이지를 관리합니다.

ReactFlow (디자이너) 프로젝트

루트 frontend/ 디렉터리에 위치한 별도의 React 프로젝트입니다.

ReactFlow 라이브러리를 사용하여 그래픽 디자이너 UI를 제공합니다.

디자인 가이드: ReactFlow 예제는 너무 어렵지 않게, 기본 기능부터 차근차근 API 테스트를 해 볼수 있는 수준으로 디자인하도록 가이드합니다.

중요 (빌드): 이 프로젝트의 빌드 산출물(예: npm run build 후 생성되는 build 또는 dist 폴더의 내용)은 Spring Boot 백엔드가 정적 파일로 서빙할 수 있도록 src/main/resources/static/designer/ 경로로 복사되어야 합니다.

🏁 시작하기 (Getting Started)

사전 요구 사항

JDK 21

Gradle

Node.js 및 npm (ReactFlow 프로젝트 빌드를 위함)

(필요시) IDE (IntelliJ, VS Code, Eclipse 등)

IDE 사용 시 Lombok 플러그인을 설치해야 어노테이션 프로세싱이 정상 동작합니다.

본 프로젝트의 .gitignore 파일은 IntelliJ IDE 환경에 맞게 생성되었습니다.

빌드 및 실행 (Build and Run)

이 프로젝트는 ReactFlow 프론트엔드와 Spring Boot 백엔드의 빌드 단계를 모두 포함합니다.

프로젝트 클론:

git clone [저장소 URL]
cd gpt-codex


Frontend (ReactFlow) 빌드:

cd frontend
npm install
npm run build


빌드 결과물 복사:

frontend 프로젝트의 빌드 산출물(예: frontend/build 또는 frontend/dist 폴더 내의 모든 파일 및 폴더)을 Spring Boot의 정적 리소스 디렉터리로 복사합니다.

대상 경로: src/main/resources/static/designer/

(참고: 이 프로세스는 build.gradle에 태스크를 추가하여 자동화할 수 있습니다.)

Backend (Spring Boot) 실행:
프로젝트 루트 디렉터리(gpt-codex/)로 돌아옵니다.

cd ..
./gradlew bootRun


(참고: build.gradle에 프론트엔드 빌드 및 복사 태스크가 연동되어 있다면, ./gradlew build 또는 bootRun만으로 모든 과정이 처리될 수 있습니다.)

접속:

메인 애플리케이션 (Thymeleaf): http://localhost:8080

디자이너 (ReactFlow): http://localhost:8080/designer/index.html (또는 React 빌드 설정에 따른 진입점)

📄 라이선스 (License)

본 프로젝트는 [라이선스 이름] 라이선스를 따릅니다. (예: MIT, Apache 2.0)

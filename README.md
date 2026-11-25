# EchoBoard

EchoBoard는 **HackerLogin LoginDay** 프로젝트를 위해 제작한 웹 게시판입니다.

## 주요 기능

- 일반·비밀·공지 게시판과 게시판별 읽기·쓰기 권한 설정
- 게시글, 댓글, 반응, 파일 첨부
- 회원가입, 로그인, TOTP 기반 2단계 인증
- 관리자 페이지에서 게시판과 회원 관리

## 기술 스택

- **웹 서버 및 화면** · TypeScript, Express, EJS
- **데이터 저장** · Prisma, SQLite
- **세션 저장** · Redis
- **자동화 요청 방지** · hCaptcha, Cloudflare Turnstile

## 로컬 실행

Node.js 26과 npm을 준비하고, 로컬 Redis를 기본 주소인 `127.0.0.1:6379`에서 실행합니다. 저장소 루트에서 다음 명령을 실행합니다.

```sh
npm install
cp .env.example .env
```

`.env`가 이미 있다면 복사 명령을 건너뜁니다. `.env`에서 `SESSION_SECRET`과 `JWT_SECRET`을 서로 다른 임의 값으로 바꿉니다. 데이터베이스 경로, 포트, 초기 관리자 아이디는 각각 `DATABASE_URL`, `PORT`, `OWNER_NAME`에서 설정할 수 있습니다. 예제의 hCaptcha와 Turnstile 키는 테스트용입니다.

```sh
npx prisma migrate deploy
npx prisma generate
node --env-file=.env --import tsx src/index.ts
```

기본 설정에서는 [http://127.0.0.1:3000](http://127.0.0.1:3000)에서 접속할 수 있습니다. 초기 관리자 계정이 없으면 `/setup/admin`으로 이동합니다. 화면에서 `OWNER_NAME`에 해당하는 관리자 계정을 생성합니다.

## 라이선스

EchoBoard는 GNU Affero General Public License v3.0 (`AGPL-3.0-only`)을 따릅니다. [라이선스 전문](LICENSE)

## 면책 조항

**EchoBoard는 관련 법률이 허용하는 최대 범위에서 어떠한 명시적 또는 묵시적 보증도 없이 현 상태 그대로 제공됩니다.** 저작권자와 기여자는 상품성, 특정 목적에의 적합성, 보안, 정확성, 가용성, 무중단 운영을 보증하지 않습니다. 소프트웨어의 품질과 성능에 따른 위험은 사용자가 부담하며, 운영 환경의 설정, 접근 권한 관리, 백업 및 복구는 운영자의 책임입니다.

관련 법률이 책임을 요구하거나 별도의 서면 합의가 있는 경우를 제외하고, 저작권자와 기여자는 EchoBoard의 사용 또는 사용 불능으로 발생한 일반적·특별·부수적·결과적 손해에 대해 책임을 지지 않습니다. 여기에는 데이터 손실 또는 손상, 개인정보 유출, 서비스 중단, 영업 손실과 제3자가 입은 손해가 포함됩니다. 손해 발생 가능성을 사전에 통지받은 경우에도 적용됩니다. 보증 부인과 책임 제한의 적용 범위는 [AGPL 3.0 제15조부터 제17조](LICENSE#L587)를 따릅니다.

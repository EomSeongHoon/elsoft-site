# 이엘소프트 웹사이트 + 법무 페이지 (Firebase Hosting 배포)

회사 소개 원페이지 + 두 앱의 개인정보처리방침·이용약관을 호스팅하는 정적 사이트다.
**2026-07-08부로 GitHub Pages → Firebase Hosting(프로젝트 `elsoft-fe596`, 계정 founder@elsoftlab.com)으로
이전 완료** — 개인 GitHub 계정 공개 리포 부담 제거가 목적. 소스는 이 폴더(로컬)에만 있으면 된다.

## 라이브 URL

- **https://elsoftlab.com** (커스텀 도메인, 인증서 자동 갱신)
- https://elsoft-fe596.web.app (Firebase 기본 도메인, 백업 접근용)

## 구성
```
web/
  index.html                     회사 소개 (링크는 상대경로)
  404.html                       커스텀 404 (GitHub Pages와 달리 Firebase도 자동 인식)
  robots.txt / sitemap.xml       SEO
  favicon.ico                    루트 폴백 파비콘
  assets/
    hero.webp / hero.jpg         히어로 배경 (webp 서빙, jpg는 OG 카드용)
    method.webp / method.mp4     '일하는 방식' 포스터·애니메이션
    logo.svg / favicon-32.png / apple-touch-icon.png
  legal/                         두 앱 개인정보처리방침·이용약관 (스토어 심사 제출 URL)
```

## 배포 방법

```bash
cd /Users/emong/dev/elsoft
firebase24 deploy --only hosting
```

- ⚠️ 이 맥에서는 `firebase`가 아니라 **`firebase24`**(~/.local/bin의 래퍼)를 쓸 것 —
  기본 Node 22 + macOS Tahoe 조합에서 CLI 네트워크가 premature close로 깨지는 버그 우회(Node 24.18로 실행).
- 배포 설정은 워크스페이스 루트의 `firebase.json`(public=web, `**/.git/**`·CNAME·README 제외, 캐시 헤더) 참조.
- `web/.git`은 로컬 이력 보존용 — 배포에는 절대 포함되지 않아야 한다(ignore 유지 필수. 첫 배포 때
  노출 사고가 있었고 `**/.git/**` 추가로 해결).

## 스토어 심사에 넣을 개인정보처리방침 URL (최종 확정)

- 어린이타자연습: `https://elsoftlab.com/legal/hangultyping-privacy.html`
- 토닥스케치:     `https://elsoftlab.com/legal/todaksketch-privacy.html`

## DNS 메모 (등록기관 관리)

- `A elsoftlab.com → 199.36.158.100` (Firebase)
- `TXT hosting-site=elsoft-fe596` (소유 확인)
- `MX 1 smtp.google.com` — **구글 비즈니스 별칭 메일. 절대 삭제/변경 금지**
- (선택) `www` 서브도메인은 Firebase 콘솔에서 리다이렉트로 추가 가능 — 현재 미설정

## 히스토리

- ~2026-07-08: GitHub Pages(EomSeongHoon/elsoft-site)에서 서빙. 이전 절차는
  `../호스팅_이전_Firebase.md` 런북 참조. 이전 완료 후 GitHub 리포는 삭제/비공개 처리.

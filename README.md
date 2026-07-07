# 이엘소프트 웹사이트 + 법무 페이지 (GitHub Pages 배포용)

회사 소개 원페이지 + 두 앱의 개인정보처리방침·이용약관을 **무료로 공개 호스팅**하기 위한 정적 사이트다.
도메인(elsoftlab.com)을 사기 전에도 GitHub Pages로 **바로 공개 URL을 확보**할 수 있어, 앱 스토어 심사에
필요한 "개인정보처리방침 URL"을 즉시 제출할 수 있다.

## 구성
```
web/
  index.html                     회사 소개 (링크는 상대경로 → 서브경로/커스텀도메인 모두 호환)
  .nojekyll                      GitHub의 Jekyll 처리 우회(파일 그대로 서빙)
  legal/
    hangultyping-privacy.html    어린이타자연습 개인정보처리방침
    hangultyping-terms.html      어린이타자연습 이용약관
    todaksketch-privacy.html     토닥스케치 개인정보처리방침
    todaksketch-terms.html       토닥스케치 이용약관
```

## 배포(무료, 5분)
1. GitHub에서 새 저장소 생성 (예: `elsoft-site`, Public).
2. 이 `web/` 폴더 **안의 내용**(index.html, legal/, .nojekyll)을 저장소 루트에 올린다:
   ```bash
   cd /Users/emong/dev/elsoft/web
   git init && git add -A && git commit -m "site: 이엘소프트 소개 + 법무 페이지"
   git branch -M main
   git remote add origin https://github.com/<your-id>/elsoft-site.git
   git push -u origin main
   ```
3. 저장소 **Settings → Pages → Build and deployment → Source: Deploy from a branch →
   Branch: main / (root)** 저장.
4. 1~2분 뒤 사이트 공개:
   ```
   https://<your-id>.github.io/elsoft-site/
   ```

## 스토어 심사에 넣을 개인정보처리방침 URL

**도메인 구매 전(임시, GitHub Pages 기본 주소):**
- 어린이타자연습: `https://<your-id>.github.io/elsoft-site/legal/hangultyping-privacy.html`
- 토닥스케치:     `https://<your-id>.github.io/elsoft-site/legal/todaksketch-privacy.html`

**도메인(elsoftlab.com) 연결 후(최종):**
- 어린이타자연습: `https://elsoftlab.com/legal/hangultyping-privacy.html`
- 토닥스케치:     `https://elsoftlab.com/legal/todaksketch-privacy.html`

> 문서 본문·스토어 문안은 최종 도메인(elsoftlab.com) 기준으로 작성돼 있다. 임시로는 위 github.io
> 주소를 스토어 콘솔에 넣고, 도메인 연결 후 최종 주소로 교체하면 된다.

## 나중에 커스텀 도메인(elsoftlab.com) 연결하기
1. 가비아/후이즈에서 `elsoftlab.com`(+ `elsoftlab.co.kr`) 등록.
2. DNS에 GitHub Pages용 레코드 추가:
   - `A` 레코드 4개 → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - (또는 `www` 서브도메인은 `CNAME` → `<your-id>.github.io`)
3. 저장소 루트에 `CNAME` 파일 생성(내용 한 줄: `elsoftlab.com`) 후 push.
   또는 Settings → Pages → Custom domain 에 `elsoftlab.com` 입력.
4. DNS 전파(수십 분~수 시간) 후 `https://elsoftlab.com/` 로 서비스 + HTTPS 자동 발급.

> ⚠️ 도메인을 아직 소유하지 않은 상태에서는 CNAME 파일을 넣지 말 것(사이트가 안 열림).
> 소유·DNS 설정 후에만 추가한다.

## 사업자정보(문서 하단) 채움 상태
- 상호 이엘소프트 / 대표자 이현미 / 사업자등록번호 579-20-01949 — **반영됨**
- 사업장 주소: 사업자등록증의 정확한 소재지 한 줄로 최종 확인 필요(현재 "…402호 (별내동, 스카이프라자)")
- 통신판매업: 어린이타자연습 = 해당 없음 / 토닥스케치 = 거래 50회 미만 면제(일반과세자)

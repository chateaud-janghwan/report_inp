# 배포 & 로컬 실행

## 로컬 실행

이 앱은 빌드가 필요 없습니다. `index.html`을 브라우저에서 열기만 하면 됩니다.

- **더블클릭**: 파일 탐색기에서 `index.html`을 더블클릭 → 브라우저에서 바로 실행
- 배포된 사이트와 100% 동일하게 작동합니다. 배포가 막혀 있을 때 임시로 쓰기 좋습니다.

> 외부 리소스(SheetJS, JSZip, 글꼴, 공휴일 API)는 CDN에서 불러오므로 로컬 실행에도 인터넷 연결이 필요합니다. 공휴일 API가 막혀도 생성은 정상 동작하며 토요일 공휴일 색상만 생략됩니다.

## GitHub 업로드

### 방법 1 — 웹 UI (간단)
1. https://github.com/chateaud-janghwan/report_inp/upload/main 접속
2. `index.html`을 드롭
3. **Commit changes**

### 방법 2 — VS Code / git CLI
```bash
git clone https://github.com/chateaud-janghwan/report_inp.git
cd report_inp
# index.html 수정
git add index.html
git commit -m "vX.X: 변경 내용"
git push origin main
```

## Cloudflare 자동 배포

`main` 브랜치에 푸시하면 Cloudflare가 자동으로 배포합니다.

### 배포 확인 순서
1. 커밋 후 1~2분 대기(Cloudflare 빌드 시간)
2. 사이트를 **강력 새로고침**(Ctrl+Shift+R) 또는 시크릿 창으로 열기 — 브라우저 캐시가 옛 버전을 잡고 있는 경우가 가장 흔함
3. 제목 옆 버전 표시(`v3.1`) 확인. 생성 로그 첫 줄에도 `(앱 vX.X)`가 찍힘

### 배포가 안 될 때
Cloudflare 대시보드 → Workers & Pages → `report_inp` → **Deployments** 탭 확인:

- **새 배포가 성공(초록)인데 화면이 옛날** → 캐시 문제. 위 2번 재시도. 커스텀 도메인이면 Caching → Purge
- **새 배포가 실패(빨강)** → 빌드 로그 확인
- **새 배포가 아예 안 생김** → GitHub 연동이 안 걸린 것. Settings에서 Production branch가 `main`인지, 자동 배포 일시중지 아닌지, GitHub 연동 권한 만료 아닌지 확인

## 버전 넘버링

버전 마커는 두 곳에 있습니다. 코드 수정 후 **반드시 함께 올려야** 배포 확인이 가능합니다.

1. 헤더 제목 옆 `<span>` (예: `>v3.1</span>`)
2. 생성 로그 첫 줄 (예: `(앱 v3.1)`)

VS Code에서 두 문자열을 찾아 바꾸면 됩니다.

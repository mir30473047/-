우리 가족의 작은 방 ♡ — 첫 번째 버전

포함 파일
- index.html: 모바일 채팅 화면, 관계 수치, 기기 저장/백업 기능
- images/yuna.png: 유나의 전신 일러스트
- manifest.webmanifest, sw.js: PWA 기본 설정
- worker.js, wrangler.toml: OpenAI API를 안전하게 호출하는 Cloudflare Worker 코드

중요: GitHub Pages만으로는 AI API 키를 안전하게 보관할 수 없습니다. worker.js를 Cloudflare Workers 같은 서버에 배포하고 API 키를 Secret으로 저장해야 실제 AI 대화가 작동합니다. HTML에 API 키를 넣지 마세요.

1단계 — 화면 배포
1. 이 압축 파일을 풀고 index.html, manifest.webmanifest, sw.js, images 폴더를 GitHub 저장소 최상위에 올립니다.
2. 저장소 Settings → Pages에서 배포합니다.
3. 앱 화면과 로컬 저장 기능은 동작하지만 AI 서버 연결 전에는 실제 AI 답변이 나오지 않습니다.

2단계 — AI 서버 연결 (Cloudflare Workers)
1. Cloudflare 계정에서 Workers & Pages → Create → Worker를 만듭니다.
2. worker.js 내용을 Worker 편집기에 붙여 넣고 Deploy 합니다.
3. Worker Settings → Variables and Secrets에서 OPENAI_API_KEY 이름으로 Secret을 추가하고 OpenAI API 키를 입력합니다.
4. 선택 사항: APP_ACCESS_CODE Secret도 설정하면 앱에 접속 코드를 입력해야 API를 사용할 수 있습니다. 추측하기 어려운 값을 사용하고 공유하지 마세요.
5. wrangler.toml의 OPENAI_MODEL이 계정에서 사용할 수 있는 모델명인지 확인합니다. 모델 오류가 나오면 지원되는 모델명으로 바꾸세요.
6. Worker 주소를 확인하고 앱 설정의 AI 서버 주소에 https://내-worker주소/chat 형태로 입력합니다. APP_ACCESS_CODE를 설정했다면 같은 코드를 앱 설정에도 입력합니다.
7. 설정 저장 및 연결 확인을 누르고 메시지를 보내 테스트합니다.

비용과 저장
- OpenAI API 사용량에 따라 비용이 발생할 수 있습니다. API 대시보드에서 사용량을 확인하세요.
- 대화와 수치는 현재 기기의 localStorage에 저장됩니다. 앱 삭제/브라우저 데이터 삭제/기기 변경 시 사라질 수 있으니 설정에서 백업하세요.
- 이 버전은 개인 실험용입니다. 공개 서비스로 만들기 전 인증, 호출량 제한, 개인정보 안내 등을 추가해야 합니다.

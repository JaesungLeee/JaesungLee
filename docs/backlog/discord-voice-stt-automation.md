# 디스코드 음성 회의 STT 자동화

- 상태: backlog (가능성 검토만 완료, 착수 전)
- 작성일: 2026-09-30

## 하고 싶은 것

디스코드에서 진행되는 음성 회의 내용을 STT로 변환해 텍스트로 저장하는 과정을 자동화한다.

## 결론

가능하다. 디스코드 봇이 음성 채널에 들어가 참가자별 오디오를 받고, 이를 STT에 넘겨 텍스트 파일로 저장하는 구조로 자동화할 수 있다.

## 방법 1: 기존 봇 사용 (코딩 없음)

- **Craig**: 참가자별로 트랙을 분리해 녹음해 주는 봇. 녹음 파일을 받아 Whisper 같은 STT에 넣으면 된다. 녹음 시작과 파일 다운로드는 수동이다.
- **Scripty, DiscMeet 등**: 통화 중 실시간으로 전사해 주는 봇. 한국어 품질과 요금은 직접 확인이 필요하다.

## 방법 2: 직접 봇 제작 (완전 자동화)

1. **봇 입장**: `/record start` 같은 명령어로, 또는 특정 채널에 사람이 들어오면 자동으로 입장한다.
2. **오디오 수신**: 디스코드는 화자별로 오디오 스트림을 따로 보내 준다. 별도의 화자 분리 없이 "누가 말했는지"를 정확히 알 수 있다.
3. **STT 변환**: 발화 단위로 잘라 STT에 넘긴다. 로컬 Whisper(Apple Silicon이면 mlx-whisper나 whisper.cpp)는 무료이고, 클라우드 STT API는 유료지만 간편하다.
4. **저장**: `[시간] 화자: 내용` 형식의 마크다운으로 저장한다. 이후 LLM 요약이나 Notion 업로드까지 이어 붙일 수 있다.

## 주의할 점

- **암호화(DAVE) 지원 필수**: 2026년 3월부터 디스코드의 모든 음성 통화(스테이지 채널 제외)가 종단간 암호화되어, DAVE를 지원하지 않는 봇은 음성 채널에 참여할 수 없다. 그 이전에 작성된 튜토리얼이나 오픈소스 봇은 그대로는 동작하지 않을 수 있다.
- **라이브러리 선택**: Node.js의 `@discordjs/voice`는 DAVE와 오디오 수신을 모두 지원한다. `@snazzah/davey`는 dev-dependency로만 잡혀 있어 명시적으로 설치해야 한다.
- **수신 기능은 비공식**: 디스코드가 오디오 수신을 공식 문서화하지 않아, 디스코드 업데이트로 깨질 가능성이 있다.
- **봇 상시 실행**: 회의 시간에 봇 프로세스가 켜져 있어야 한다(내 PC 또는 서버).
- **참가자 동의**: 녹음과 전사 사실을 참가자에게 알리고 동의를 받아야 한다.

## 추천 방향

- 회의록을 꾸준히 남길 목적이라면 방법 2를 `discord.js` + `@discordjs/voice` + Whisper 조합으로 만든다.
- 가끔만 필요하다면 Craig로 녹음한 뒤 Whisper로 돌리는 편이 가장 빠르다.

## 착수 전에 확인할 것

- Python 쪽(py-cord, discord.py 확장)의 DAVE 환경 오디오 수신 지원 여부. 이번 검토에서는 확인하지 못했다.
- Scripty, DiscMeet의 한국어 전사 품질과 요금.
- 로컬 Whisper와 클라우드 STT 중 무엇을 쓸지(한국어 정확도, 비용, 실시간 필요 여부).
- 봇을 어디서 돌릴지(내 Mac 또는 서버).
- 전사 결과의 저장 위치와 후처리(요약, Notion 업로드) 범위.

## 참고 자료

- [Discord 블로그: 모든 음성·영상 통화 종단간 암호화](https://discord.com/blog/every-voice-and-video-call-on-discord-is-now-end-to-end-encrypted)
- [BleepingComputer: Discord E2EE 적용](https://bleepingcomputer.com/news/security/discord-rolls-out-end-to-end-encryption-on-voice-video-calls)
- [@discordjs/voice 문서](https://discord.js.org/docs/packages/voice/stable)
- [@discordjs/voice 0.19.2 README](https://cdn.jsdelivr.net/npm/@discordjs/voice@0.19.2/README.md)
- [Discord 개발자 문서: Voice Connections](https://docs.discord.com/developers/topics/voice-connections)
- [Sonix: Discord 녹음 자동 전사 방법 (2026)](https://sonix.ai/resources/transcribe-discord-recordings-automatically/)

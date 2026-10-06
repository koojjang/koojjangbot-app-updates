# 쿠짱 키우기 업데이트

공개 APK, 최신 버전 정보, 진행상황 및 새 대화의 인계 진입점입니다.

## 새 대화에서 이어가기

먼저 **[WORKLOG.md — 현재 진행상황·이번 작업 계획](WORKLOG.md)**와 **[HANDOFF.md — 상세 인계문](HANDOFF.md)**을 읽습니다.

앞으로 작업자는 현재 상태와 이번 배포에 추가/개선할 내용을 WORKLOG.md에 먼저 기록하고 커밋한 뒤 구현을 시작합니다. 완료 후 구현·검증·배포 결과를 갱신합니다. 문서만 변경할 때는 APK를 새로 배포하지 않습니다.

소스 및 승인 그림 원본: 비공개 [koojjang/koojjangbot-app](https://github.com/koojjang/koojjangbot-app). 소스의 AGENTS.md에도 작업 전 기록 규칙이 고정돼 있습니다.
정확한 배포 저장소 이름은 koojjang/koojjangbot-app-updates입니다.

## 현재 배포

**0.1.31 (versionCode31)**. 최신 버전의 최종 기준은 [latest.json](latest.json)입니다.

[0.1.31 APK 다운로드](https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-31.apk)

앱 시작 또는 설정 → 업데이트 확인에서 새 버전을 확인합니다. 다운로드 후 Android 설치 화면에서 기존 앱에 덮어 설치합니다.

## 최근 완료

- 0.1.31: 식사 말풍선을 실제 그림 윤곽 가까이 머리 옆으로 배치. 말풍선 크기는 유지하며 캐릭터 크기에 따라 위치/간격 연동. 사용자 배치 개선 만족 확인.
- 0.1.30: 채택된 흰 내부·핑크 크레파스 말풍선. 음식3개 중 하나만 랜덤 표시/유지, 아이콘20% 축소. 사용자 외형 만족 확인.
- 0.1.29: 8시간 식사, 방 테스트1분, 30초 젖병 모션/0.5초 교차, 잡힘 일시정지 후 재개, 방/HUD 성장 공유.
- 이전 기능·미술 규칙·검증 이력은 HANDOFF.md 참조.

현재 다음 앱 기능은 정하지 않았습니다. 다음 요청부터 기록 후 작업합니다.

## 배포 순서

행동 검사·빌드·lint와 APK 버전/서명/소재를 확인한 뒤 APK를 먼저 게시하고 latest.json을 갱신합니다. 문서 전용 커밋은 [skip ci]를 사용하며 실제 앱 버전0.1.31을 유지합니다.

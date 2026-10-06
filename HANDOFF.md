# 쿠짱 앱 개발 인계문

기준일: 2026-10-06 (한국 시간). 이 문서는 대화 이동 시 개발을 이어가기 위한 기준이다. 이후 작업자는 기능·그림·배포가 바뀔 때 이 문서도 갱신한다. 최신 배포 버전의 최종 기준은 배포 저장소의 latest.json이며, 아래 기록은 이 날짜의 상태다.

## 작업 시작 전 기록 규칙 · 사용자 요청 2026-10-06

새 대화/작업자는 구현·미술 수정·빌드·배포에 착수하기 전에 아래 순서를 따른다. 상태 확인을 위한 읽기는 먼저 할 수 있다.
1. 공개 저장소 latest.json, 이 HANDOFF.md, WORKLOG.md를 읽고 현재 배포와 완료/미완료를 확인한다. 실제 코드가 필요할 때만 비공개 소스를 읽는다.
2. 공개 WORKLOG.md의 현재 진행상황과 이번 작업 항목을 먼저 갱신해 커밋한다. 현재 버전, 사용자 요청, 이번 배포에서 추가/개선할 사항, 유지할 동작, 검증 계획, 상태(예정/진행 중)를 명시한다. 아직 하지 않은 일을 완료로 기록하지 않는다.
3. 해당 내용을 소스 docs/WORKLOG.md에도 반영하고 커밋한 다음 실제 구현을 시작한다. 긴 작업에서 단계가 바뀌거나 막히면 진행상황을 갱신한다.
4. 완료 후 검사·실제 APK 버전·배포 결과·실기기 확인 수준을 WORKLOG.md에 기록하고 HANDOFF.md를 갱신한다. 공개/소스 두 문서는 동기화한다. 앱 내부 자동 업데이트용 latest.json은 검증한 APK 게시 후에만 갱신한다.
5. 단순 문서 변경은 [skip ci]로 커밋하고 APK를 새로 빌드/배포하거나 버전을 올리지 않는다.
6. 대화 출력은 핵심 요약으로 제한한다. 이미 읽은 파일·이미지·대형 도구 결과를 반복 출력하지 않고, 후속 인계에 필요한 세부 정보는 GitHub 문서에 남긴다.

진입점은 공개 koojjang/koojjangbot-app-updates. HANDOFF.md=프로젝트 기준·미술/동작 규칙·배포 이력, WORKLOG.md=현재 진행상황·이번 작업/배포의 추가·개선 계획과 실행 상태. 사용자가 배포 저장소만 알려줘도 이 두 문서에서 이어갈 수 있게 유지한다.

## 1. 프로젝트 목표와 저장소

안드로이드 휴대폰 안에서 SD 캐릭터 쿠짱이 쉬고 걷고, 이후 다양한 행동을 하는 다마고치 스타일 APK를 만든다. 방 안의 캐릭터에서 시작했고, 현재 다른 앱 위에 떠 있는 HUD/오버레이까지 구현했다. 사용자는 카카오톡 자동응답봇 쿠짱봇의 제작자이지만 APK 개발은 초심자다. PC 봇은 별개 프로젝트이며 현재 앱은 Iris·카카오톡과 연결하지 않는다. LLM 채팅봇 구현이 목표가 아니다.

- 소스: https://github.com/koojjang/koojjangbot-app (비공개). 실제 개발·그림 원본·CI는 여기서 관리한다.
- 배포 및 인계 진입점: https://github.com/koojjang/koojjangbot-app-updates (공개). APK, latest.json, HANDOFF.md 보관.
- 정확한 이름은 koojjangbot-app-updates다. koojjang-app-updates가 아니다.
- 사용자가 새 대화에 배포 저장소만 알려줘도 이 문서를 읽고 소스 저장소로 이동할 수 있게 한다. 배포 저장소만으로 코드를 수정할 수는 없다.
- PC 자동응답봇 저장소 koojjangbot-pc를 이 앱의 수정 대상으로 착각하지 않는다.

장기적으로 옷·액세서리 교체, 여러 행동, 친밀도, PC 봇의 정보 기능 연결, 관리센터에서 소재 교체 등이 가능하도록 확장 여지는 남기되, 어떤 기능도 확정된 계획은 아니다. 사용자와 다음 작업을 정하고 진행한다.

## 2. 현재 배포와 검증 수준

현재 공개 배포: 0.1.35 / versionCode 35. 최신 수면 말풍선 위치 수정 결과는 문서 마지막 절 참조.

최신 햄버거 모션 배포 정보는 마지막 배포 결과 절 참조. 식사 GUI 정보는19절 참조. 이어지는 0.1.28 항목은 직전 배포 기록이다.

- 소스 기능·소재 커밋: 1c4438df62bfdd127f0af79265194f9f80d57dbf.
- CI 실행: https://github.com/koojjang/koojjangbot-app/actions/runs/37409884558 (run_number 28, 성공).
- APK: https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-28.apk
- APK SHA-256: 9e906e2067b587b30ae2ccb0a1e9b3d1cef250d88804e31b11b66674d615eb01.
- 업데이트 정보: https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/latest.json
- 행동 검사, APK 빌드, Android lint 통과. 산출물 ZIP digest 확인, APK 안의 모든 캐릭터 WebP와 로컬 채택 소재가 바이트 단위로 같은지 확인했다.
- 0.1.20의 새 앉기 그림은 사용자 승인 후 배포했다. 사용자가 0.1.20 앉기 전환이 실제 폰에서도 자연스럽다고 확인했다. 빌드 성공을 실기기 성공으로 표현하지 않는다.
- 사용자는 기존 걷기 2프레임, 크기 조절, 업데이트, 잠금 해제 복귀, 부드러운 HUD 이동 및 눈 깜빡임이 잘 된다고 확인했다.

중요 변경 이력:
- 0.1.14: 크기 조절 50~150%, 저장.
- 0.1.15: 다른 앱 위에 표시, 드래그, 서비스 알림.
- 0.1.16: 화면 껐다 켠 뒤 HUD 복구, 화면 프레임에 맞춘 이동 갱신으로 부드러움 개선.
- 0.1.18: 스탠딩 깜빡임, 방/HUD 공통 기본 크기 120dp, 앱 표기 쿠짱.
- 0.1.19: 더블탭 앉기 고정·해제, 고정 중 드래그, 1~10분/무제한 제한.
- 0.1.20: 고정1/고정2 소재를 승인한 수정6으로 교체, 공통 배율·바닥 정렬.

문서 커밋도 현재 main push 워크플로를 실행할 수 있다. 최신 Actions 번호가 반드시 공개 배포 번호는 아니다. 문서만 변경했다고 새 APK를 배포하거나 latest.json의 버전을 올리지 않는다.

## 3. 캐릭터 명칭과 최우선 미술 기준

현재 이름은 쿠짱이다. 중간에 뀨짱으로 바꿨지만 다시 쿠짱으로 확정했다. 화면상 명칭은 쿠짱, 내부 폴더 kkyujjang 등 기존 식별자는 업데이트 호환을 위해 유지할 수 있다.

사용자에게는 보이는 모습과 움직임이 프로젝트 지속 여부를 결정할 만큼 중요하다. 구현 편의보다 그림의 일체감이 중요하다. 후보1의 서있는 그림이 색감·그림체 기준이다. 너무 디테일한 후보0, 더 짧은 후보2는 기준이 아니다.

- 고양이 같은 나긋하고 약간 도도한 눈매, 작은 닫힌 미소, 따뜻한 밝은 갈색 단발, 연하고 차분한 핑크 눈과 파자마.
- 핑크 고양이 귀 후드, 흰 물결 테두리, 폼폼, 채도가 낮은 핑크 리본·단추, 고양이 무늬 핑크/흰 양말.
- 머리는 하나의 갈색을 바탕으로 한다. 특히 눈 옆 머리 일부를 밝은 브릿지/염색 띠처럼 칠하지 않는다. 자연스러운 같은 색 계열의 명암만 허용한다.
- 리본 채도가 강해지거나 옷·머리·피부색이 프레임별로 바뀌는 것을 싫어한다.
- 머리/몸/팔/다리를 개별 조각으로 움직이는 초기 방식은 어깨가 볼에 붙고 거북목·안짱걸음·얼굴/몸 유격 등 위화감이 컸다. 현재는 행동별 완성 일러스트를 교차 표시한다. 사용자 승인 없이 관절형 방식으로 되돌리지 않는다.
- 동작 전환으로 머리나 캐릭터 전체가 커졌다 작아지면 안 된다. 얼굴 아래 진한 검은 경계와 불필요한 목 유격도 피한다.
- 곰돌이 백팩은 기본에서 제외. 액세서리/의상 선택 기능은 장기 가능성일 뿐, 현재 완성 프레임에서 분리 교체하지 않는다.
- 외곽 흰색/검은색 오프셋 테두리는 다른 앱 위의 가독성을 위한 검토 사항이며 확정되지 않았다.
- 재생성 시 같은 색/구도가 픽셀 단위로 보존된다고 약속하지 않는다. 실제 결과를 확인하고 차이를 솔직히 말한다.
- 수정 반복으로 AI 리터치 느낌이 누적되면 스탠딩1을 외형 기준으로 새로 그리는 방안을 쓴다. 수정본은 자세 참고 역할만 명시한다.
- 앞으로 그림 생성은 반드시 한 프레임에 한 캐릭터를 한 장씩 개별 생성한다. 한 장에 두 프레임을 나란히 넣으면 개별 해상도·퀄리티가 떨어진다는 사용자 피드백으로 금지했다.
- 채택된 원본은 덮어 잃지 않게 버전 기록과 함께 보존한다. 승인 전 시안을 임의로 앱에 반영하지 않는다.

## 4. 그림 이름과 파일 대응

스탠딩·걷기·고정은 두 프레임을 사용한다. 하품·기지개는 채택한 한 장씩 우선 사용하고 두 번째 프레임 추가는 보류한다. 수정본은 _수정n 접미사를 쓴다. 단, 스탠딩/고정은 눈 뜸·감음 두 프레임으로 깜빡임을 표현하며 걷기처럼 0.5초마다 계속 교차하지 않는다.

| 사용자 명칭 | 앱 파일 | 설명 |
| --- | --- | --- |
| 스탠딩1 | idle.webp | 최초 후보1, 외형·색감의 최우선 기준 |
| 스탠딩2 | standing-2.webp | 스탠딩1 눈 감은 그림 |
| 걷기1 | walk-a.webp | 걷기 A |
| 걷기2_수정1 | walk-b.webp | 걷기 B 수정본 |
| 고정1_수정6 | fixed-1.webp | 현재 채택된 앉기, 눈 뜸 |
| 고정2_수정6 | fixed-2.webp | 현재 채택된 앉기, 눈 감음 |
| 하품1 | yawn-1.webp | 채택된 한 장, 2초 표시 |
| 기지개1 | stretch-1.webp | 채택된 한 장, 2.5초 표시 |
| 메뉴1 | menu-1.webp | HUD 메뉴 방향을 바라봄, 왼쪽 메뉴는 좌우 반전 |
| 잡힌 모습1 | held-1.webp | 드래그 중 한 프레임 |

소스 저장소의 소재 경로: app/src/main/assets/characters/kkyujjang/.
- character.json: 그림 파일·크기·앵커·걷기 간격/배율.
- 원래 스탠딩1: art/kkyujjang/palette-v1/candidate-1-source.png. 이 원본을 실제 열어 보고 미술 작업한다.
- 팔레트: art/kkyujjang/palette-v1/README.md, palette.json, swatches.svg/png. 여러 역할별 색을 추출해 저장했다. 팔레트 지시만으로 AI 재생성 색이 완전히 일치하지는 않는다.
- 스탠딩2 원본: art/kkyujjang/standing-2/standing-2-source.png.
- 현재 고정 원본: art/kkyujjang/fixed/fixed-1-source.png, fixed-2-source.png.
- 승인된 수정6 시트 원본: art/kkyujjang/fixed/fixed-revision-6-pair-source.png.
- 수정6 제작/변환 규칙: art/kkyujjang/fixed/README.md.

현재 그림은 APK 안에 들어 있다. 런타임 원격 다운로드로 교체하는 구조는 아직 아니다. 원본 PNG를 보존하고 앱 표시용 WebP로 변환해 빌드한다. 소재 관리센터나 핫교체는 미구현이다.

### 고정 자세에서 지켜야 할 해부/포즈 조건

약 45도 사선으로 앉고 시선은 사용자 쪽. 손은 바닥에 공손히 놓는다. 가까운 무릎은 보이고 작은 먼 오른쪽 무릎도 손 옆에 보여 다리가 없는 느낌을 막는다. 먼 오른발과 발목은 몸통/접힌 다리에 가려 완전히 보이지 않아야 한다. 보이는 양말 발은 하나. 발을 지우기만 하면 엉덩이가 떠 있는 자세가 되었기 때문에, 골반/엉덩이도 낮게 바닥에 내려앉게 조정했다. 무릎을 추가하려고 골반 폭을 키우지 않는다.

사용자는 수정6의 색이 스탠딩1과 조금 다른 점을 알지만 일단 채택했다. 색감 등 전반적인 미술 보정은 나중에 모아서 손볼 수 있으며, 지금 자동으로 재수정하지 않는다.

### 크기·바닥 정렬

- 스탠딩/걷기 소재: 320×512, anchorX=0.58, anchorY=0.985.
- 걷기는 원래 스탠딩보다 커 보였으므로 walkScale=0.98 적용. 지면 기준을 유지한다.
- 고정 소재: 384×512. 앵커 x=185.6px (정규화 0.48333333333333334), y=504.32px (0.985).
- 고정 프레임은 앉은 총 높이를 서있는 총 높이로 늘리지 않는다. 후드/머리 크기를 맞추고 바닥 접촉선을 정렬한다.
- 수정6 시트 1774×887에서 왼쪽 (100,0)-(890,887), 오른쪽 (904,0)-(1694,887)을 추출. 공통 scale=289/680, x=0 배치, 원본 바닥 y=883을 출력 y=503에 맞췄다. 색 재채색 없이 lossless WebP.
- 렌더러의 공통 표시 배율은 displayWidth/320을 사용한다. 고정 bitmap 폭384를 기준으로 다시 배율 계산하지 않는다.
- 사용자 선호: 방과 HUD 크기를 맞출 때 HUD의 상대적으로 작은 크기를 기준으로 한다. 기존에 66%에서 업데이트 후 크기가 달라 보인 문제를 공통120dp 기준으로 보정했다.

## 5. 현재 행동 규칙

### 이동과 휴식

자동으로 서있기/걷기를 반복한다. 걷기1↔걷기2 간격0.5초 (전체 주기1초). 이동 방향에 따라 좌우 반전. 추가 관절 회전·과장된 상하 출렁임을 넣지 않는다. 걷는 시선은 걷는 방향 쪽이어야 하고 양쪽 무릎이 서로 향하는 안짱걸음을 피한다. 현재 2프레임 표현은 사용자가 자연스럽다고 평가했다.

### 깜빡임

3~7초 랜덤 대기, 단일70%/두 번30%. 한 번 감기100ms. 두 번은 감기100ms→뜨기120ms→감기100ms (약320ms). 걷는 동안 예정된 이벤트는 다음 스탠딩까지 기다린다. 스탠딩과 고정 모두 동일 규칙. 깜빡임과 이동의 난수원을 분리해 기존 움직임 흐름을 불필요하게 바꾸지 않는다.

### 더블탭 고정

빠르게 두 번 누르면 그 자리에 고정1/고정2로 앉아 이동 정지. 다시 더블탭하면 해제되어 자동 행동 복귀. 앉은 채 드래그 가능. 방과 HUD 모두 동작.

최대 고정 시간은 설정에서1~10분/무제한, 기본5분. 내부0=무제한. SystemClock.elapsedRealtime 기반으로 화면을 꺼둔 시간도 포함한다. 드래그는 시작 시각이나 만료 시각을 초기화하지 않는다. 고정 중 제한을 바꾸면 최초 시작 시각을 기준으로 새 제한을 적용하며 이미 지났다면 해제한다. 앱/서비스 재생성 후 고정 상태 자체의 복원은 구현했다고 가정하지 않는다.

단일 탭 인사·하트 등 과거 리액션은 비활성화. 더블탭과 드래그가 있는 현재 동작을 모든 터치가 꺼져 있다고 설명하지 않는다.

## 6. 방·HUD·설정

- Native Android Canvas 앱. 외부 게임 엔진 없이 Java로 구현.
- 방과 HUD는 같은 엔진/렌더러/소재를 사용하지만 각각의 실행 상태는 별개이며 자동 위치·행동을 실시간 동기화하지 않는다.
- 크기 조절50~150%, 기본100%, 공통120dp 기본 폭. 저장된 비율은 업데이트 후 유지한다. 작은 공간에서는 잘리지 않도록 크기 제한이 적용될 수 있다.
- SharedPreferences 파일 MainActivity, key petSizePercent / fixedMinutes. 파일 이름·키를 함부로 바꾸면 설정이 초기화된다.
- HUD 위치 overlayX / overlayY 저장.
- 폰 화면에 띄우기 버튼으로 다른 앱 위에 표시 권한을 받고 실행. 앱/알림의 끄기로 종료.
- TYPE_APPLICATION_OVERLAY, 작은 투명 창, foreground service specialUse. 전체 화면을 덮는 터치 창이 아니다. 캐릭터 주변 사각형 안에서 터치를 받는다.
- Choreographer로 위치 이동을 화면 프레임에 맞춘다. 좌표/크기 변화 없을 때 layout 재요청, 그림 토큰·방향 변화 없을 때 불필요한 redraw를 줄였다.
- 화면 꺼짐/잠금 중 창과 애니메이션 숨김, 잠금 해제 후 복구. 화면 이벤트+750ms 상태 재확인으로 보완. 사용자가 실제 정상 복구 확인.
- wakelock 없음. 재부팅/강제 종료 후 자동 시작은 없다. 화면 잠금 시 숨겨져도 서비스 실행 표시는 남을 수 있다.
- 장치별 절전·권한 차이는 실제 테스트가 필요하다. 미리 별도의 대규모 대응을 임의로 추가하지 않는다.

## 7. 구현 파일 안내

app/src/main/java/com/koojjang/app/ 아래:
- PetEngine.java: IDLE/WALK/FIXED, 이동·좌표·프레임·고정 만료.
- BlinkEngine.java: 깜빡임 전용 시계/난수.
- PetRenderer.java: JSON/bitmap 로드, 프레임 선택, 공통 배율·기준점.
- PetSize.java: 방/HUD 공통 크기 계산.
- RoomView.java: 방 Canvas와 이동 범위, 더블탭·드래그, 화면 갱신.
- OverlayService.java: 권한이 필요한 foreground service, 작은 오버레이 창, 프레임 이동, 화면 복구, 드래그·더블탭, 설정 공유.
- MainActivity.java: 방 화면, 설정/크기/고정 시간/업데이트 UI, HUD 켜기·끄기.
- UpdateChecker.java / UpdateInfo.java: 최신 버전 읽기·검증·안내.

검증 도구: tools/EngineCheck.java, BlinkCheck.java, FixedCheck.java, UpdateCheck.java. 소재 확인용 tools/preview.html. 배포 준비 tools/prepare_update.py. CI .github/workflows/android.yml에서 행동 검사 후 assembleDebug/lintDebug, APK 업로드.

## 8. 업데이트·빌드·유지보수

Java17, Gradle8.11.1, AGP8.9.2, compile/target SDK35, minSDK26. package/applicationId com.koojjang.app. 기존 signing/development.jks로 동일 서명 유지. 공개 테스트용 개발키이며 정식 배포 보안키로 간주하지 않는다. 서명이나 패키지가 바뀌면 기존 앱에 덮어 설치되지 않는다. 서명키 재생성·앱 삭제·설정 초기화를 무심코 안내하지 않는다.

CI versionCode=GITHUB_RUN_NUMBER, versionName=0.1.N. 다음 번호를 현재 공개 버전+1로 가정하지 말고 실제 산출물 기준으로 확인한다.

업데이트는 앱 시작 시 또는 설정 버튼에서 공개 latest.json 확인. 사용자가 다운로드를 선택하면 브라우저에서 APK를 받고 Android 설치 화면에서 직접 확인한다. 무인 자동 설치·앱 내부 APK 자동 다운로드는 없다. 사용자는 완전 자동 설치를 원했으나 현재 방식도 충분히 편하다고 수용했다.

latest.json은 versionCode 숫자 비교, HTTPS·지정 배포 저장소 APK 경로 검증, 최대32KiB. sha256은 유지보수 배포 확인용이며 현재 앱이 APK를 직접 해시 검증하는 구조는 아니다. 자동 확인 실패가 실행을 막으면 안 된다. GitHub 토큰·로그인 정보를 APK에 넣지 않는다.

배포 순서:
1. 소스 변경을 검토하고 관련 검사·CI 빌드를 통과시킨다. 단순 문서 수정에는 별도의 동작 테스트를 추가하지 않는다.
2. 성공한 실행의 APK 아티팩트를 다운로드하고 versionCode/versionName·서명 호환·소재 포함 여부를 확인한다.
3. tools/prepare_update.py에 실제 버전과 변경 설명을 전달해 APK와 latest.json 준비.
4. 공개 apks/kkyujjang-N.apk를 먼저 게시하고 그 뒤 latest.json 갱신. 이전 APK 유지.
5. 게시된 manifest/APK를 확인하고 README 및 인계문 갱신. 가능하면 비로그인 URL/해시도 검증하며 환경 차단이면 미확인 범위를 적는다.
6. 사용자에게 앱의 업데이트 확인을 누르면 된다고 설명하고 실제 폰 피드백을 받는다.

이전 작업 환경에서는 shell Git 인증 대신 연결된 GitHub 도구로 blob→tree→commit→ref를 사용했다. 연결 방식은 새 대화에서 재확인한다. GitHub Actions APK download tool의 파일 참조를 받아 로컬로 내려 검증할 수 있다. 환경의 scratch 경로와 이전 생성 이미지 경로는 사라질 수 있으므로 영구 인계 기준으로 사용하지 않는다. 원본은 소스 저장소에서 가져온다.

## 9. 다음 작업과 대화 방식

현재 배포0.1.31. 사용자는 식사 아이콘/말풍선 모습과 머리 옆 배치 개선을 실제 사용 후 마음에 든다고 확인했다. 이번 요청은 진행상황 문서화 및 작업 전 기록 방식 도입이며, 새 앱 기능은 정하지 않았다. WORKLOG.md의 현재 상태를 기준으로 다음 사용자 요청을 기록한 뒤 작업한다.

사용자는 여러 차례 대화 최대길이에 도달하여 대화를 옮겼다. 짧고 사실에 근거한 진행 업데이트를 하고, 세부 작업·검증 기록은 GitHub에 보존한다. 이미 요청한 수정·빌드·배포에 불필요한 승인을 반복 요구하지 않는다. 새 그림은 사용자가 볼 수 있게 표시하고 승인된 그림만 앱에 반영한다.

## 10. 랜덤 행동 추가 · 2026-10-06

- 사용자 하품1·기지개1 채택. 각각 한 장으로 우선 적용하고 하품2/기지개2는 실기기 피드백 후 판단한다.
- 기지개는 스탠딩1의 심한 목 기울임을 따라 하지 않고 고개를 자연스럽게 세운다. 원본 참고는 항상 스탠딩1.
- 걷기·하품·기지개 각각 설정 ON/OFF, 기본 모두 ON. 스탠딩·고정은 기본 자세로 ON/OFF 대상이 아님.
- 모든 행동 사이에는 원래 기본 자세로 돌아와 쉬어야 한다. 고정 중 걷기 제외, 하품·기지개는 같은 서있는 그림을 사용 후 고정 복귀. 별도의 앉은 버전은 아직 만들지 않는다.
- OFF 변경 시 진행 중 행동은 마무리하고 다음 선택부터 제외. 전부 OFF면 기본 자세와 깜빡임만 유지.
- PetEngine의 fixedMode는 표시 자세와 독립적으로 유지. 하품 중 더블탭도 고정 해제, 고정 만료도 동작. 드래그는 고정 기한 초기화 금지.
- 기본 자세 대기: 스탠딩 3~8초, 고정 12~24초. 선택 가중치 걷기6/하품1/기지개1. 고정은 걷기 제외. 하품2초·기지개2.5초. 모두 임시 시작값이며 사용자 피드백으로 조절 가능.
- 설정 키 walkEnabled/yawnEnabled/stretchEnabled를 기존 MainActivity preferences에 추가. 방/HUD 공유.
- 채택 원본 art/kkyujjang/random-actions/, 앱 소재 yawn-1.webp/stretch-1.webp. 확장384×512 캔버스, 렌더러 공통 폭320 배율, 바닥/앵커 유지.
- RandomActionCheck 추가: 후보 제외, 기본 자세 대기, 고정 상태 보존, 전부 OFF, 진행 중 OFF, 드래그, 더블탭 및 기한 만료 검사.
- 이 변경의 실기기 확인은 새 APK 배포 후 필요.

## 11. 0.1.22 배포 수습 결과 · 2026-10-06

- APK 업로드까지만 완료되어 latest.json이 0.1.20에 남은 중단 지점을 수습했다. APK 게시 후 업데이트 정보와 이 문서를 0.1.22로 갱신했다.
- CI 37355034680의 행동 검사, 빌드·lint 및 APK 업로드 모두 성공 확인.
- 로컬 산출물과 공개 APK의 Git blob SHA 487cc5104f2916b08debd914b644ee5d1ccebbcc가 동일하다. versionCode 22, versionName 0.1.22, package com.koojjang.app 확인.
- APK 안의 캐릭터 JSON과 모든 WebP의 Git blob SHA가 소스 저장소와 일치한다. 기존 서명 인증서 포함 확인. 실제 폰 덮어설치·표시 확인은 사용자 피드백 대기.


## 12. 앱 이름·아이콘 변경 · 2026-10-06 / 0.1.23

- 사용자 실기기 확인: 0.1.22 하품·기지개 정상 작동.
- 앱 이름은 쿠짱 키우기. 홈 화면·Android 앱/권한 화면·앱 내부 제목과 안내를 변경.
- 사용자 제공 11836.png (388×388) 원본 그대로 아이콘으로 채택. 원본 art/launcher/launcher-source.png, 앱 drawable-nodpi/launcher_art.png. AI 재생성·리터치 없음.
- legacy mdpi~xxxhdpi PNG 및 adaptive icon. 108dp 레이어에 18dp inset으로 72dp 그림 배치, 배경 #F2E4EB. 기기 마스크에 따라 가장자리 일부가 잘릴 수 있음.
- package com.koojjang.app, 기존 서명 인증서 일치. 설정 저장 이름·키 유지, 기존 행동 소재 바이트 단위 동일.
- CI run 37398265711: 행동 검사, assembleDebug/lintDebug 성공. APK versionCode=23/versionName=0.1.23, 이름 리소스 및 아이콘 원본 포함 확인.
- artifact ZIP digest dd629539e00dc862eca341b08cfa7e6fcddabb6d86b1f89cb702c36419a24fe2 확인. 공개 APK blob 26f4706850f9eb9c7f3d205b8c48a8d913fbc396, 검증한 APK와 동일. APK 먼저 게시 후 latest.json 갱신.
- 0.1.23 이름·아이콘의 실기기 표시 및 실제 덮어설치 확인은 사용자 피드백 대기.


## 13. HUD 원터치 메뉴 · 2026-10-06 / 0.1.24

- 요청: 전용 일러스트는 추후 제작하고 원터치 메뉴 기능 먼저 구현. 앱 열기 하나만 제공.
- HUD의 onSingleTapConfirmed로 단일 터치 확정 후 작은 메뉴 표시. 더블탭 고정/해제 및 드래그 유지.
- 별도 작은 overlay 창 160×64dp, 아이보리·연핑크 테두리·둥근 모서리. 오른쪽 공간 부족 시 왼쪽, 화면 밖으로 나가지 않도록 제한.
- 메뉴 열린 동안 기존 기본 자세로 돌아와 메뉴 방향으로 좌우 반전하고 이동·랜덤 행동 일시 중단. 고정 만료 시각은 유지.
- 앱 열기 버튼은 기존 MainActivity를 앞으로 열고 메뉴 닫기. 메뉴 밖 터치·캐릭터 재터치·드래그·화면 잠금·크기/회전 변경·서비스 종료 시 닫기.
- 전체 화면 터치 창 없이 FLAG_NOT_TOUCH_MODAL/FLAG_WATCH_OUTSIDE_TOUCH 사용. 메뉴 밖 터치는 다른 앱에 전달. 앱 내부 방에는 앱 열기 메뉴 없음.
- OverlayService의 actionMenu 및 dismissActionMenu/toggleActionMenu에서 메뉴 관리. PetEngine.prepareMenu에서 기본 자세 및 방향 설정. 향후 메뉴 항목 추가 가능.
- CI 37399821968 행동 검사·APK 빌드·lint 성공. APK versionCode24/versionName0.1.24, com.koojjang.app, 기존 서명 일치 확인.
- ZIP digest sha256:52c1301c7b0e340965a2a45a046e40031f160a5e25aef19353b22f0920f6f9b0, 공개 APK blob 56f6e9e9f7e12ada5be7adf11e739b43e7262a32, 검증한 산출물과 일치. 기존 캐릭터·아이콘 소재 바이트 단위 동일.
- 실제 휴대폰 메뉴 표시·앱 열기·더블탭과 드래그 구분·바깥 터치 전달은 사용자 피드백 대기.


## 14. 메뉴 전용 자세·터치 조절 · 2026-10-06 / 0.1.25

- 사용자 채택 메뉴1: 스탠딩1 원본 기준으로 화면 오른쪽을 바라보는 그림. art/kkyujjang/menu/menu-1-source.png 보존, app assets menu-1.webp, 384×512/anchor .5/.985. 왼쪽 메뉴는 좌우 반전.
- 메뉴 표시 중 전용 그림을 쓰고, 닫으면 기존 고정 여부에 따라 스탠딩/앉기 복귀. 고정 만료 시각 유지. 메뉴1 눈감기 그림은 아직 없음.
- 원본 투명 alpha 유지·바닥 정렬·lossless WebP, 재채색 없음. art/kkyujjang/menu/README.md에 변환 기록.
- 방/HUD 공통 PetTapGesture: Android getDoubleTapTimeout의 80%로 단일탭 대기 및 더블탭 인정 간격 단축(보통300→240ms), 첫 DOWN 기준. 드래그·긴 누름·취소·멀티터치 메뉴 방지.
- 메뉴64→48dp 높이, 폭160dp 유지. 전용 일러스트 반영과 함께 조절하라는 사용자 요청대로 함께 배포.
- CI 37404697613: 행동 검사(메뉴 이동 중단·방향·고정 복귀/만료 포함), assembleDebug/lintDebug 성공.
- APK 0.1.25/versionCode25/com.koojjang.app, 기존 서명 일치. 메뉴1이 승인 변환 소재와 바이트 동일, 기존 행동 그림·아이콘 동일.
- artifact sha256:86a7aa3e24f837ac815fecd65f3367815abd48df9a561f932fc4c68d82b64cdf, 공개 APK blob 968ab29ac1a74eb37e86b062d7952537a4e51f10, 검증 산출물과 일치. APK 게시 후 latest.json 갱신.
- 실기기 메뉴 자세/크기·단축한 탭 반응 및 더블탭 조작 확인 대기.


## 15. 키보드 회피 시도 · 2026-10-06 / 0.1.26

- 사용자 요청: 키보드가 나오면 HUD 활동 영역을 줄이고 현재 위치·걷기 목적지의 비율(0~1) 유지. 영역 변화는 걷기 모션 대신 현재 자세 그대로 짧게 부드럽게 이동.
- API30+ WindowManager.getCurrentWindowMetrics의 전체 영역 IME visible/bottom을 표시 중150ms 간격으로 조회. 작은 캐릭터 창의 local inset을 전체 높이로 오해하지 않음. 기존 창 focus/layer 유지, 새 권한·접근성·전체화면 창 없음.
- full screenHeight와 activityHeight 분리. 내비게이션 하단 중복 차감 방지·키보드 위8dp 여백. PetSize는 full height로 계산해 그림 크기 유지.
- 활동 높이200ms smoothstep 전환. PetEngine x/y/tx/ty는 변경하지 않고 표시·드래그 범위만 조절. 키보드 닫으면 동일 비율 복귀. 드래그 중 영역 변화는 범위와 기준점 보정.
- 영역 변경 시 열린 메뉴 닫음. 고정 제한시간은 유지. 영역 변화 때문에 서기/앉기/하품/기지개를 바꾸지 않음.
- API26~29는 기존 영역 유지. 바닥에 붙은 키보드 대상으로 floating keyboard는 bottom inset이 없으면 회피하지 않음.
- HudAreaCheck: 영역 계산·비율 위치 복귀·부드러운 이동·하단 경계 검증. CI 37408364750: 행동 검사·assembleDebug/lintDebug 성공.
- APK 0.1.26/versionCode26/com.koojjang.app, 기존 서명 및 모든 캐릭터/아이콘 소재 동일. ZIP sha256:6d757a6dedb7e2a362e097f3d8e8eb40973f11a8d097f55fa0a88076a3175a0f, APK blob 4fd4e528974670109f04080eed808bc9cedbf28f 검증.
- 사용자는 0.1.26 실제 키보드 회피가 작동해 이제 앉혀 고정해 둘 필요가 없어졌다고 확인했다. 변경 시 Logcat KoojjangHud에 keyboard/imeBottom/availableHeight 기록. 입력 텍스트는 읽지 않음.


## 16. 잡힌 모습1 · 2026-10-06 / 0.1.28

- 사용자 생성 시안 그대로 채택. 스탠딩1 원본 참고, 후드 뒷덜미가 들리고 팔·다리를 축 늘어뜨린 느낌, 아주 약간 삐진 무표정. 사용자 승인 후 추가 미술 수정 없음.
- 원본 art/kkyujjang/held/held-1-source.png (1024×1536 RGBA) 보존, blob ca060ffc8c97fc41d18d377dfa722fdf27e83152. 원본 업로드의 출력 길이 제한 문제를 바로 수정해 완전한 원본 해시 확인.
- 앱 held-1.webp 384×512, scale=485/1451/x10/y5, alpha·색 유지, lossless WebP. 발끝503px, 앵커 .5/.985, 공통 배율 displayWidth/320. blob 8bbbfcd63f8942d03d07c249a2c429fbcdad7815.
- 방/HUD 공통, 움직임이 touch slop을 넘을 때만 잡힌 모습 표시. 짧은 탭/더블탭은 기존 처리. 드래그 중 자동 행동·깜빡임 중단, 놓기/취소/화면 숨김/방 pause 시 기존 고정 여부에 따라 앉기 또는 서기 복귀.
- PetEngine.heldMode는 fixedMode와 독립. beginHeld/endHeld, renderer.frameIndex -8. 고정 시각/기한 초기화 금지, 드래그 중 기한이 만료되면 놓았을 때 서기. 드래그 시작 시 메뉴 닫음, 기존 방향 유지.
- HeldCheck: 이동·행동 중단, 좌표 이동 중 자세 유지, 서기/앉기 복귀, 메뉴 종료, 원래 고정 기한 만료, 무제한·반복 정리 검증. CI 37409884558 행동 검사·assembleDebug/lintDebug 성공.
- APK 0.1.28/versionCode28/com.koojjang.app, 기존 0.1.26 서명 인증서 일치, 기존 캐릭터 및 아이콘 바이트 동일. 새 그림·설정 JSON 포함 및 해시 확인. ZIP digest sha256:290e3f0a11139fb08b22a101a16b159db69c6b8de2bf0f933b2c43732f669acc, APK blob b355fd3d024483089431fa80e2bc887cb2f2b9dd.
- run27은 원본 보존 수정 전 실행이라 배포하지 않음. 최종 main의 run28 산출물만 공개. APK 먼저 게시하고 최신 정보 갱신.
- 사용자는 0.1.25 메뉴 표시 및 0.1.26 키보드 회피를 실제 정상으로 확인했다. 잡힌 모습의 실기기 전환·놓기·취소·잠금 복귀는 이번 배포 후 확인 대기.


## 17. 식사·성장 시스템 · 2026-10-06 / 0.1.29

- 소스 기능 커밋: 03e391ebbec35bd34ad170d6021db139812f5944. CI https://github.com/koojjang/koojjangbot-app/actions/runs/37416816702 성공. 행동 검사(새 MealCheck 포함), assembleDebug, lintDebug 통과.
- 정상 식사는 8시간 간격. 지나간 요청은 계속 남고 누적 보상은 없음. 첫 성장 데이터 생성 시점부터 첫 대기 시작. 쿠짱의 방 하단 식사 테스트 모드로 1분 간격 시험 가능하며, 저장되고 HUD에도 같은 간격 적용. 정상 모드 복귀 시 마지막 급식 기준 8시간으로 돌아감.
- 방/HUD에 밥·햄버거 세트·우유 젖병 아이콘 3개를 표시. 현재 어떤 아이콘을 눌러도 식사젖병1·2만 0.5초마다 교차하며 실제 보이는 시간 기준 총 30초. 식사 중 자동 이동·랜덤 행동 중단.
- 드래그가 시작되면 잡힘으로 전환하고 식사 남은시간과 프레임 위상을 일시정지. 놓기/취소 시 남은시간부터 재개. 보이는 방/HUD가 모두 사라지면 멈추고 화면 복귀 시 재개. 한쪽이 잡힌 동안 공통 식사 시계도 멈춤. 기존 고정 시간은 독립적으로 만료.
- GrowthState/GrowthStore에서 경험치·급식 시각·남은시간·프레임 위상·테스트 모드 공유/저장. 방과 HUD 동시 실행으로 경험치를 중복 지급하지 않음. 급식 1회 경험치 +1, 경험치 2마다 레벨 +1. 방 상단과 HUD 메뉴에 성장 정보 표시.
- 식사젖병 원본/음식 원본은 art/kkyujjang/meals에 보존, 변환 규칙은 해당 README.md. 앱 milk-meal-1/2.webp는 384×512, 공통 anchor .5/.985. 사용자 승인 소재에 추가 미술 수정 없음.
- APK: https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-29.apk . 내부 package com.koojjang.app, versionCode29/versionName0.1.29 확인. 기존 0.1.28과 서명 인증서 SHA-256 동일.
- 산출물 ZIP SHA-256 55431b02316b39e3ccc0f7fa118dd2ada521ccd82382d13b4a434463d50b2fab 검증. APK SHA-256 e7d24693861c1afd6b855ebb7c7f68c3edcb2c18658e86e4b6cede6e87c2a129, 공개 APK blob defb8888c487d5abffa43e529778da222d4acd1a. APK 안 캐릭터/음식/설정 16개 파일이 기능 커밋의 Git blob과 전부 일치.
- APK 게시 후 latest.json 0.1.29로 갱신. 실기기 식사 풍선·아이콘 크기·식사/잡힘 전환과 재개는 사용자 확인 대기. 빌드 성공을 실기기 검증으로 표현하지 않음.


## 18. 랜덤 음식 한 개·크레파스 말풍선 · 2026-10-06 / 0.1.30

- 사용자 정정: 음식3개 선택 메뉴가 아니라 밥/햄버거/젖병 중 하나만 랜덤 표시. 흰 내부와 파자마 핑크 크레파스 테두리의 생성 시안 세 번째를 채택. 음식 아이콘은 기존보다 20% 축소(80%).
- 말풍선 원본 art/kkyujjang/meals/food-bubble-approved-3-source.png, 앱 food-bubble.png. blob 239c0b6f3d34e1d6e2c471179f01508f5cc96c92 동일. 기존 생성1·2는 가운데까지 투명해 미채택. 세 번째 원본은 재생성·재채색·변형 없이 사용.
- FoodArt는 한 장의 말풍선과 선택된 음식 하나만 합성. 64dp 정사각형 영역. 좌측 배치 시 말풍선만 반전하여 꼬리가 캐릭터 방향으로 향하고 음식 자체는 반전하지 않음. 말풍선 전체가 하나의 급식 버튼.
- GrowthState.requestFood가 요청당 균등랜덤(nextInt(3)) 한 번만 선택. requestedFood를 GrowthStore/MainActivity preferences에 저장하여 방/HUD, 화면 갱신, 앱 재시작에서 동일 음식 유지. 급식 성공 시 초기화하고 다음 요청에 다시 뽑음. 대기 미도달 시 표시 안 함.
- 기존 8시간/테스트1분 간격·경험치·0.5초 프레임 교차·30초 식사·잡힘 일시정지 후 재개는 유지. 방 음식 탭에서도 멀티터치는 급식 취소.
- 소스 기능 커밋 b4d4cb784d749d3c735d84683a36a603fac76162. CI https://github.com/koojjang/koojjangbot-app/actions/runs/37419376264 성공(행동 검사·assembleDebug·lintDebug). 로컬 MealCheck에서도 랜덤 후보3개, 요청 유지/재시작/다음 급식, 기존 식사 타이밍/재개 검사 통과.
- APK 0.1.30/versionCode30, com.koojjang.app. 기존 배포와 서명 인증서 동일. APK의 캐릭터/음식/설정17개 파일 모두 기능 커밋과 Git blob 동일.
- ZIP SHA-256 ec24c89331c0db20ea4520444eea41222039c46b9dedda1965f8082fd655b965 확인. APK SHA-256 f1958ac8cce307324cad8c011581dbbabad51cf798c689580e9c7993909f3da6, 공개 blob 3e9c933166ac27251a34401032f2fdf0cc1d44c8. APK 먼저 게시 후 latest.json 갱신.
- APK https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-30.apk . 실제 폰에서 말풍선 크기·배치·아이콘 크기와 탭 사용감은 사용자 피드백 대기.


## 19. 머리 옆 말풍선·캐릭터 크기 연동 배치 · 2026-10-06 / 0.1.31

- 사용자 75% 사용 사진에서 말풍선이 캐릭터와 멀고 몸통 옆에 표시됨. 아이콘/말풍선 미술과 크기는 채택 유지. 말풍선을 더 가까이 머리 옆으로 올리고 캐릭터 크기50~150% 변경에도 위치/간격을 연동하도록 요청.
- PetRenderer가 프레임 로드 시 alpha>=32인 가시 영역을 한 번 계산/캐시. draw와 visibleBounds가 같은 Pose(프레임·앵커·배율·방향)를 공유하여 투명 패딩과 실제 표시 위치를 혼동하지 않음. 걷기98% 보정과 좌우반전도 반영.
- 방/HUD 공통 FoodBubblePlacement: 가시 윤곽 옆2dp 간격, 가시 높이27% 지점에 말풍선 중앙을 맞춰 머리 옆 배치. 말풍선64dp 및 아이콘 크기는 캐릭터 설정과 독립적으로 유지. 크기를 바꾸면 실제 표시 bounds 기준 위치만 함께 변경. 매 표시 프레임 갱신.
- 오른쪽 공간 부족 시 왼쪽으로 전환(말풍선 꼬리 반전). 양쪽 불가 시 위/아래 비겹침 공간 사용. 가능한 공간이 전혀 없으면 덮어 표시하지 않음. 화면/키보드 활동 영역 밖으로 나가지 않으며 방 상단 성장패널88dp 제외.
- 그림/아이콘·랜덤 음식·식사 타이밍은 변경하지 않음. 드래그 때 기존 숨김 유지.
- 기능 커밋 865f5d93dd8955e51f8605a9d1c6c822829ab792. CI https://github.com/koojjang/koojjangbot-app/actions/runs/37420300697 행동검사·assembleDebug·lintDebug 성공. 로컬 FoodBubbleCheck도 통과(50~150% 1%단위 머리 추적/윤곽 간격/비겹침, 좌우 가장자리, 상단, 방 패널, 좁은 공간 fallback).
- APK0.1.31/versionCode31/com.koojjang.app, 기존 서명 인증서 동일. 캐릭터/음식/설정17개 소재가 저장소와 바이트 동일. ZIP SHA-256 54a38ac96888dee95d41c29d8cdf425359fbd13efa07def286ed25d3780dae1e. APK SHA-256 e1503ea3ede444769ee746e72e3ba7cab80d75f8d344574da2d638545fcc9f3f, 공개 blob a4014dfacd351bc84654f8ffe72d06c29994eb33.
- APK https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-31.apk 를 먼저 게시 후 latest.json 갱신. 사용자는 2026-10-06 14:54 KST에 배치 개선 결과를 ‘아주좋아’라고 확인. 주 사용 크기75%에서 만족한 것으로 기록한다. 모든 크기·키보드·가장자리 조합을 실기기로 전수 확인했다는 뜻은 아니다.


## 20. 진행상황·작업 전 기록 체계 · 2026-10-06

- 사용자 요청으로 WORKLOG.md를 현재 진행/이번 배포 계획의 기준 문서로 추가. 앞으로 변경 계획과 상태를 GitHub에 먼저 커밋한 뒤 구현 시작, 완료 후 검증/배포/실기기 결과 갱신.
- 소스 루트 AGENTS.md에 동일 작업 규칙 고정. 공개 HANDOFF.md/WORKLOG.md와 소스 docs 사본 동기화.
- 현재 식사 UI·머리 옆 배치는 사용자 확인 완료. 다음 기능 작업 미지정. 이번 변경은 문서 전용이며 배포0.1.31 유지.


## 21. 음식별 식사 모션 작업 · 2026-10-06

- 사용자 요청으로 햄버거/밥 전용 식사 프레임을 추가하고 음식별 연결 예정. 공개 및 소스 WORKLOG.md에 계획을 먼저 커밋함.
- 스탠딩1 원본을 실제 열어 확인한 뒤 식사버거1 시안 한 장 생성. 서서 약45도 사선, 양손으로 반쯤 포장된 온전한 햄버거를 들고 기대하는 모습. 현재 사용자 채택 대기.
- 식사버거2는 한입 베어문 뒤 기쁘게 씹는 모습으로 다음 개별 제작 예정. 밥 프레임 세부 자세는 추후 확정. 한 장에 한 프레임, 채택 후만 반영.
- 정상8시간/테스트1분·식사30초·프레임0.5초·잡힘 중 시간/프레임 일시정지 및 재개 유지. 앱 소재/코드 미변경, 배포0.1.31 유지. 다음 이어갈 지점은 버거1 사용자 피드백.

### 햄버거 식사 배포 결과 · 2026-10-06 / 0.1.32

- 상태: 햄버거 모션 구현·검증·배포 완료. 밥 전용 모션은 미제작으로 후속 작업.
- 사용자 식사버거1/2 모두 채택. 승인 PNG 원본 art/kkyujjang/meals/burger-meal-1-source.png 및 burger-meal-2-source.png 보존. 최종 원본 blob f9884583d7e8b6b22ddb3817bfd90dfc2cdb9028 / be8e8801a867ff8761dc33f06d6da862fba57e9c. 원본 업로드 출력 제한으로 잘린 첫 업로드를 수정해 완전한 해시 확인.
- 앱 burger-meal-1/2.webp 384×512. 공통scale289/905, 리사이즈327×491, x29/y16, 발끝503, anchor .5/.985. 재채색 없음, alpha 유지, lossless WebP. 2의 맛있다는 이모티콘 말풍선 포함.
- 음식1(햄버거 세트)은 버거1/2, 밥0·젖병2는 기존 젖병1/2. GrowthState.feed에서 요청음식을 mealFood로 보존하고 GrowthStore의 기존 MainActivity preferences에 저장·복원. 기존 진행 중 식사는 기본 젖병으로 호환. 방/HUD 공통 상태를 PetEngine/렌더러에 전달, 음식별 그림 토큰 구분.
- 정상8시간/테스트1분·30초·500ms·잡힘/숨김 일시정지 및 재개·경험치·랜덤 요청·기존 말풍선 유지.
- 기능 커밋 c3263cee208226b6c0ed2e2d1568c2f3bed4bbc7. 원본 보존 보완 커밋28b15a20c220afec9538f2a4868adb65c8f349e9(문서/원본만, 앱 코드·소재 동일).
- CI https://github.com/koojjang/koojjangbot-app/actions/runs/37423491849 (run32) 행동 검사·assembleDebug·lintDebug 성공. MealCheck에 음식별 급식·보존/복원·방/HUD·잡힘 위상 재개·이전 저장값 호환 검증 추가. 로컬 Java 미설치로 로컬 검사 실행 불가, CI에서 전체 검사 통과.
- ZIP SHA-256 2cc7e4c61ce04f92e28ffb2bea8ed685c47dcdb0cadc5d821314fbe6b18eb050 검증. 실제 APK package com.koojjang.app/versionCode32/versionName0.1.32. 기존31과 서명 인증서 동일, 이전 그림/아이콘 전부 바이트 동일 및 새 버거/JSON 소스와 동일 확인.
- APK SHA-256 fd0d347ed3897d900a76ac023c3c0d31915c964d1528a71a2db33a3cbb539366, 공개 blob d2f4d2f9196f13909d4eb693f333575112f9fc35 검증. APK 먼저 게시 후 latest.json 갱신.
- APK https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-32.apk . 실기기 햄버거 표시/크기/전환·잡힘 재개는 사용자 확인 대기.
- 다음 이어갈 지점: 밥1/2 자세를 사용자와 확정해 스탠딩1 기준 한 장씩 생성/채택 후 추가. 햄버거는 추가 채택 질문 없이 완료.

### 밥 모션·HUD 단일 표시 배포 결과 · 2026-10-06 / 0.1.33

- 상태: 구현·검증·배포 완료. 식사밥1/2 모두 사용자 채택. 밥0=밥1/2, 햄버거1=버거1/2, 젖병2=젖병1/2. 음식별 렌더러/그림 토큰 분리, 기존 공유 시계·음식 저장 유지.
- 밥 원본 art/kkyujjang/meals/rice-meal-1-source.png 및 rice-meal-2-source.png 각각1199×1312 RGBA 보존. 원본 blob05e0a34431b33c2d8d42955f71b9b7b9cf485f59 / bc9b6462f85daa8f63ebb6c34757026d2e1d050b. 공통scale289/927,374×409,x6/y106로384×512 lossless WebP,alpha/색 유지,anchor .5/.985. 발끝503/502px, 앉은 높이는 자연스럽게 유지. 2에 음표 말풍선 포함.
- RoomView는 실제 OverlayService.active를 프레임/터치/복귀 때 확인. HUD 활성 시 방 캐릭터·그림자·급식 말풍선 숨김, 터치 취소, 방의 visible/held 등록 해제·행동 멈춤. HUD 해제 시 방 표시 복귀. 배경·성장 패널·설정 유지. 서비스 실패/권한 해제/알림 끄기에서도 실제 active=false로 복귀. 방과 HUD의 위치·앉기 상태를 이관하는 변경은 아님.
- 식사30초/500ms, 잡힘/숨김 일시정지 및 재개,8시간/테스트1분·경험치·랜덤 요청 유지. 숨겨진 방은 식사 시간을 별도로 진행하거나 HUD 잡힘을 방해하지 않음.
- 기능 커밋1a1757c0d68734c6cd130453599956fcc9db7630. CI https://github.com/koojjang/koojjangbot-app/actions/runs/37427124533 (run33) 행동 검사·assembleDebug·lintDebug 모두 성공. 음식/시계 기존MealCheck 회귀 통과. RoomView HUD 분기의그림/터치/visible·held 정리와resume/pause 코드를 검토. Android UI 실기기 전환 테스트는 사용자 확인 대기.
- 산출물 ZIP SHA-256 b95f836ff590e8699c56e74154625f81cb1de50ad96c6735dedec6d4991034d3 검증. 실제 APK com.koojjang.app/versionCode33/versionName0.1.33,32와 서명 동일. 기존 소재 모두 바이트 동일, 새 밥 그림/JSON 소스와 동일 검증.
- APK SHA-256 733c334965293b26693fb959e598df9e8d66581b05180c885a65367f5bc3560b, 공개blob0a01a207ad830115a056977ab89ebd1a0750fba0 일치. APK 게시 후latest.json 갱신.
- APK https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-33.apk . 실기기 밥 크기/전환·HUD 켜기/끄기·재진입·알림 종료 확인 대기. 사용자 햄버거0.1.32 결과 만족 확인.
- 다음 작업: 사용자 실기기 피드백. 승인 없이 새 미술/기능 추가 없음.


## 자동 수면·시간 슬라이더 배포 결과 · 2026-10-06 / 0.1.34

- 상태: 사용자 수면1·zzZ 말풍선 채택 후 구현·검증·배포 완료. 실제 APK com.koojjang.app/versionCode34/versionName0.1.34. 기능 커밋 a6364e6e03ddfd7a35b3aa888838c90aa6bc298f.
- 마지막 캐릭터 터치·드래그·성공 급식 이후 기본10분 수면. 자동 이동/깜빡임/하품/기지개는 초기화하지 않음. 기존 성장 수치/급식 규칙을 바꾸지 않고 수면 자체의 육성 수치 없음.
- 수면은 fixedMode/heldMode와 독립. 스탠딩/앉기에서 현재 자리의 바닥 기준 옆잠, 자동 이동/랜덤 행동/기존 깜빡임 중지. 터치 DOWN에서 깨우며 깨우기 제스처 및 직후 더블탭 간격은 메뉴/더블탭에서 소비. 드래그 slop 도달 시 기존 잡힘. 깨우기/놓기 때 고정 기한 검사, 원래 기한 유지·무제한 유지·만료 시 서기. 수면 때문에 고정 시각 연장/초기화 없음.
- 식사/잡힘은 수면보다 우선. 음식 요청은 수면 중 계속 표시, 누르면 해당 음식으로 급식하며 시각 초기화/깨우기. 음식 요청이 있으면 zzZ 장식만 숨겨 충돌 방지. 기존30초/500ms/잡힘·숨김 일시정지/재개 및 HUD 활성 시 방 숨김 유지.
- 설정 sleepEnabled 기본true/sleepMinutes 기본10,1~20분 SeekBar·즉시 저장. fixedMinutes도1~20분 SeekBar와 별도 무제한 스위치(0), 기존5분 등 저장값 호환. 같은 MainActivity preferences 사용.
- 시간 정책: GrowthStore 공통 SleepState와 lastPetInteraction 저장. 실행 중에는 elapsedRealtime으로 잠금 포함 경과를 계산, 재시작은 저장한 벽시계 시각에서 경과 복원. 최초/기존 데이터에 시각 없으면 첫 초기화부터 대기, 시계 역행 음수 경과0 보정. 잠금 해제·재시작·방/HUD 전환 자체는 상호작용으로 처리하지 않음. 숨김 중 그림은 멈추고 복귀 시 수면 여부 계산, 진행 식사 우선. 기존 방/HUD의 위치·고정 상태 독립 및 재시작 시 기존 복원 범위 유지, 수면 때문에 추가로 고정 상태를 영구 저장하지 않음.
- 승인 PNG art/kkyujjang/sleep/sleep-1-source.png (1536×1024) 및 sleep-bubble-source.png (1536×1024) 바이트 그대로 보존. 원본 Git blob15c9eef785703bf2e8632ebd31b5a364607ea499 /51b941a8e566328733b1a14a64238b59be655c47 확인. 수면2 보류.
- 수면1 변환: 후드 머리 폭 기준289/990,448×299로 리사이즈,512×384 canvas x32/y92, 가시 바닥378px, anchor .5/.984375, lossless WebP·색/alpha 유지. 서기 높이로 확대 안 함. 원본 방향 유지. 4초 주기0~0.4% 세로 호흡만 바닥 기준, 가로 출렁임 없음.
- 별도 zzZ는 완전 투명 여백만 crop하여1105×745 lossless WebP. 가시 말풍선 폭은 약 캐릭터 표시폭23%(투명 패딩 포함34%)로 후드 귀 정도. 얼굴 쪽 꼬리로 머리 위에 겹쳐 표시. HUD에는 FLAG_NOT_TOUCHABLE 별도 장식 창, 음식/메뉴/잡힘/잠금 시 숨김. 수면 HUD 창만 넓혀 눕기 잘림 방지, 기본 중심/바닥 기준 유지하고 가장자리에서만 안전 범위 보정.
- CI https://github.com/koojjang/koojjangbot-app/actions/runs/37461812083 run34: 행동 검사(기존9개+SleepCheck), assembleDebug,lintDebug 모두 성공. SleepCheck에서10분 경계/ON-OFF/1·20분/상호작용 초기화/잠금·재시작 경과/시계 역행/수면 중 이동 중단/고정 만료·무제한/잡힘/식사 우선/20분 고정 확인. 로컬 javac 미설치로 로컬 검사 실행 불가; CI 검사 성공으로 기록.
- Android 메뉴·더블탭 깨우기 소비/음식 터치/방 숨김·HUD 전환·잠금 복귀·설정 반영은 해당 코드 흐름 검토. 합성 PNG에서 얼굴 방향·머리 크기·말풍선 겹침 육안 확인. 실기기 UI 검증으로 표현하지 않음.
- 산출물 ZIP SHA-25678e9253ef9c95be82492556b51c587f8360ef61cd6028dcf27c41adaa49a369a 일치. APK v2 서명 및 콘텐츠 digest 암호학적으로 검증,33과 인증서 SHA-256 b1b7fe19f0a737c57a9e23ab76f8e4e9fa75e71e4c5bcbc405af05d82db8f21a 동일. 기존 그림/음식 소재 전부33과 바이트 동일, 새 수면/말풍선/character.json 소스와 바이트 동일.
- APK SHA-256 d3431023931c60945171b79864307f54ae6f622668e24dbe48dad54c97b0f7ff, 공개 Git blob101f3bd342defaa5bea87f63f95dcc478fd9a2fd 일치. APK 먼저 게시 후 latest.json34 갱신.
- APK https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-34.apk . 사용자 실기기 확인 대기: 수면1·zzZ 위치/크기/호흡, 깨우기 첫 터치·연속 탭·드래그, 고정 만료/무제한, 식사 요청/급식, 설정1~20분/OFF, 잠금 복귀/재시작/방-HUD 전환. 1분 대기로 빠른 시험 가능. 수면2 추가는 실제 결과 후 판단.

- 공개 다운로드 최종 확인: latest.json 및 kkyujjang-34.apk HTTP200, manifest34 및 다운로드 APK SHA-256 d3431023931c60945171b79864307f54ae6f622668e24dbe48dad54c97b0f7ff 일치.


## 수면 말풍선 위치 수정 배포 결과 · 2026-10-06 / 0.1.35
- 사용자0.1.34 실기기 피드백: 수면은 좋음. zzZ가 후드 위에 겹쳐 있어 원하는 '후드 바깥에 약간 여백을 두고 떠 있는' 배치와 다름. 위치만 수정하여0.1.35 배포 완료.
- 방/HUD 공통 PetRenderer.sleepBubbleBounds 수정. 수면 canvas512×384의 후드 오른쪽 x327/y267 및 말풍선 불투명 윤곽 위치를 기준으로 native8px 오른쪽 간격,24px 위로 올려 머리/등 모두 비겹침. 간격/위치만 캐릭터 배율 연동, 말풍선 크기·꼬리 방향·문자 유지.
- 수면1·말풍선·기존 그림·character.json 모두0.1.34와 바이트 동일. 승인 원본 재생성/재채색 없음. 수면/호흡/급식/고정/설정/잠금/방-HUD 규칙 유지.
- 합성 preview에서 후드 오른쪽 공중 배치 및 꼬리 방향 확인. alpha>=32의 실제 캐릭터/말풍선 픽셀 겹침0 확인. 실기기 새 위치 확인은 사용자 대기.
- 기능 커밋823313bdc64a84b95a08a42d6c74eed5787b36f7. CI https://github.com/koojjang/koojjangbot-app/actions/runs/37463660436 run35: 기존 행동 검사/SleepCheck·assembleDebug·lintDebug 모두 성공.
- ZIP SHA-256 fca9ec9aa33170267532515a56880d3e08c511d76575df36381aaf8482e90200 확인. APK 내부 com.koojjang.app/versionCode35/versionName0.1.35. v2 서명/콘텐츠 digest 검증,34와 인증서 동일. APK SHA-256 a5fb13616e1bfb0c262f201f816e436aa2f6e096689e044c75a2c8882352fba9, 공개 blob b43aefc2b8ce5342bb558464bd7b91f921488461 일치. APK 게시 후 latest.json35 갱신.
- APK https://raw.githubusercontent.com/koojjang/koojjangbot-app-updates/main/apks/kkyujjang-35.apk . 빌드/합성 검증과 실기기 확인을 구분. 다음 확인: 사용자 폰75% 등 실제 크기에서 후드 옆 여유·말풍선 위치, 기존 수면 사용감. 수면2 보류 유지.

<p align="center">
  <img src="https://raw.githubusercontent.com/arriveon-lab/pleos-reservation-assistant/main/ux/brand/org-avatar.png" width="96" alt="ArriveOn 로고">
</p>

<h1 align="center">ArriveOn Lab</h1>

<p align="center">
  <strong>목적지부터 예약, 도착까지 이어지는 차량용 AI 비서</strong><br>
  차량의 목적지와 동승자의 필수 조건을 바탕으로 방문 장소를 찾고,<br>
  조건 확인·예약·도착 지연에 따른 변경을 지원하는 ArriveOn을 개발합니다.
</p>

<p align="center">
  <a href="https://github.com/arriveon-lab/pleos-reservation-assistant">프로젝트</a> ·
  <a href="https://github.com/arriveon-lab/pleos-reservation-assistant#2-실행-방법">실행 방법</a> ·
  <a href="https://github.com/arriveon-lab/pleos-reservation-assistant/blob/main/apk/ArriveOn_ArriveOn_release.apk">제출용 APK</a> ·
  <a href="https://github.com/arriveon-lab/pleos-reservation-assistant/blob/main/docs/STATUS.md">검증 현황</a>
</p>

## 차량에서 필요한 예약 비서

운전 중에는 목적지 주변 식당의 주차·유아의자·접근성 등을 비교하고 전화로 확인하기 어렵습니다. ArriveOn은 **Pleos 내비게이션의 목적지, 동승자의 필수 조건, 사용자의 명시적 승인**을 연결해 이 과정을 줄이는 것을 목표로 합니다. 첫 구현 범위는 음식점 추천과 전화 예약입니다.

- **목적지 주변 후보 추천:** 동승 조건과 확인 근거를 함께 보여 주고, 확인되지 않은 정보는 미확인으로 남깁니다.
- **승인 후 AI 전화:** 사용자가 확인한 일시·인원·조건·비용 범위 안에서 문의하고, 상대의 수락을 확인한 뒤 예약을 확정합니다.
- **변경 중 기존 예약 유지:** 도착 지연이나 매장 회신으로 변경을 요청해도, 필요한 동의가 완료되기 전까지 원래 예약을 유지합니다.
- **차량 환경 연동:** Pleos NaviHelper, Gleo 음성 비서, AAOS 주행 제한을 활용합니다. 기능별 검증 범위는 아래에 구분했습니다.

## 앱 화면

<img src="https://raw.githubusercontent.com/arriveon-lab/pleos-reservation-assistant/main/docs/images/screens/pleos-overview.png" alt="Pleos Connect 에뮬레이터의 ArriveOn 시연 화면">

Pleos Connect 에뮬레이터에서 촬영했습니다. 화면의 식당·예약자·지연 상황은 시연용 가상 데이터입니다.

## 확인한 범위

2026년 11월 15일 기준입니다. 최신 결과와 남은 작업은 [검증 현황](https://github.com/arriveon-lab/pleos-reservation-assistant/blob/main/docs/STATUS.md)에서 확인할 수 있습니다.

| 구분 | 확인한 내용과 한계 |
| --- | --- |
| 목적지 연동 | Pleos 에뮬레이터에서 목적지와 남은 이동시간 수신을 확인했습니다. 실제 ETA를 예약 시각 계산에 연결하는 작업은 진행 중입니다. |
| 등록 휴대폰 전화 시험 | 본인 휴대폰을 식당 역할로 사용해 실제 발신과 예약 확정·앱 반영을 확인했습니다. 실제 매장 예약 검증은 아닙니다. 회신 변경에는 시간 인식 등 추가 검증이 남아 있습니다. |
| Gleo 음성 시험 | 별도 시험 APK에서 에뮬레이션 주행 상태와 한국어 합성 음성으로 가상 추천·선택·예약 승인을 확인했습니다. 실제 발신은 0건이며 사람 발화 반복 인식·실차·LIVE 예약은 미검증입니다. |
| 도착 지연 | 가상 ETA로 지연 안내를 시연하고, 별도 등록 번호 시험에서 변경 확인 전화와 결과 반영을 검증했습니다. 실제 교통 지연 자동 연동은 진행 중입니다. |

기본 개발 실행은 MOCK입니다. **제출용 APK는 등록 휴대폰 대상 LIVE 시험용**이므로 [실행 절차](https://github.com/arriveon-lab/pleos-reservation-assistant#2-실행-방법)를 먼저 확인해 주세요. 실제 전화·유료 API는 명시적 승인과 설정된 범위 안에서만 실행합니다.

## 팀

다섯 명이 차량·추천·전화·서버·화면을 나누어 개발합니다. 역할은 [프로젝트 README](https://github.com/arriveon-lab/pleos-reservation-assistant#팀)를 기준으로 합니다.

| 영역 | 담당 | 주요 작업 |
| --- | --- | --- |
| 차량 / Pleos | [csjws](https://github.com/csjws) | NaviHelper 목적지·ETA probe, 기기 검증 |
| 추천 / 장소 | [tiemo0708](https://github.com/tiemo0708) | 장소 어댑터, 추천 근거·확인 질문, 웹 상세정보 보강, 저장소·CI 초기 설정 |
| AI 전화 | [tiemo0708](https://github.com/tiemo0708), [zito-git](https://github.com/zito-git) | 통신 업체 검토·선정, 전화예약 에이전트, LiveKit 음성 대화, 회신 처리·시험 서버 배포 |
| 서버 / 예약 | [jjin70](https://github.com/jjin70) | 익명 인증·접근 격리, 조건 추천·전화 승인 API |
| UX / 통합 | [soyeong03](https://github.com/soyeong03) | Android 차량 화면·주야간 테마, 주행 제한, 인증 보관·기기 통합 |

## 개발 자료

[시스템 구성](https://github.com/arriveon-lab/pleos-reservation-assistant#시스템-구성) · [팀 문서](https://github.com/arriveon-lab/pleos-reservation-assistant/blob/main/docs/README.md) · [협업 규칙](https://github.com/arriveon-lab/pleos-reservation-assistant/blob/main/CONTRIBUTING.md) · [작업 이슈](https://github.com/arriveon-lab/pleos-reservation-assistant/issues)

향후에는 일정 조회 → 다른 업종 예약 → 주차·충전 → 동행자 안내 순서로 확장을 검토합니다. 사업자 API와 MCP 연결은 각 서비스의 지원·이용 권한을 확인하며 추진할 계획입니다.

현대자동차그룹 차량용 앱 개발 공모전 출품 프로젝트입니다.

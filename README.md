# EQ-Flow

**SNF engineering calculation flow visualizer — Windows desktop app**
사용후핵연료(SNF) 공학 계산의 수식과 파라미터 의존 관계를 시각화하는 Windows 데스크톱 도구입니다.

이 저장소는 배포 전용(public) 저장소이며, 서명된 설치 파일과 자동 업데이트 매니페스트(`latest.json`)만 호스팅합니다. 소스코드는 비공개 저장소에서 관리됩니다.

---

## Download / 다운로드

최신 설치 파일은 **[Releases 페이지](../../releases/latest)** 에서 다운로드할 수 있습니다.

| 파일 | 설명 |
|------|------|
| `EQ-Flow_<version>_x64-setup.exe` | NSIS 설치 파일 — 더블클릭으로 설치 |
| `EQ-Flow_<version>_x64-setup.exe.sig` | minisign 전자서명 (자동 검증용, 수동 확인 선택) |
| `latest.json` | 자동 업데이터 매니페스트 (직접 다운로드 불필요) |

---

## Screenshots / 스크린샷

> 스크린샷은 준비되는 대로 추가됩니다. / Screenshots will be added shortly.

<!--
Place the following images under `docs/screenshots/` and remove this comment wrapper:

![EQ-Flow overview](docs/screenshots/overview.png)

<sub>그래프 캔버스 — 수식 노드와 파라미터 노드가 의존 관계에 따라 계층적으로 배치됩니다.</sub>

![Peer edge](docs/screenshots/peer-edge.png)

<sub>Peer 엣지 — 같은 계산 계층에 속하는 노드를 보라색 점선으로 연결합니다.</sub>

![Auto updater](docs/screenshots/auto-update.png)

<sub>자동 업데이트 — 새 버전이 출시되면 앱 시작 시 자동으로 알림이 표시됩니다.</sub>
-->

---

## System Requirements / 시스템 요구사항

- **OS**: Windows 10 / 11 (x64)
- **WebView2**: Microsoft Edge WebView2 Runtime (설치 파일에 포함되어 자동 설치)
- **RAM**: 최소 2 GB 권장
- **Disk**: 약 100 MB

---

## Installation / 설치

1. **[Releases 페이지](../../releases/latest)** 에서 `EQ-Flow_<version>_x64-setup.exe` 다운로드
2. 설치 파일 더블클릭 → 설치 마법사 진행
3. 설치 완료 후 시작 메뉴 또는 바탕화면 아이콘으로 실행

### File Association / 파일 연결

설치 후에는 Windows 탐색기에서 `.eqflow` 프로젝트 파일을 더블클릭하면 EQ-Flow가 자동으로 실행됩니다.

---

## Auto Update / 자동 업데이트

EQ-Flow는 앱 시작 시 자동으로 최신 버전을 확인합니다.

- 새 버전이 있으면 업데이트 대화상자가 표시되어 한 번의 클릭으로 설치할 수 있습니다
- "이 버전 건너뛰기" 선택 시 해당 버전은 다음부터 자동으로 생략됩니다
- 메뉴바 우측의 업데이트 버튼(⭳)으로 언제든 수동 확인이 가능합니다
- 모든 업데이트 패키지는 minisign 전자서명으로 자동 검증되며, 서명 불일치 시 설치가 거부됩니다

---

## Documentation / 문서

- **[CHANGELOG](CHANGELOG.md)** — 전체 버전 변경 이력
- **[Releases](../../releases)** — 각 버전의 상세 릴리스 노트 및 다운로드

---

## Contact / 문의

사용 중 문의사항, 불편사항, 기능 요청이 있으시면 아래로 연락 주시기 바랍니다.

- **Maintainer**: 권용민 (ymgwon@tsne.co.kr)
- **Organization**: TSNE

---

© 2026 TSNE. All rights reserved.
Internal distribution repository — for authorized users only.
내부 사용자용 배포 저장소입니다.

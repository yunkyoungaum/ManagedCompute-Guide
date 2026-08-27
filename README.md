# Foundry Managed Compute 전환 가이드

IaaS GPU VM에서 Microsoft Foundry Managed Compute로 추론 워크로드를 전환할 때 필요한 개념, 배포 절차, 운영 지표와 비용 판단 기준을 정리한 한·영 문서입니다.

**배포 문서:** [https://yunkyoungaum.github.io/ManagedCompute-Guide/](https://yunkyoungaum.github.io/ManagedCompute-Guide/)

> [!WARNING]
> 현재 문서는 **Draft**이며 Managed Compute는 **Public Preview** 상태입니다. Part A의 벤치마크 값은 아직 실측 전이고, C2의 커스텀 모델 배포 및 H200 지원은 `Coming soon`으로 표시되어 있습니다. 고객 공유나 의사결정에 인용하기 전에 최신 Microsoft Learn 문서와 Azure 가격을 다시 확인하세요.

## 문서 구성

| 구분 | 내용 |
| --- | --- |
| Part A · Benchmark | 테스트 설계, 처리량·지연, 토큰당 비용, 워크로드별 권장 구성 템플릿 |
| Part B · What | 배포 유형, 모델·템플릿·가속기 선택, 책임 분계, VM 매핑, 쿼터 |
| Part C · How | 포털 배포, 코드 마이그레이션, 인증·권한, 모니터링, 스케일링, 전환 체크리스트 |
| Part D · Economics | 비용 공식, 시나리오 시뮬레이션, $/1M 토큰 계산, 제약과 로드맵 |

페이지 오른쪽 위의 언어 선택기로 한국어와 영어를 전환할 수 있습니다. 선택한 언어는 URL의 `lang` 쿼리와 브라우저 로컬 저장소에 유지됩니다.

## 로컬에서 확인하기

별도의 빌드나 패키지 설치가 필요 없는 정적 사이트입니다. 저장소 루트에서 간단한 HTTP 서버를 실행하세요.

```bash
python3 -m http.server 8000
```

브라우저에서 `http://localhost:8000`을 열면 됩니다. 언어와 테마는 다음 쿼리로 직접 지정할 수 있습니다.

- 영어: `?lang=en`
- 한국어: `?lang=ko`
- 다크 테마: `?scoutTheme=dark`
- 라이트 테마: `?scoutTheme=light`

## 저장소 구조

```text
.
├── index.html   # 한·영 본문, 스타일, 언어 전환 및 목차 스크립트
└── assets/      # 배포, 쿼터, 모니터링 화면 이미지
```

`main` 브랜치의 루트가 GitHub Pages로 배포됩니다. 문서와 이미지를 수정해 브랜치에 반영하면 Pages 배포에도 반영됩니다.

## 갱신 체크리스트

- 한국어와 영어 본문을 함께 수정합니다.
- Part A의 `TBD`를 실측값으로 교체하고 비용 계산 결과를 함께 검증합니다.
- 가격, 쿼터, 지원 가속기와 Public Preview 상태를 최신 공식 문서에서 확인합니다.
- 목차 링크와 본문의 `id`가 일치하는지 확인합니다.
- `assets/`의 모든 이미지가 페이지에서 정상 표시되고 대체 텍스트를 갖는지 확인합니다.
- 새 창으로 여는 외부 링크에 `rel="noopener"`가 있는지 확인합니다.

## 주요 참고 자료

- [Managed compute in Microsoft Foundry](https://learn.microsoft.com/en-us/azure/foundry/concepts/managed-compute-overview)
- [Deploy open-source models with managed compute](https://learn.microsoft.com/en-us/azure/foundry/how-to/deploy-models-managed?tabs=openai-entra&pivots=python-sdk)
- [Manage and increase quotas](https://learn.microsoft.com/en-us/azure/foundry/how-to/quota)
- [Azure Retail Prices API](https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices)

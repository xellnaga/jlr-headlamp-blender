# JLR-Style Headlamp — Blender Python (bpy)

JLR(재규어랜드로버) 차량 스타일의 헤드램프를 **코드만으로** 모델링하고 렌더링하는
프로젝트입니다. Blender GUI 없이 `bpy` 파이썬 모듈을 이용해 헤드리스 환경에서
모델 생성부터 Cycles 렌더링, .blend 저장까지 자동으로 수행합니다.

![render](renders/headlamp_v2.png)

## 구성

| 파일 | 설명 |
|------|------|
| `headlamp_v1.py` | 기본 버전 — 슬림 하우징, 듀얼 프로젝터, 수평 DRL 바 |
| `headlamp_v2.py` | 고급 버전 — 곡면 하우징, 3단 프로젝터, 픽셀 LED, 곡선 DRL |
| `headlamp_v2.blend` | v2 씬 파일 (Blender에서 바로 열어 편집 가능) |
| `renders/` | 렌더링 결과 이미지 |

## v2 주요 모델링 요소

- **곡면 하우징**: Bend + Taper 모디파이어로 펜더를 따라 감기는 형태, 3단 계단식 베젤
- **프로젝터 유닛 ×2**: 알루미늄 링 → 크롬 리플렉터 콘 → 내부 배럴 → 유리 렌즈 → 발광 링 → 방열 핀
- **픽셀 LED 매트릭스**: 6×3 그리드, 일부 점등 상태 랜덤 배치
- **DRL 라이트 가이드**: J자형 베지어 커브 + bevel, 하단 앰버 방향지시등 스트립
- **렌더링**: Cycles(CPU) + 디노이징, 4점 조명, 피사계 심도(DOF) 카메라

## 실행 방법

bpy 모듈은 Python 3.11 wheel로 배포되므로 3.11 환경이 필요합니다.

```bash
# uv 사용 시
uv venv blenv --python 3.11
uv pip install bpy --python blenv/bin/python
blenv/bin/python headlamp_v2.py
```

실행이 끝나면 `headlamp_v2.png`(렌더 이미지)와 `headlamp_v2.blend`(씬 파일)가 생성됩니다.
GPU가 없어도 동작합니다 (CPU 렌더링, 약 2~3분).

## 커스터마이징 포인트

- `scene.cycles.samples` / `resolution_x·y` — 품질과 렌더 시간 조절
- `projector(x, y, z, r, ry)` — 프로젝터 위치·크기 변경
- `m_ring`, `m_led`의 Emission Strength — 점등 밝기
- 카메라 `location` / `rotation` — 앵글 변경

## 라이선스 / 주의

실제 JLR 차량 디자인은 지적재산입니다. 이 리포지토리의 모델은 해당 스타일에서
영감을 받은 오리지널 형상이며 학습·포트폴리오 용도로 사용하세요.

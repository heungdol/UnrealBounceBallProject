# ToyProject - Bounce Ball Game

Unreal Engine 5.2 기반의 물리 기반 아케이드 게임 프로젝트입니다. 튀어다니는 공 캐릭터가 다양한 어빌리티를 사용하여 블록을 파괴하는 게임입니다.

## 주요 기능

### 캐릭터 시스템
- **커스텀 바운스 물리**: 벽/바닥 충돌 시 다른 반발력 적용
- **비대칭 중력**: 상승/하강 시 다른 중력 스케일 적용으로 아케이드 느낌 구현
- **젤리 이펙트**: 속도 기반 스쿼시/스트레치 변형 효과

### 전투 시스템 (Gameplay Ability System)
| 어빌리티 | 설명 |
|---------|------|
| **Boom Attack** | 범위 500 유닛의 광역 폭발 공격 |
| **Dash** | 0.5초간 500 유닛 거리를 이동하는 돌진 |
| **Stomp** | 빠르게 하강하며 착지 시 반발하는 내려찍기 |

### 환경 상호작용
- **파괴 가능한 블록**: 체력 시스템, 데미지/회복/리스폰 지원
- **젤리 변형 이펙트**: 블록 피격 시 시각적 피드백

### 카메라 시스템
- **동적 FOV**: 캐릭터 이동 속도에 따른 FOV 오프셋
- **Y축 보간**: 부드러운 카메라 추적
- **Z축 오프셋**: 동적 카메라 높이 조절

## 프로젝트 구조

```
Source/ToyProject/
├── Attack/          # 데미지 타입 정의
├── Camera/          # 커스텀 카메라 및 스프링암 컴포넌트
├── Character/       # 메인 캐릭터 (ToyBounceBall)
├── Component/       # 재사용 가능한 컴포넌트
│   ├── ToyStatComponent           # 체력/스탯 관리
│   ├── ToyJellyEffectComponent    # 젤리 변형 이펙트
│   └── ToyCharacterJellyEffectComponent
├── Data/            # 데이터 에셋 정의
│   ├── ToyBounceBallActionData    # 어빌리티 입력 매핑
│   └── ToyJellyEffectData         # 젤리 이펙트 커브 데이터
├── GAS/             # Gameplay Ability System
│   ├── AT/          # Ability Tasks (MoveSweep, MoveToGround)
│   └── GA/          # Gameplay Abilities (Boom, Dash, Stomp)
├── Interface/       # 인터페이스 정의
├── Movement/        # 커스텀 무브먼트 컴포넌트
├── Player/          # 플레이어 스테이트
└── Prop/            # 상호작용 오브젝트 (ToyBlock)
```

## 기술 스택

- **엔진**: Unreal Engine 5.2
- **언어**: C++
- **주요 프레임워크**: Gameplay Ability System (GAS)
- **입력 시스템**: Enhanced Input System

## 핵심 클래스

### AToyBounceBall
메인 캐릭터 클래스. `IAbilitySystemInterface`를 구현하여 GAS와 통합됩니다.

```cpp
// 주요 속성
float BallRadius = 50.f;
float BounceGroundPower = 3000.f;
float BounceWallPowerX = 1500.f;
float BounceWallPowerZ = 2000.f;
```

### UToyBounceBallMovementComponent
비대칭 중력을 구현하는 커스텀 무브먼트 컴포넌트입니다.

```cpp
// 중력 스케일
float UpwardGravityScale = 8.f;   // 상승 시 (빠르게 감속)
float DownwardGravityScale = 5.f; // 하강 시
```

### UToyStatComponent
체력 시스템을 담당하는 모듈화된 컴포넌트입니다. 네트워크 리플리케이션을 지원합니다.

### UToyJellyEffectComponent
커브 기반 애니메이션으로 스쿼시/스트레치 변형 효과를 구현합니다.

## 인터페이스

| 인터페이스 | 용도 |
|-----------|------|
| `IToyBounceBallInterface` | 캐릭터 공격 관련 |
| `IToyBlockInterface` | 블록 상호작용 (데미지, 파괴, 회복) |
| `IToyStatInterface` | 스탯 컴포넌트 접근 |

## 빌드 및 실행

1. Unreal Engine 5.2 설치
2. 프로젝트를 UE5 에디터로 열기
3. `Content/ToyProject/Level/Level_Test` 레벨 로드
4. PIE(Play In Editor)로 실행

## 최근 개발 내역

- SetComponentTickEnabled 최적화
- 공격 이펙트 시스템 추가
- 체력 컴포넌트 모듈화
- 음파 공격(Boom Attack) 구현
- 젤리 이펙트 컴포넌트 추가
- 부서지는 블록 시스템 구현

## 라이선스

이 프로젝트는 개인/학습 목적으로 제작되었습니다.

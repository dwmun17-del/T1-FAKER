# 훈련생 출결 · 상담 관리

Windows용 훈련생 관리 시험 버전입니다. 훈련생 기본정보, 날짜별 출결, 상담 기록을 한 프로그램에서 관리합니다.

![화면 예시](./화면예시.png)

## 주요 기능

- 훈련생 이름, 훈련과정, 상태(훈련 중/수료/중도 종료) 관리
- 날짜별 출석·지각·조퇴·결석·공결 및 사유 저장
- 미입력 출결 일괄 출석 처리 후 검토/저장
- 훈련생별 상담일, 상담 내용, 후속 조치 저장·검색·수정
- 현재 Windows 사용자 계정 기준 DPAPI 암호화 저장 및 백업/복원

## 실행 환경

- Windows 10/11 64비트 권장
- GitHub Actions 배포본은 .NET 8 런타임을 포함한 단일 실행 파일로 빌드됩니다.

## 데이터 저장 위치

프로그램 데이터는 다음 위치에 저장됩니다.

```text
%LOCALAPPDATA%\VocationalTrainingManager\records.dat
```

백업 파일(`*.vtbackup`)과 실제 훈련생 데이터는 Git 저장소에 커밋하지 마세요.

## GitHub에서 빌드하기

이 저장소에는 `.github/workflows/build-windows.yml`이 포함되어 있습니다.

1. `main` 브랜치에 코드를 올리면 GitHub Actions가 자동으로 Windows 실행 파일을 빌드합니다.
2. GitHub 저장소의 **Actions** 탭에서 `Build Windows app` 실행 결과를 엽니다.
3. 실행 결과의 **Artifacts**에서 `TrainingManager-Windows-x64`를 내려받습니다.
4. 버전 태그(`v0.1.0` 등)를 푸시하면 동일한 ZIP이 GitHub **Releases**에도 자동 등록됩니다.

## 로컬 개발 빌드

.NET 8 SDK가 설치된 Windows 환경에서:

```powershell
dotnet restore TrainingManager.csproj
dotnet run --project TrainingManager.csproj
```

배포용 단일 실행 파일:

```powershell
dotnet publish TrainingManager.csproj -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:IncludeNativeLibrariesForSelfExtract=true -o publish
```

## 시험 기능

소스에는 `--self-test`와 `--preview` 실행 인자가 포함되어 있습니다.

```powershell
.\TrainingManager.exe --self-test
.\TrainingManager.exe --preview
```

## 개인정보 및 운영 주의사항

이 버전은 시험용입니다. 실제 훈련생 이름, 출결, 상담 내용은 개인정보 또는 민감한 업무정보가 될 수 있으므로 기관의 개인정보 처리 기준과 내부 프로그램 사용 기준을 확인하기 전에는 실제 자료를 입력하지 않는 것을 권장합니다.

현재 백업 암호화는 Windows DPAPI의 `CurrentUser` 범위를 사용하므로, 다른 PC·다른 Windows 계정·Windows 재설치 환경에서 복원을 보장하지 않습니다.

## 현재 포함되지 않은 기능

- 별도 사용자 로그인 및 권한관리
- 수정 이력/감사 로그
- 중앙 서버 또는 기관 시스템 연동
- 다중 사용자 동시 사용
- 출결 통계 및 보고서 출력

## 버전 상태

시험용 첫 버전입니다. 실제 업무 배포 전에는 가상 데이터로 저장, 재실행, 백업, 복원 기능을 충분히 검증하세요.

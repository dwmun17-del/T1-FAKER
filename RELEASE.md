# GitHub 배포 절차

## 1. 자동 빌드 확인

`main` 브랜치에 코드가 올라가면 **Actions → Build Windows app**이 자동 실행됩니다.
성공 후 실행 상세 화면의 Artifacts에서 `TrainingManager-Windows-x64` ZIP을 받을 수 있습니다.

## 2. 정식 Release 만들기

로컬 Git이 있다면:

```bash
git tag v0.1.0
git push origin v0.1.0
```

태그가 올라가면 GitHub Actions가 `TrainingManager-Windows-x64.zip`을 Releases에 자동 등록합니다.

## 3. 배포 전 점검

- 가상 훈련생으로 등록/수정 테스트
- 날짜별 출결 저장 및 재실행 후 유지 확인
- 상담 기록 저장/검색/수정 확인
- 백업 저장 및 동일 Windows 계정에서 복원 확인
- 실제 개인정보 입력 전 기관 보안/개인정보 기준 확인

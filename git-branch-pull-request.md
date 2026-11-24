# Git 브랜치와 Pull Request

## 1. 브랜치란?
- 원본(main)에 영향을 주지 않고 **독립적으로 작업하는 작업 공간**

## 2. 기본 명령어
```bash
git branch                       # 브랜치 목록
git switch -c feature/login      # 새 브랜치 만들고 이동
git switch main                  # main으로 이동
git merge feature/login          # 현재 브랜치에 합치기
git branch -d feature/login      # 브랜치 삭제
```

## 3. 협업 흐름 (GitHub Flow)
```bash
git switch main
git pull origin main                 # 최신 코드 받기
git switch -c feature/budget-page    # 기능 브랜치 생성
# 작업 후
git add .
git commit -m "feat: 예산 관리 화면 추가"
git push origin feature/budget-page
```
1. GitHub에서 **Pull Request(PR)** 생성
2. 팀원 코드 리뷰
3. 승인 후 main에 Merge
4. 로컬 main 최신화 후 다음 작업

## 4. 브랜치 이름 규칙 예시
| 접두어 | 용도 |
|---|---|
| feature/ | 새 기능 |
| fix/ | 버그 수정 |
| docs/ | 문서 |
| refactor/ | 구조 개선 |

## 5. 충돌(Conflict)
```
<<<<<<< HEAD
내 코드
=======
다른 사람 코드
>>>>>>> main
```
- 남길 코드를 직접 고르고 표시줄을 지운 뒤 다시 add, commit

## 6. 커밋 메시지 규칙 예시
- `feat:` 기능, `fix:` 버그, `docs:` 문서, `style:` 포맷, `refactor:` 리팩터링

## 정리
- main에 직접 push하지 않고, 브랜치 → PR → 리뷰 → Merge 순서로 협업한다.

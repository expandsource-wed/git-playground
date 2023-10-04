# git-playground
git 다양한 기능 연습하기

## git amend 마지막에 사용한 커밋에 추가하기

- 소스트리 기준 
- 커밋할 때 '마지막 커밋 정정'을 클릭하고
- 커밋하게 되면, 기존 커밋이 정정되고 새로운 커밋이 추가되지 않는다.

- 원격 저장소의 마지막 커밋을 수정할 때
- 로컬 저장소에서 amend를 사용해 '마지막 커밋 정정' 후 push를 하게 되면 오류메시지 발생

- 푸쉬 사용 시 강제 푸쉬에 체크하고 푸쉬하면 깔끔하게 원격저장소의 커밋도 정정된다.

- `git commit --amend`
- 커밋 수정 후 덮어쓰기

# Cherry Pick
- 필요한 커밋만 딱 가져와서 현재 브랜치에 붙이는 기능
- 현재 브랜치에서 다른 변경사항을 제외한 (예를 들면 버그 수정 등 중요한 커밋) 필요한 커밋만 선택해서 (소스트리 기준 우클릭 - 체리 픽)

- `git cherry-pick [커밋해시]`
- 커밋이 여러개일 경우
- `git cherry-pick [커밋해시1] [커밋해시2]`

# Git reset : 옛날 커밋으로 브랜치 되돌리기
- 소스트리에서 돌아가고 싶은 커밋을 선택
- 우클릭 -> 이 커밋까지 현재 브랜치를 초기화
- Mode
    1. soft
        - 커밋을 취소하고, 변경사항은 스테이징까지
    2. mixed
        - 커밋 취소, 스테이징 취소, 변경사항 유지
    3. hard
        - 커밋 취소, 스테이징 취소, 변경사항 취소
        - 작업 내용이 완전히 사라지므로 주의
        - 원격 브랜치에도 반영할 경우 [강제 푸쉬]

# revert
- 리셋의 경우 개인이 사용할떄는 강제 푸쉬로 이력관리(없었던 일처럼 만드는 것)이 가능하다.
- 하지만 함께 쓰는 브랜치에서 되돌아간 흔적까지 남기고 싶을 때, revert
- 소스트리에서는 우클릭 -> 커밋 되돌리기
- 되돌아간 커밋이 추가로 생성되고
- 해당 커밋의 변경사항은 사라진다.

`git revert [커밋해시]``


# stash


## 원격저장소 (GitHub)에서 pull request 되돌리기(revert)
- 되돌려야하는 PR (merge가 완료된)이 있을 경우
- 깃헙저장소 > pull request > closed
- 되돌려야하는 PR 선택 후
- Revert 선택
- revert를 위한 새로운 PR이 생성됨
- 새로운 PR을 merge하고 나면 기존 PR이 되돌려진 상태로 복귀

## 브랜치 보호하기
- branch protection rule
- GitHub > 저장소 > Setting > Branches
- > Add branch protection rules
    - Branch name pattern
        - (패턴 가능 feature* => 모든 feature 브랜치)
        - 일반적으로 main 브랜치를 보호
    - Requires a pull request before merging
        - 반드시 병합하기 위해서는 PR이 필요
        - (일반적인 commit & push를 통한 병합은 원격저장소에서 block이 됨)
        - Requires approvals
            - PR 병합하기 위해서 반드시 승인이 있어야 하는 Reviewer의 수
    - 룰을 설정하게 되면 main 브랜치가 보호된다.
    
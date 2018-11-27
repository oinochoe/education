# [GIT] git & github 중급 😅
* 신승엽

## REBASE

* feature를 master에 rebase한다란
* feature의 master에 대한 base(feature와 mster의 공통조상)를 master로 변경
* base에서 경로를 찾고
* head가 master로 변경
* hash 값이 구해지는 방식 : 커밋을 이루고 있는 오브젝트들의 합
* dangling 된 오브젝트가 많아지기 때문에 주의
* fast-foward란 master에 feature를 머지하는데 굳이 머지 하지않고 c3 에서 c5로 단순히 포인터만 변경해주는 것을 말한다.
* rebase를 사용하는 이유는 커밋 그래프를 이쁘게 잘 정리하기 위함
* 결국 문제점과 히스토리를 편하게 볼 수 있다.

![[사진]feature 2 master](feature_2_image.jpg)

## 대화형 REBASE 🏋 Interactive REBASE ☸️
* 커밋을 합치고, 없애고, 순서를 바꿀 수 있다
* 커밋 메시지를 바꾸고 중간 커밋의 내용을 바꿀 수 있다.

### 커밋합치기
* 변경사항 1과 변경사항 2를 동시에 적용하여 c2/3를 생성
* c2와 c3을 하나로 합치는 효과

* 우리가 바꾸고 싶은 클릭 `하위 요소 대화식 재배치`
* 재배치 하고 나면 새로운 해시로 생성됩니다.

## 커밋 없애기
* base인 c1을 head가 가리키고 변경사항 1을 적용
    * 적용 결과가 이전과 다르지 않기 때문에 git에서는 새로운 c2` 커밋을 생성하지 않고 c2를 그대로 사용
* 바로 전에껄로 reabse 할 필요는 없다 왜냐면 리셋이 있으니까!!
* 실수로 삭제했을 시에는 `git reflog` 를 뒤져서 다시 돌아가면 된다.

## 커밋 순서 바꾸기
* 대화형 rebase 접속

![[사진]hash_change.jpg](hash_change.jpg)

## 커밋 메시지 바꾸기 🌾
* 대화형 rebase 접속

![[사진] 커밋 메시지로 해쉬값 변경](commit_message_change_2_hash_change.jpg)

## 중간 커밋의 내용 바꾸기 👨‍👨‍👦‍👦
* 변경사항 1을 적용한 후 reabse를 잠시 멈춤
* 중간에 name 을 변경 후에 `git rebase --continue` 명령을 통해 rebase를 계속 진행하여 마무리 👨
* 대화형 rebase에서 체크해서 그 곳으로 돌아가서 
* 동작 재배치 계속 (rebase continue) 클릭하여 재배치 계속하기

![[사진] 중간에 커밋 추가해서 리베이스 계속 명령어로 만들기](중간기능바꾸기.jpg)

## rebase 중 충돌해결 🎆
* 빈 conflict 파일을 추가하고 conflict 브랜치 만듦
* master에서 파일 내용을 작성
* 같은 파일 고칠 시 충돌
* 충돌이 발생
* conflict에 master를 maerge 할때의 충돌과는 정반대
* 기존에 merge 할때는 `head` 내 로컬 `master` 는 리모트
* base에서 현재 브랜치의 변경사항을 구한다
* 스테이지에만 올리고 rebase continue를 한다

#### 두번째 rebase 충돌 해결 🗡
* 두번 diff를 한다음 단계적으로 `rebase continue`하면 
* 두번의 충돌을 해결해야한다.. 
* 충돌을 피하기 위해 각각의 diff를 체리픽을 해도 된다.

* rebase로 feature들을 차례대로 merge(no-ff) 한 것과 같이 하거나( 특정 feature의 범위를 한 눈에 파악 용이)
* master를 일렬로 유지
* 히스토리 파악 쉬움
  

## 모두가 함께 사용하는 브랜치에 REBASE
* 티웜 1은 feture를 master에 rebase
* 팀원 2는 feature에 새로운 커밋을 생성



# 젠킨스 깃헙 연동 👯
* 깃헙에서 PR이 생성 되었을 때 자동으로 관리하고 싶다면
* 젠킨스 플러그인 관리 상에 `github pull request builder` 사용 하면 된다
* 깃헙 Personal Access Token으로 젠킨스 상에 세팅 해두면 편하다
* 유출 시에는 깃헙 상 토큰을 삭제하면 그만이다
* 깃헙 vscode 세팅시에 추가했던 녀석 추가하고
* 젠킨스 상에서 `Jenkins Credentials Provider`로 추가한다.
* 깃헙에 있는 소스를 관리해보자
  1. Jenkins로 갑니다
  2. PR 이라는 이름으로 Fresstyle ~~ 만듦니다
  3. 젠킨스 설치시 기본적으로 깃헙 플러그인이 추가 되어있다.
  4. 추가 되어있으면 `github project` 체크
  5. 깃 저장소 URL 삽입
  6. 공개 저장소일시 Credential 설정은 안해도 된다
  7. 고급을 눌러줍니다. 
  8. RefSpec은 +refs/pull*:refs/~~ 적어줍니다.
  9. 빌드유발 탭은 `Github pull request Builder`를 체크
  10. Admin list -> `OK 2 TEST` 권한을 가지고 있는 아이디를 적어줍니다
  11. `use github hooks for build triggerring` 체크
  12. 깃헙으로 돌아가서 `webhooks`에 체크를 확인합니다.
  13. ghprbhook(github pull request build hook)
  14. 소스 수정 후 커밋 해서 jenkins에서 자동 빌드 되는 것과 풀리퀘스트를 날렸을 때 github도 확인합니다.
  15. 젠킨스 자체 고급 기능들 확인하기
        1. Use github hooks for build triggering(플러그인 사용)
        2. Trigger phrase -> `test`라고 적으면 깃헙 풀리퀘스트 상에 댓글에 `test`가 적혀있을 때만 젠킨스 플러그인이 돈다

## 깃헙 기능
1. `GIThub-protected-branch` --> `master`를 입력하면 bracnh 보호 됨
2. Require pull request reviews before merging
3. Require approving reviews (리뷰 숫자)
4. Require review from code Owners -> 특정 언어를 이 사람에게 허락받아라 라고 지정도 할 수있다 . `code Owners`라는 파일이 필요하다 (저장소) , 깃헙 헬프에 들어가보면 확인 할 수 있다.
5. Require branches to be up to date before merging (최신 체크)
6. Status checks found in the last week for this repo
    * default 체크 : 체크를 여러개 만들 수 있다.

7. 이런 다양한 옵션으로 인해서 좀 더 제약사항들을 가지고 관리 할 수 있다.

## codeOwners 파일
* gitignore의 패턴 규칙과 동일
* 개인은 물론 팀도 지정 가능

## GitHubFlow
### 여러가지 Git workFlow들 🚚

* 메인 브랜치
    * 항상 존재하는 브랜치
    * master
        * 배포된 소스가 있는 브랜치
    * develop
        * 다음 배포를 위한 소스가 있는 브랜치
        * 개발이 완료되면 일련의 과정을 통해 master로 merge
* 서포팅 브랜치
    * master와 develop 외에 팀 멤버들이 병렬로 일 할 수 있도록 도와주는 브랜치
    * 메인 브랜치와는 다르게 필요할 때마다 생성하였다가 삭제
* feature 브랜치
    * 브랜치 생성 : develop으로 부터
    * merge : develop으로prefix : feature/
    * feature 브랜치는 특정 기능 하나에 대하여 사용
  
* release 브랜치
    * 브랜치 생성은 devleop으로 부터
    * merge : master와 develop으로
    * prefix: release/
    * release 브랜치는 배포를 위한 준비를 할 수 있는 브랜치
    * merge된 master를 배포
    * release 브랜치를 따로 가져가기 때문에 develop 브랜치에서는 바로 다음 배포를 위한 기능을 시작할 수 있다.
  
* hotfix 브랜치
    * 급한 것을 위해 master에서 생성
    * merge: master와 develop으로

![[사진] 깃 플로우 도표 넣기](gitflow.jpg)

### Github flow
* Gitflow는 너무 복잡
* 대부분의 케이스에서 gitflow처럼 복잡한 workflow가 불필요
* master 브랜치는 항상 배포 가능한 상태여야 한다.
* 새로운 기능 개발은 명확한 브랜치 이름으로 master에서 생성
* 토픽 브랜치의 커밋은 빈번하게 push
* 피드백 , 도움이 필요하거나 merge할 준비가 되었다면 PR

#### 언제나 PR을 생성
* 라인 단위로 코멘트 가능
* PR 자체에서도 코멘트 가능

### 리뷰가 완료된 것만 merge 👍
* 👍 과 같은 표시로 사용

## GitLabFlow
* 기존 `GithubFlow`에서 `Production` 이 추가되어 배포 필요 시 master에서 production으로 merge하여 배포

#### Environment Branches
* 환경에 맞게 브런치를 추가하여 쓰자

#### Release Branches
* 마이너 버전 릴리즈 브랜치가 존재
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
# [GIT] git & github 중급
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

피쳐 두번째 커밋
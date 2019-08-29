# Git

###### Tech Talk: Linus Torvalds on git

git maked: Linus Tovalds

https://youtu.be/4XpnKHJAok8





```
# 끝말잇기
git을 통한 협업 프로젝트

## 협업시작
부하는 들어라. 내가 쓴 단어로부터 끝말잇기를 시작해라.

- 
```





**git init**: .git을 생성. git정보를 기록한다.



**git status**: 



git은 바로 저장되지 않고 중간 레벨을 두었다. = Staging Area (INDEX)

| Working Directory |         | Staging Area (Index) |            | Commit Log |
| ----------------- | ------- | -------------------- | ---------- | ---------- |
| 업로드할 Code파일 | **add** | commit을 위한 접시   | **commit** | git에 기록 |



**git log**: Commit log 출력

* SHA1 해시알고리즘으로 Comiit ID를 가진다.
* 블록체인과 유사한 구조.

**git log --oneline**: 간략하게 출력.



**git remote -v**: remote 원격장소 확인.





### GIt의 강점

* 관리주체가 회사 1곳이 아니라, 참여하는 모든 사람





### Git Issue





### Git Pull Request

Fork 한 Repository를 수정하여 수정을 요청할 수 있다.



### Git Fork

단순한 복사가 아니다.

Collaboration을 받지 못한 사용자들이 수정을 요청할 수 있다.



Master에서 merge를 하지 않으면, 또는 추가로 Commit한 부분에 대해서는 일치 하지 않는 문제가 발생한다.





### Git Checkout

**git checkout [hashnum]**: hashnum commit으로 돌아간다.!

**git checkout master**: 마지막수정으로 돌아온다.



### Git Branch

```
c:\codes\branch (master -> origin)
λ git log --oneline
51eba4b (HEAD -> master) add team member
b005c0d add Skillset
0f15076 profile first commit

c:\codes\branch (master -> origin)
λ git branch slice

c:\codes\branch (master -> origin)
λ git log --oneline
51eba4b (HEAD -> master, slice) add team member
b005c0d add Skillset
0f15076 profile first commit

c:\codes\branch (master -> origin)
λ git branch
* master
  slice

c:\codes\branch (master -> origin)
λ git checkout slice
Switched to branch 'slice'

c:\codes\branch (slice -> origin)
λ git branch
  master
* slice
```

* branch는 평행 Git 세계를 만는다.
* master는 최종으로 결정되는 부분을 수정하고, branch에서 테스트 한다.



### Git Merge

```
c:\codes\branch (slice -> origin)
λ git log --oneline
50160ba (HEAD -> slice) add contents to project
30fcc07 start real Project
1fbc582 start Project
51eba4b (master) add team member
b005c0d add Skillset
0f15076 profile first commit

c:\codes\branch (slice -> origin)
λ git checkout master
Switched to branch 'master'

c:\codes\branch (master -> origin)
λ git merge slice
Updating 51eba4b..50160ba
Fast-forward
 index.html | 4 ++++
 1 file changed, 4 insertions(+)

c:\codes\branch (master -> origin)
λ git status
On branch master
nothing to commit, working tree clean

c:\codes\branch (master -> origin)
λ git log --oneline
50160ba (HEAD -> master, slice) add contents to project
30fcc07 start real Project
1fbc582 start Project
51eba4b add team member
b005c0d add Skillset
0f15076 profile first commit
```



### Git Push

**git pull/push [remote name] [branch name]**




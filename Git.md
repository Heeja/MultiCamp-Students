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

**git log --oneline**: 간략하게 출력



**git remote -v**: remote 원격장소 확인


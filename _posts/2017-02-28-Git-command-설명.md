---
layout: post
title: Git command 설명
date: 2017-02-28 00:00:00
categories: git
---

- 저장소 받아오기

```
git clone https://github.com/whitelife/whitelife.github.com.git
```

- 파일 추가

```
git add file
git add *
```

- 확정하기

```
git commit -m "설명"
```

- 발행하기

local 저장소에서 remote 저장소로 올리기.

```
git push origin master
```

- branch 만들기

```
git checkout -b feature
```

- branch 이동하기

```
git checkout master
```

- local branch 삭제하기

```
git checkout -d feature
```

- remote branch 삭제하기

```
git push origin --delete feature
```

- remote branch 발행하기

```
git push origin feature
```

- 갱신하기

```
git pull
```

- branch 병합하기

```
git merge feature
```

- branch 비교하기

```
git diff feature master
```

- tag 생성하기

```
git tag v1.0
```

- local tag 삭제하기

```
git tag -d v1.0
```

- remote tag 삭제하기

```
git push origin :refs/tags/v1.0
```

- remote tag 발행하기

```
git push origin v1.0
```

- local 파일 HEAD 복원하기

```
git checkout -- file
```

- 발행 hash 확인

```
git rev-list --reverse HEAD
git rev-list --reverse HEAD | head -1
```

- simple log

```
git log --pretty=oneline
git log --pretty=oneline --reverse
```

- tree log

```
git log --pretty=oneline --graph --decorate --all
```

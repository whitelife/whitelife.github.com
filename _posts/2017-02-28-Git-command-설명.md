---
layout: post
title: Git command 설명
date: 2017-02-28 00:00:00
categories: git
---

## Branch

### 모든 branch 목록보기

local, remote branch가 조회된다.

```
git branch --all
* develop
  feature/test
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/develop
  remotes/origin/hotfix
  remotes/origin/master
```

### 원격 저장소에 branch 발행하기

```
$ git push origin feature/test
 * [new branch]      feature/test -> feature/test
```

### 원격 저장소에 branch 삭제하기

```
 git push origin --delete feature/test
 - [deleted]         feature/test
```

## 기능개발하기

### 개발 branch 전환하기

개발 branch로 이동한다.

```
git checkout develop
Switched to branch 'develop'
Your branch is up-to-date with 'origin/develop'.
```

### branch 생성하기

local branch를 생성한다.

```
git checkout -b feature/test
Switched to a new branch 'feature/test'
```

### 수정사항 branch 적용하기

#### 수정사항 추가

```
git add benchmark/test.js
```

#### 수정사항 확정

```
git commit -m 'test commit'
[feature/test 339387a] test commit
The file will have its original line endings in your working directory.
 1 file changed, 4 insertions(+)
 create mode 100644 benchmark/test.js
```

자세하게 메시지 작성이 필요한경우 사용한다.

```
git commit --amend

test commit

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Thu Mar 9 01:57:27 2017 +0000
#
# On branch feature/test
# Changes to be committed:
#       new file:   benchmark/test.js
#
```

## log 확인하기

### 간단한 log 보기

```
git log --oneline
feb44a9 test commit
```

### 상세 log 보기

```
$ git log feb44a9 --max-count=1
commit feb44a9e9ad33c93b8ca470fef9890072ae3f597
Author: unknown <parkmc_0@naver.com>
Date:   Thu Mar 9 01:57:27 2017 +0000

    test commit
```

### log 및 수정사항 보기

```
$ git show feb44a9e9ad33c93b8ca470fef9890072ae3f597
commit feb44a9e9ad33c93b8ca470fef9890072ae3f597
Author: unknown <parkmc_0@naver.com>
Date:   Thu Mar 9 01:57:27 2017 +0000

    test commit

diff --git a/benchmark/test.js b/benchmark/test.js
new file mode 100644
index 0000000..7bcf7c2
--- /dev/null
+++ b/benchmark/test.js
@@ -0,0 +1,4 @@
+
+'use strict';
+
+console.log('test');
```

## 취소 및 복구

### 파일 추가 취소하기

```
git rm --cached benchmark/test.js
```

### 삭제한 파일 복구하기

```
git checkout -- benchmark/test.js
```

### commit 합치기

2개의 commit을 합친다.

```
git reset HEAD~2
```

### commit 취소하기

```
git revert 1f46efe5f368e04615d56994b3e89ab74591d7af
[feature/test 3caf4cc] Revert "test commit"
 1 file changed, 5 deletions(-)
 delete mode 100644 benchmark/test.js
```

### merge 취소하기

```
git reset --merge develop
```



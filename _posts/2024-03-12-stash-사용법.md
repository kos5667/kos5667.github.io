---
layout: post
title:  "Git Stash를 활용하는 방법."
date:   2024-03-12 09:00:00 +0900
excerpt_image: "../assets/images/git-stash.png"
categories: Git
tags: [git, stash]
---
## Git Stash.
`git stash`는 Git에서 제공하는 매우 유용한 기능 중 하나로, 작업 중인 변경 사항을 임시로 저장하고 나중에 다시 적용할 수 있게 해줍니다. 이 기능은 브랜치 간에 이동해야 하거나 다른 작업을 처리하기 전에 현재 작업 중인 변경 사항을 깨끗하게 보관하고 싶을 때 유용합니다.

### Git Stash 사용법

1. **Stash 생성**: 현재 작업 중인 변경 사항(스테이징된 변경 사항과 스테이징되지 않은 변경 사항 모두)을 stash에 저장하려면 다음 명령어를 사용합니다.

```bash
git stash
```

또는

```bash
git stash push
```

변경 사항에 대한 설명을 추가하고 싶다면 `-m` 옵션을 사용하여 메시지를 추가할 수 있습니다.

```bash
git stash push -m "내 변경 사항 설명"
```

<br/>
2. **Stash 목록 확인**: 저장된 stash 목록을 확인하려면 다음 명령어를 사용합니다.

```bash
git stash list
```
<br/>
3. **Stash 적용**: 가장 최근에 stash된 변경 사항을 현재 브랜치에 적용하고 싶다면 다음과 같이 명령합니다.

```bash
git stash apply
```

특정 stash를 적용하고 싶은 경우, stash 목록에서 해당 stash의 이름을 찾아서 사용합니다(예: `stash@{0}`).

```bash
git stash apply stash@{0}
```
<br/>
4. **Stash 삭제**: stash 적용 후에는 stash 목록에서 해당 항목을 삭제할 필요가 있습니다. 가장 최근의 stash를 삭제하려면 다음 명령어를 사용합니다.

```bash
git stash drop
```

특정 stash를 삭제하려면, 해당 stash의 이름을 명시합니다.

```bash
git stash drop stash@{0}
```
<br/>
5. **Stash 적용 및 삭제**: stash를 적용하고 바로 삭제하고 싶다면 `pop` 명령어를 사용합니다.

```bash
git stash pop
```

이 명령어는 가장 최근의 stash를 현재 브랜치에 적용한 후, 해당 stash를 목록에서 삭제합니다.

`git stash` 기능은 변경 사항을 임시로 보관하고 나중에 다시 작업을 재개할 수 있게 해주어, Git을 사용하는 개발자에게 매우 유용한 도구입니다.
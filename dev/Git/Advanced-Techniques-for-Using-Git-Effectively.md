---
title: Git을 효율적으로 사용하는 추가 명령어들
description: 
published: true
date: 2023-02-17T18:06:17.908Z
tags: git
editor: markdown
dateCreated: 2023-02-17T17:37:53.651Z
---


# Git을 효율적으로 사용하는 추가 명령어들

Git은 개발자가 코드베이스의 변경 사항을 추적하고 다른 사람과 협업할 수 있는 강력한 버전 제어 시스템입니다. 많은 개발자가 Git을 정기적으로 사용하지만 Git을 더욱 효과적으로 사용하는 데 도움이 되는 고급 기술이 있습니다. 이 블로그 게시물에서는 가장 유용한 고급 Git 기술 중 일부를 다룰 것입니다.

## 1. Rebase

Git에서 가장 강력하고 잠재적으로 위험한 기술 중 하나는 Rebase입니다. Rebase는 브랜치를 새로운 기본 커밋으로 이동하여 브랜치 기록을 효과적으로 다시 작성하는 프로세스입니다. 이는 지저분한 기록을 정리하거나 여러 브랜치의 변경 사항을 통합하는 데 유용할 수 있습니다. 그러나 Rebase는 충돌을 일으키고 버그를 추적하기 어렵게 만들 수도 있습니다. Rebase를 신중하고 신중하게 사용하는 것이 중요합니다.

브랜치를 Rebase하려면 다음 명령을 사용하십시오.

```
git rebase <new-base>
```

- [Git Rebase*wiki.yowu.dev*](/ko/dev/Git/git-rebase)
{.links-list}

## 2. Interactive Rebase

대화식 리베이스(Interactive Rebase)는 분기 히스토리에서 커밋을 선택적으로 편집, 삭제 또는 재정렬할 수 있는 고급 Rebase 형식입니다. 이는 커밋 메시지를 정리하거나 관련 커밋을 결합하거나 불필요한 변경 사항을 제거하는 데 유용할 수 있습니다.

대화식 리베이스를 시작하려면 다음 명령을 사용하십시오.

```
git rebase -i <new-base>
```

- [Git Interactive Rebase*wiki.yowu.dev*](/ko/dev/Git/git-interactive-rebase)
{.links-list}

## 3. Cherry-picking

체리 피킹(Cherry-picking)은 한 브랜치에서 다른 브랜치로 개별 커밋을 적용하는 기술입니다. 이는 전체 브랜치를 병합하지 않고 한 브랜치에서 다른 브랜치로 특정 변경 사항을 통합하려는 경우에 유용할 수 있습니다.

커밋을 Cherry-picking하려면 다음 명령을 사용합니다.

```
git cherry-pick <commit-hash>
```

- [Git Cherry-pick*wiki.yowu.dev*](/ko/dev/Git/git-cherry-pick)
{.links-list}

## 4. Stash

Stash는 커밋할 준비가 되지 않은 변경 사항을 임시로 저장할 수 있는 Git의 기능입니다. 이는 현재 변경 사항을 커밋하지 않고 다른 브랜치로 전환하거나 다른 기능에 대해 작업해야 할 때 유용할 수 있습니다.

변경 사항을 숨기려면 다음 명령을 사용하십시오.

```
git stash save
```

숨겨진 변경 사항을 적용하려면 다음 명령을 사용하십시오.

```
git stash apply
```

- [Git Stash*wiki.yowu.dev*](/ko/dev/Git/git-stash)
{.links-list}

## 5. Git Reflog

Git reflog는 손실된 커밋 또는 브랜치를 복구하기 위한 강력한 도구입니다. Reflog는 변경 사항을 삭제한 경우에도 모든 변경 사항을 포함하여 Git 리포지토리의 기록을 추적합니다. 이는 손실된 커밋이나 실수로 삭제된 브랜치를 복구하는 데 유용할 수 있습니다.

reflog를 보려면 다음 명령을 사용하십시오.

```
git reflog
```

- [Git Reflog*wiki.yowu.dev*](/ko/dev/Git/git-reflog)
{.links-list}

![git-logo.png](/git-logo.png){.align-center}

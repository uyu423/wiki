---
title: EUCKR 인코딩을 UTF8-로 바꾸는 명령어
description: 
published: true
date: 2022-11-24T08:42:08.232Z
tags: terminal, encoding
editor: markdown
dateCreated: 2022-11-24T04:41:07.577Z
---

```bash
iconv -f euc-kr -t utf-8 update_needed_users.csv > update_needed_users_utf8.csv
```

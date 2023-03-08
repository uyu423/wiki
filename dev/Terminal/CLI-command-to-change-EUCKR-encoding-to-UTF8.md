---
title: EUC-KR 인코딩을 UTF-8 로 바꾸는 명령어
description: 
published: true
date: 2023-02-17T17:59:11.264Z
tags: terminal, encoding
editor: markdown
dateCreated: 2022-11-24T04:41:07.577Z
---

# bash CLI

> `iconv -f encoding [-t encoding] [inputfile] ...`


## Example

```bash
iconv -f euc-kr -t utf-8 update_needed_users.csv > update_needed_users_utf8.csv
```

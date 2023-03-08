---
title: 윈도우 탐색기에서 SFTP 폴더 사용하기
description: 
published: true
date: 2023-02-19T11:46:17.565Z
tags: sftp, windows
editor: markdown
dateCreated: 2023-02-19T11:44:01.082Z
---

## 필요 msi 설치

- https://github.com/billziss-gh/winfsp/releases/latest
- https://github.com/billziss-gh/sshfs-win/releases/latest

## "내 PC" - "네트워크 드라이브 연결"

![sftp-in-windows-1.png](/sftp-in-windows-1.png)
![sftp-in-windows-2.png](/sftp-in-windows-2.png)
![sftp-in-windows-3.png](/sftp-in-windows-3.png)

## 기타

### 우분투의 경우

- 로그인한 계정의 홈 디렉토리 외부는 접근이 안된다.
  - 보안상 접근하지 않는 것이 좋지만, 만약 필요하다면 외부의 디렉토리를 홈 디렉토리로 마운트시키면 윈도우 네트워크 드라이브로 접근할 수 있다.
  
```bash
sudo apt install bindfs
```

```bash
mkdir link_directory
```

```bash
bindfs  --no-allow-other /media/tc1/origin_directory /home/yowu/link_directory
```

- 언마운트할 때는 `rm -r`이 아닌 `umount` 명령어를 사용한다.

```bash
sudo umount /home/yowu/link_directory
```

### References

- [[Windows] 외부 ssh 서버 폴더 연결*nuggy875.tistory.com*](https://nuggy875.tistory.com/160)
- [How do I mount a folder from another partition?*askubuntu.com*](https://askubuntu.com/questions/205841/how-do-i-mount-a-folder-from-another-partition)
- [bindfs, inverse operation?*stackoverflow.com*](https://stackoverflow.com/questions/19336170/bindfs-inverse-operation)
{.links-list}
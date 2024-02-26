---
title: "[aws] solved, aws private key bad permissions error"
categories:
  - aws
tags:
  - aws
  - private key
  - bad permission
---

# aws private key bad permission error

## ssh 연결 cmd 입력하면 다음과 같은 오류가 발생한다.

```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'private_key.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "private_key.pem": bad permissions
```


해당 오류는 private_key.pem 파일의 접근 권한으로 발생하는 오류이다.
private_key.pem의 권한을 나에게만 읽기 권한으로 부여하면 오류가 해결된다.

```bash
chmod 400 private_key.pem
```




 
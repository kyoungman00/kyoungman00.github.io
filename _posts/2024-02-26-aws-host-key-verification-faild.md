---
title: "[aws] solved, aws host key verification faild error"
categories:
  - aws
tags:
  - aws
  - host key
  - host key verifictaion faild
---

# aws host key verification faild error

## ssh 연결 cmd 입력하면 다음과 같은 오류가 발생한다.

```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@  
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @  
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@  
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!  
Someone could be eavesdropping on you right now (man-in-the-middle attack)!  
It is also possible that a host key has just been changed.  
The fingerprint for the ED25519 key sent by the remote host is  
SHA256:gxj6hpPerSdBpbfB59rco9VKOqTZgFjeNzvX0y6YugA.  
Please contact your system administrator.  
Add correct host key in "PATH"/.ssh/known_hosts to get rid of this message.  
Offending ED25519 key in "PATH"/.ssh/known_hosts:2  
Host key for ec2-xx-xx-xxx-xxx.ap-southeast-2.compute.amazonaws.com has changed and you have requested strict checking.  
Host key verification failed.  
```



"PATH"/.ssh/known_hosts 의 2번째 line의 host key가 변경되어서 그렇다. 

sudo vim "PATH"/.ssh/known_hosts로 파일을 수정해준다. 
필자는 입력되어있는 내용을 모두 지워서 해결하였다.




 
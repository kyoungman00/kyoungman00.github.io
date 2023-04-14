---
title: "[server] cors error access-control-allow-origin"
categories:
  - server
tags:
  - server
  - iis
  - cors
  - access-control-allow-origin
---


# access-control-allow-origin cors error
Web 통신의 보안을 위해, server와 browser간 동일 origin(domain, scheme, port)간에 통신만 가능하다.   


> 'Access-Control-Allow-Origin' header is present on the requested resource!  


발생 원인은 server 와 browser의 origin이 다르기 때문이다. 



# solution
server에 허용할 origin을 명시하여 cors error 발생을 막을 수 있다. 


server의 web.config에 아래 내용을 추가하자. 

```xml
~
<system.webServer>
	<httpProtocol>
      <customHeaders>
        <add name="access-control-allow-origin" value="*" />
        <add name="Access-Control-Allow-Headers" value="Content-Type" />
        <add name="Access-Control-Allow-Methods" value="GET,POST,PUT,DELETE,OPTIONS" />
        <add name="Access-Control-Allow-Credentials" value="true" />
      </customHeaders>
    </httpProtocol>
</system.webServer>
~
```


# tip
위 config를 추가하여도 cros error를 피할 수 없다면, web server api에 options method가 구현되어있는지 확인하자. 
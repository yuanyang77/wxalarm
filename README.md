# 企业微信报警接口应用
## 运行示例
```
docker run -d --rm \
--name wxalarm \
-e SECRET="xxxx" \
-e CORPID="xxxx" \
-e AGENTID=xxx \
-p 51001:51001 \
wxalarm:[tag]

```

## Shell

```
#!/bin/bash
wechat()
{
                DT_ADDR='127.0.0.1:51001'
                #处理下编码，用于合并告警内容的标题和内容
                #中文需要utf8编码并进行urlencode
                message=$(echo -e "$title\n$content"|od -t x1 -A n -v -w1000000000 | tr " " %)
                DT_URL="http://$DT_ADDR/send_message?content=$message"
                /usr/bin/curl $DT_URL
}

#title=test
#content=test
#wechat

```

## Python

```
#!/usr/bin/python
# coding: utf-8
#
from urllib import quote
import urllib2
import sys

reload(sys)
sys.setdefaultencoding('utf-8')

def wechat(title,content):
        Title = quote(title.encode('utf8'))
        Content = quote(content.encode('utf8'))
        API_URL="http://127.0.0.1:51001/send_message?content=%s%s" % (Title,Content)
        try:
            req = urllib2.Request(API_URL)
            result = urllib2.urlopen(req)
            res = result.read()
        except:
            print "error"


```

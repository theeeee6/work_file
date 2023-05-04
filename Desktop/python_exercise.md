# python处理简单逻辑

```py
s = "helloHworld123"
len_num = 0
len_eng = 0 
for i in range(len(s)):
    if((s[i]>='A' and s[i]<='Z') or (s[i]>='a' and s[i]<='z')):
        len_eng+=1
    elif(s[i]>='0' and s[i]<='9'):
        len_num+=1
```



# 列表去重

```
# 内置函数
l =[1,1,2,2,3]
a = set(l)
a = list(a)
print(a)

# 非内置函数
for i in range(len(l)):
    for j in range(i+1,len(l)):
        if(l[i] == l[j]):
            l.pop(i)
            break;
print(l)
```



# 删除素数并输出最大值

```
import random
l = [random.randint(0, 100)for i in range(100)]

def prime_number(a):
    if(a%2 !=0 and a%3 !=0 and a%5!=0 and a%7 !=0):
        return True;
    return False;

l1 = []
for i in range(len(l)):
    if(not prime_number(l[i])):
        l1.append(l[i])        
print(max(l1))
```



# lscpu解析

```
import os
filepath = r'C:\Users\83989\Desktop\lc.txt'
dict_kv = {}
with open(filepath, "r", encoding="utf-8") as file:
    content = file.read()
    lines = [] #换行符的位置
    lines.append(0)
    next_colon = [] #冒号的位置
    for i in range(len(content)):
        if(content[i]=="\n"):
            lines.append(i)
        if(content[i]==":"):
            next_colon.append(i)
            
    for i in range(len(next_colon)):
        key = ""
        for k in range(lines[i],next_colon[i]):
            key += content[k]
        value = ""
        for v in range(next_colon[i]+1,lines[i+1]):
            if(content[v]==' '):
                continue
            value += content[v]
        dict_kv[key]=value
        #print(key)
        #print(value)
        
#print(dict_kv)

import json
js = json.dumps(dict_kv)
print(js)
# print(lines)
# print(next_colon)
```



# requests库获得百度

```
import requests
r = requests.get('https://www.baidu.com/')
print(r.status_code)
print(r.content)
```



# 未完成的list

在Linux机器上SSH连接另外一台Linux机器运行lscpu命令，打印输出

​		Linux机器数量不够，待完成

获取母机所有adam组件版本号及其健康状态（本地、SSH两种形式）

​		暂未了解母机、adam以及健康状态的定义，待完成

使用正则表达式从speccpu txt结果中找出测试值

​		没有speccpu.txt文件，待完成

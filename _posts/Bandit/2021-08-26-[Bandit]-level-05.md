---
title:  "[Bandit] level 0~5"

categories: bandit
tags: [bandit]

toc: true
toc_sticky: true

date: 2021-08-26 18:18:33
---

https://overthewire.org/wargames/

kali linux 에서 ssh 접속법

ssh bandit_@bandit.labs.overthewire.org -p 2220

_ 부분에는 레벨을 적어주면 됨

# level 0 → level 1

ssh bandit0@bandit.labs.overthewire.org -p 2220

비밀번호 : bandit0

![image](https://user-images.githubusercontent.com/69203345/130926147-4b430932-5216-4dad-9804-72dd892a4d88.png)

home directory에 있는 readme 에 비밀번호가 있다고 한다

![image](https://user-images.githubusercontent.com/69203345/130926488-713b3a14-42cd-42a0-9f06-da0d1fd67d3d.png)

다음 레벨의 비밀번호를 찾았다

# level 1 → level 2

![image](https://user-images.githubusercontent.com/69203345/130928962-050bad83-8d38-4c07-9405-53da30574346.png)

홈 디렉토리에 - 파일에 있다고 하는거 같은데

![image](https://user-images.githubusercontent.com/69203345/130929744-d60a7420-1c02-4f91-ad0f-9c44d8f8d2b5.png)

\- 형태의 파일은 

cat < filename

cat ./- 로 읽을 수 있다

# level 2 → level 3

![image](https://user-images.githubusercontent.com/69203345/130930127-eff06216-b7f3-4f60-b614-144d82ac29df.png)

이번에는 파일 이름이 공백이란다

![image](https://user-images.githubusercontent.com/69203345/130930329-a0e9fb7b-be8f-477f-9c2b-6885bc65e43e.png)

공백이 있다는 거였구나 공백이 아니라

공백이 있는 경우엔 " " 로 묶어주면 읽을 수 있다

# level 3 → level 4

![image](https://user-images.githubusercontent.com/69203345/130931782-9fd3af49-8c4c-4ca1-9b72-1ae35b72b88c.png)

inhere 디렉토리에 숨김 파일로 돼있나보다

![image](https://user-images.githubusercontent.com/69203345/130932164-6a3ff1a8-0d0f-4134-b55b-b0ca07d350b6.png)

inhere 폴더로 이동후 ls -al로 숨김 파일을 찾았다

# level 4 → level 5

![image](https://user-images.githubusercontent.com/69203345/130936226-4823d45b-39f2-4ff1-9ba7-5c8cab01d020.png)

인간이 읽을수 있는 파일?

![image](https://user-images.githubusercontent.com/69203345/130936772-e8f56b7f-28b0-4839-8441-3c732a15383a.png)

나머지는 특수문자등으로 읽을 수 없는걸로 봐선 이게 맞는듯
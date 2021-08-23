---
title:  "[Android][Java] Android Studio 시작하기,버튼 추가 맛보기"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-08-23 21:48:33 \
---

# Android Studio 시작하기

## 프로젝트 파일 만들기

![1](https://user-images.githubusercontent.com/69203345/130451105-af328e95-0af2-4516-a2d4-2aeda78ea99f.PNG)

new project → Empty Activity 클릭 한후 이름은 원하는걸로

![2](https://user-images.githubusercontent.com/69203345/130451212-a1c6a55b-650f-40e2-b869-be65ad99d443.PNG)

language java로 바꿔줄것

finish 누른 후 실행창

![3](https://user-images.githubusercontent.com/69203345/130451220-b2194685-ab12-4dc3-81cd-2b4b549aa926.PNG)

첫 프로젝트 로딩은 조금 시간이 걸린다 

기다리면 폴더랑 다 뜬다!

![4](https://user-images.githubusercontent.com/69203345/130451223-3c430c5e-fe98-4d67-8b31-ca007d679d6d.PNG)

activity_main,xml 탭을 열면 이런걸 볼 수 있는데

두개다 만들 앱의 화면이다 다만,

왼쪽은 디자인 화면, 보통 생각하는 우리한테 보이는 화면이다

오른쪽은 청사진 화면, 뭔가 만들다 보면 겹쳐있는 경우가 있을텐데 그때 보면 된다



에뮬레이터 받기

오른쪽 위에 핸드폰 모양 아이콘 (avd manager) 클릭

![5](https://user-images.githubusercontent.com/69203345/130451225-9514cfa0-3e22-49d2-853e-aa5b61d1140f.PNG)

저는 이걸로 했습니다

next 누른후

![6](https://user-images.githubusercontent.com/69203345/130451229-c5fdbdc4-3d28-4c43-b5e0-768322c8a9c0.PNG)

이걸로 받았습니다

이미 받고 난 뒤에 캡쳐라 Download는 없다는거

용량이 크니 천천히ㅣㅣㅣ 기다리면 됩니다

다운로드가 다 된후 avd manager 를 클릭하면 다운돼있는 에뮬레이터를 클릭!

그럼 핸드폰이 나옵니다

그럼 궁금하니까 바로 위에 ▶ 모양 클릭!

그럼 이런게 뜬다!

<img src="https://user-images.githubusercontent.com/69203345/130451233-2de7bf30-3ea6-4c6f-ad82-bf6866b9e1fb.PNG" alt="7" style="zoom:67%;" />

만약 SDK 라이선스 오류가 뜬다면

file - setting - apperance & behavior - system setting - android sdk 로 들어가서 

sdk tools 탭 에있는 Android SDK Command-line Tools 를 받아주면 된다

본인도 오류떠서 이걸로 해결함 

중지는 ■ 버튼 클릭

**화면 구성은 .xml 파일, 동작기능 소스코드(.java) 파일로 기능**

## 설정 바꿔주기

File - Settings - Editor - General - Auto Import

- Add unambiguous imports on the fly 체크

- Optimize imports on the fly ( for current project ) 체크

안드로이드 스튜디오에서 자동으로 import구문을 자동으로 넣는 기능

코드가 입력되었을 때 필요한 import 구문을 자동으로 넣을 수 있는 기능을 제공한다.

## 화면에 버튼 추가

![8](https://user-images.githubusercontent.com/69203345/130451720-6755bdfc-6d2b-4da4-b903-aeb85ab72701.PNG)

왼쪽 팔레트에서 버튼을 드래그해서 화면에 붙이기

<img src="https://user-images.githubusercontent.com/69203345/130451724-85c01f7d-aa0e-472f-90f2-f6bcc99468d6.PNG" alt="9" style="zoom:67%;" />

오른쪽 에서 text 및 onClick 바꿔주기

onClick 에는 클릭 했을때 발생할 이벤트를 적어놓은 함수(메소드)의 이름을 적어주면됨

대소문자 꼭 구분

<img src="https://user-images.githubusercontent.com/69203345/130451726-a03a2ad2-f9ee-4696-beee-3857e5feb217.PNG" alt="10" style="zoom: 80%;" />

아직 MainActivity.java 파일에 적어놓은 함수가 없기때문에 오류가 뜨는것이 당연

**.java 파일에 입력** 

```java
public void onButton1Clicked(View v){
    Toast.makeText(this, "확인1 버튼이 눌림",Toast.LENGTH_LONG).show();
}
```

this 만 입력하면 자동으로 context: 이 생김, context: 은 타이핑 하는게 아님

잠깐 나타났다 사라지는 메세지를 토스트(Toast) 메세지 라고 함



위에처럼 버튼을 2개 더 만듦

네이버로 이동할 버튼, 전화번호 입력화면으로 이동할 버튼 추가 하기

 **.java 파일에 입력** 

```java
public void onButton2Clicked(View v){ //웹을 띄우고 네이버사이트를 보여줌
    Intent internet = new Intent(Intent.ACTION_VIEW,Uri.parse("http://m.naver.com")); //internet은 변수의 이름
    startActivity(internet);
}
public void onButton3Clicked(View v){ //전화번호 입력 화면으로 이동
    Intent call = new Intent(Intent.ACTION_VIEW,Uri.parse("tel:010-1234-5678"));
    startActivity(call);
}
```




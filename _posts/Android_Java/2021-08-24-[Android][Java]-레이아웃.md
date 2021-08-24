---
title:  "[Android][Java] 레이아웃"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-08-24 22:55:28 
---

새 프로젝트 empty activity 로 시작

버튼 만들기

<img src="https://user-images.githubusercontent.com/69203345/130575563-01f9d9dc-7449-483c-86d7-efec18adff2f.png" alt="image" style="zoom:67%;" />

속성

- text = 안녕하세요
- layout_width = 200dp 

dp는 단위, px로 만들수 있지민

px로 만들경우 단말기 마다 크기가 달라질수 있음

# 레이아웃 변경

## LinearLayout

Component Tree 에서 ContraintLayout 오른쪽 클릭,

Convert view 에서 LinearLayout 으로 변경해주면

만들어놓은 버튼 속성에서

![image](https://user-images.githubusercontent.com/69203345/130576308-bf7dff65-55cd-468d-902d-af23374d8829.png)

match parent 속성 사용 가능 

layout_marginLeft = 50dp

layout_marginTop = 50dp 로 속성 변경

margin - 얼마나 띄울 것 인지 값을 정함

현재 보이는 화면

<img src="https://user-images.githubusercontent.com/69203345/130577025-350d3bbe-690a-443f-b4bc-45297065b7bb.png" alt="image" style="zoom:67%;" />

## ConstraintLayout

다시 Convert view 에서 ConstraintLayout으로 변경한후 

버튼을 추가하며 가이드라인, 연결점/선을 이용해봄

<img src="https://user-images.githubusercontent.com/69203345/130579505-c5a39444-38a1-4353-9b6e-c83c29f05e3c.png" alt="image" style="zoom: 67%;" />

왼쪽에 보이는 세로 선이 가이드 라인 이다

버튼의 연결점을 이용해 가이드라인에 부착 사용할수 있다

연결점 - 버튼을 클릭해서 나오는 상하좌우의 점

연결선 - 연결점을 레이아웃, 가이드라인에 붙였을때 나오는 선

다른 레이아웃들도 천천히 다뤄볼 예정

---

**새 프로젝트 empty activity 로 시작**

# 레이아웃

## 리니어 레이아웃

**convert view 에서 LinearLayout 으로 변경**

오른쪽 속성에서 

![image](https://user-images.githubusercontent.com/69203345/130586931-6a90946e-9d1a-4035-b3a7-2af6b882088d.png)

vertical 로 설정

그럼 이제 세로방향으로 쌓을수 있음

<img src="https://user-images.githubusercontent.com/69203345/130587072-a203b0bd-004e-4cee-8127-dbc0a0f48326.png" alt="image" style="zoom:67%;" />

버튼을 놓는데 어디에 놓든 위에 쌓이는 것을 볼수 있음

버튼을 더 쌓은후 vertical을 horizonal로 바꾸고 

layout_width를 wrap_content로 바꾸면

vertical과 다르게 horizonal 에서는 가로 방향으로 쌓이는 것을 볼 수 있다

<img src="https://user-images.githubusercontent.com/69203345/130609560-1e4683f6-2f41-419a-8da3-c38842680680.png" alt="image" style="zoom:67%;" />

vertical과 horizonal을 바꿔주는 orientation은 리니어 레이아웃의 만의 필수 속성이다

layout_gravity와 gravity속성 값의 변경

<img src="https://user-images.githubusercontent.com/69203345/130611479-a3f03f58-a036-4fa2-8a03-5e2f671c1b2f.png" alt="image" style="zoom:67%;" />

layout_gravity 속성은 정렬 속성이다 (왼쪽 정렬, 가운데 정렬, 오른쪽 정렬)

**gravity속성과 layout_gravity 속성의 차이**

layout 이 붙어있으면 이 뷰(버튼 하나)가 레이아웃의 어디에 정렬될지 라면,

그냥 gravity는 뷰 안의 내용물에 대한 정렬이다



horizonal로 변경 (바꿔준것도 원래대로), baselineAligned속성 = true

- baselineAligned = 글자들에 같은 선 위에 표시되어있게 만듦

![image](https://user-images.githubusercontent.com/69203345/130614908-57052693-5ecb-4536-91e5-d6062cf45ace.png)

textSize, height, margin, padding 속성 변경

**글자크기는 dp가 아닌 sp 사용**

### 공간분할

vertical로 바꾼후 바꿔놓은 값 다시 원래대로 한 상태에서 진행

layout_weight 사용

- 이미 채워있는 공간 이외의 여유공간을 나눠서 배분해줌

<img src="https://user-images.githubusercontent.com/69203345/130615812-b64e7d83-7b18-4470-a1db-92d17ffa10db.png" alt="image" style="zoom:67%;" />

세 버튼의 layout_height 를 0dp로 바꾼후 layout_weight를 1로 설정하면

1/3 씩 나눠가진걸 볼 수 있다

## 상대 레이아웃

새 프로젝트 만들어서 진행

layout도 RelativeLayout으로 바꿔주기

<img src="https://user-images.githubusercontent.com/69203345/130618784-58f1e11a-487a-4bd8-9539-619de82e1a81.png" alt="image" style="zoom:50%;" />

버튼은 layout_width 속성 match_parent로 바꾸고

가운데 버튼은 layout_above, layout_below속성 바꿔보기

## 프레임 레이아웃, 뷰의 전환

새 프로젝트 만들어서진행

res 아래 drawable 폴더에 사진 2장 넣어놓기, linearlayout 으로 바꾼뒤 진행

orientation 속성 vertical,

왼쪽 팔레트 에서 버튼과 framelayout을 끌어다 놓고

![image](https://user-images.githubusercontent.com/69203345/130623706-d5fd458d-a5ef-465d-b219-c0d104f501f3.png)

팔레트에서 imageView도 올리면

<img src="https://user-images.githubusercontent.com/69203345/130623838-fe927698-cb8d-4b59-9fa9-bf87edeb0f42.png" alt="image" style="zoom:80%;" />

이런게 뜨는데 여기서 월하는 사진 선택

같은 작업 한번더!

이후 버튼의 onClick 이벤트 설정

```java
package com.example.myframelayout;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;

public class MainActivity extends AppCompatActivity {
    ImageView imageView; //첫번째 이미지를 가르킬 변수선언
    ImageView imageView2; //추가 

    int imageIndex =0;//이미지 변환을 위한 변수


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        imageView = findViewById(R.id.imageView);//
        //findViewById() -> 아이디를 이용해서 view를 찾는 함수
        imageView2 = findViewById(R.id.imageView2);//
    }
    public void onButton1Clicked(View v){//아래 모두 추가
        changeImage();
    }
    public void changeImage(){
        if (imageIndex==0){
            imageView.setVisibility(View.VISIBLE);//
            imageView2.setVisibility(View.INVISIBLE);

            imageIndex=1;
        }else if(imageIndex==1){
            imageView.setVisibility(View.INVISIBLE);
            imageView2.setVisibility(View.VISIBLE);

            imageIndex=0;
        }
    }
}
```

코드 타이핑한 부분 옆에는 주석을 붙여놨으니 참고 

## 스크롤뷰 사용하기

새 프로젝트, 리니어 레이아웃(vertical) 으로 진행

![image](https://user-images.githubusercontent.com/69203345/130627915-38787368-74c9-4f0d-82d4-445c6aae2bd0.png)

![13-1](https://user-images.githubusercontent.com/69203345/130628109-8a54b2fa-c8cd-4047-9829-cc8091c7e52c.PNG)

scrollview도 넣어줌 

(진행하면 오류는 사라짐)

![image](https://user-images.githubusercontent.com/69203345/130628858-d3a2acbd-5795-4d83-bcbb-3b15eb521964.png)

팔레트에서 textView를 ScrollView 아래에 넣어줌

그럼 이후 text가 화면을 넘는다면 스크롤 할수 있음
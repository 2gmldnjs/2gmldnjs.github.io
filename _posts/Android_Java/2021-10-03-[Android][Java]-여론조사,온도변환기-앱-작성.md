---
title:  "[Android][Java] 여론조사,온도변환기 앱 작성"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-10-03 23:57:55

---

# 여론조사 앱 작성

이미지 3장을 drawable 디렉토리에 넣어놓기

여러 라디오 버튼중에서 하나만 선택 가능하게 하기 위해서 라디오 그룹을 사용

linear layout(vertical) 사용

![image](https://user-images.githubusercontent.com/69203345/135756889-59fa0ee1-c6c1-4180-a434-28b7e91b3227.png)

![image](https://user-images.githubusercontent.com/69203345/135758744-6e0e331e-7099-470c-b109-1cfd4af61f1c.png)

디자인만 했기때문에 아직 아무 변화는 없음

라디오 버튼중 하나를 누르고 diaplay image 버튼을 누르면 이미지가 바뀌도록 작성

1. xml의 onclick 속성을 사용 하는 방법
2. 리스너를 만들고 콜백 함수를 구현 하는 방법(리스너 객체를 만들고 사용)
3. 무명 리스너를 사용하는 방법(객체를 만들지 않고 사용)

1번 방법 사용

버튼을 눌렀을때 이미지를 바꾸기 때문에 버튼에 OnClick 속성을 변경

onClick 속성을 PressButon으로 지정

MainActivity.java

```java
package com.example.survey;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.RadioButton;
import android.widget.RadioGroup;

public class MainActivity extends AppCompatActivity {
    RadioGroup group;//위젯 클래스의 객체를 담기 위한 이름들
    RadioButton button1, button2,button3;
    Button button;
    ImageView image;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        setTitle("Survey");

        group = (RadioGroup) findViewById(R.id.rgroup); //화면에 있는 라디오 그룹을 연결
        button1 = (RadioButton) findViewById(R.id.radioButton); //화면의 라디오 버튼과 연결
        button2 = (RadioButton) findViewById(R.id.radioButton2);
        button3 = (RadioButton) findViewById(R.id.radioButton3);
        button = (Button) findViewById(R.id.button);
        image = (ImageView) findViewById(R.id.imageView);

    }

    public void PressButton(View v){
        //라디오 그룹에서 어떤버튼이 체크됐는지 확인 필요 (라디오 그룹에 체크여부 확인 함수존재)
        switch (group.getCheckedRadioButtonId()){
            case R.id.radioButton: //체크돼있다면 이미지를 바꿈
                image.setImageResource(R.drawable.image0);
                break;
            case R.id.radioButton2:
                image.setImageResource(R.drawable.image1);
                break;
            case R.id.radioButton3:
                image.setImageResource(R.drawable.image2);
                break;

        }

    }
}
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/135758841-e89d75fb-046a-47af-a4c5-933bc399075b.png" alt="image" style="zoom:80%;" />
<img src="https://user-images.githubusercontent.com/69203345/135758853-891952e9-d3d1-449c-9cc4-631d4b057cc9.png" alt="image" style="zoom:80%;" />
<img src="https://user-images.githubusercontent.com/69203345/135758867-09438b1a-2489-43d6-b126-7feb0e1d3bbb.png" alt="image" style="zoom:80%;" />

# 온도변환기 앱 작성

섭씨,화씨 온도 변환

디자인

<img src="https://user-images.githubusercontent.com/69203345/135759470-6b1da2ea-7319-4c7b-8864-bf08f4a3d2f9.png" alt="image" style="zoom:80%;" />

<img src="https://user-images.githubusercontent.com/69203345/135759481-686db062-894f-4f81-9243-c7c99af78c48.png" alt="image" style="zoom:80%;" />

변환 버튼을 누를시 이벤트 발생

체크돼있으면 true

```java
package com.example.tempconverter;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.RadioButton;
import android.widget.RadioGroup;

public class MainActivity extends AppCompatActivity {
    EditText text;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        text = (EditText) findViewById(R.id.editText);
    }
    public void ClickButton(View v){
        RadioButton rb1, rb2;
        float output;
        rb1 = (RadioButton) findViewById(R.id.radioButton);
        rb2 = (RadioButton) findViewById(R.id.radioButton2);

        float inputValue = Float.parseFloat(text.getText().toString());

        if (rb1.isChecked()){ //체크돼있으면 true
            output = (inputValue - 32) *5/9;
            text.setText(String.valueOf(output)); //float 값을 문자열로 변경

        }
        if (rb2.isChecked()){
            output = ((inputValue*9)/5)+32;
            text.setText(String.valueOf(output)); //float 값을 문자열로 변경

        }
    }
}
```

실행화면

섭씨 35도 입력후 화씨 변환

<img src="https://user-images.githubusercontent.com/69203345/135760760-ce328017-b251-4484-a7d3-0cce6e54ee7a.png" alt="image" style="zoom:80%;" />

다시 섭씨 변환

<img src="https://user-images.githubusercontent.com/69203345/135760787-f1dbace0-7dde-4f28-89a2-566383cfd3cc.png" alt="image" style="zoom:80%;" />
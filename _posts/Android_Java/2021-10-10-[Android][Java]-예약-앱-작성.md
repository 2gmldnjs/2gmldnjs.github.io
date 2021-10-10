---
title:  "[Android][Java] 예약 앱 작성"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-10-10 23:06:27
---

# 예약 앱 작성

RelativeLaytout 사용

layout_centerHorizonal

layout_below 를 이용해서 위치조절



activity_main.xml 디자인

timepicker를 팔렛트에서 찾을 수없다면 직접 코드로 쳐주면 나온다

버튼에 onClick 속성 설정해주기

<img src="https://user-images.githubusercontent.com/69203345/136698022-25f3f55d-3c5d-429d-b0d9-c29b49292008.png" alt="image" style="zoom:80%;" />

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    //전역변수를 사용,/모든 함수에서 이 내용을 알게하기 위해 사용
    private TimePicker timePicker; //private : 현재 클래스에서만 사용
    private TextView time;
    private Calendar calendar; //현재 시간을 받기 위해 만듦
    private String format = "";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        timePicker = (TimePicker) findViewById(R.id.TimePicker);
        time = (TextView) findViewById(R.id.textView2);
        calendar = Calendar.getInstance();

        int hour = calendar.get(Calendar.HOUR_OF_DAY);
        int min =calendar.get(Calendar.MINUTE);
        showTime(hour,min);

    }
    @RequiresApi(api = Build.VERSION_CODES.M)
    public void displayTime(View v){
        int hour = timePicker.getHour();
        int min = timePicker.getMinute();
        showTime(hour,min);
    }

    public void showTime(int hour, int min) {
        if (hour == 0) {
            hour += 12;
            format = "AM";
        } else if (hour == 12) {
            format = "PM";
        } else if (hour > 12) {
            hour -= 12;
            format = "PM";
        } else {
            format = "AM";
        }
        time.setText(new StringBuilder().append(hour).append(":").append(min).append(" ").append(format));
    }
}
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/136698947-c067b0d2-d903-49f8-9880-143206e34922.png" alt="image" style="zoom:80%;" />




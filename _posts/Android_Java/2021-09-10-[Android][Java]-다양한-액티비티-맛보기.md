---
title:  "[Android][Java] 다양한 액티비티 맛보기"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-09-10 21:55:44 

---

# 다양한 Activity 맛보기

## Basic Activity

프로젝트 만들기 → basic activity 으로 만들기

res폴더(리소스 폴더)에 보면 그동안 해왔던 액티비티와는 다르게

xml파일이 여러개인것을 볼 수 있음, 하나하나 파해칠 시간임



activity_main.xml 화면

![image](https://user-images.githubusercontent.com/69203345/132822480-29521d77-7ca5-4b09-b927-11abbba24c86.png)

activity_main.xml의 component Tree 상태

![image](https://user-images.githubusercontent.com/69203345/132822633-cfa0544a-c130-455e-87be-d08173acc48e.png)

! 는 일단 무시 지금은 상관없음

어머나! @layout/conte... 이건 뭔가요????? → 아래에 설명 할 겁니다



contant_main.xml

![image](https://user-images.githubusercontent.com/69203345/132823225-175b2d37-d634-417d-b825-4eba53b7a21d.png)

contant_main.xmldml component Tree 상태

![image](https://user-images.githubusercontent.com/69203345/132823362-d949a053-2679-45a1-92da-e8ff57c7ebc5.png)

fragment_first.xml

![image](https://user-images.githubusercontent.com/69203345/132823569-70176581-a8b7-4436-a074-fd7a607f502c.png)

fragment_first.xml의 component Tree 

![image](https://user-images.githubusercontent.com/69203345/132823703-244d6c5c-f110-49c5-9082-59bef7b18568.png)

길어서 안보이지만

@string/hello_first_fragment

@string/next 라고 적혀있음



아니 그래서 @string/어쩌고... 가 뭔데?

그건 vales 폴더 아래 strings.xml을 보면 알지!

value 폴더 안의 strings.xml 내용

```xml
<resources>
    <string name="app_name">week2-basic-activity</string>
    <string name="action_settings">Settings</string>
    <!-- Strings used for fragments for navigation -->
    <string name="first_fragment_label">First Fragment</string>
    <string name="second_fragment_label">Second Fragment</string>
    <string name="next">Next</string>
    <string name="previous">Previous</string>

    <string name="hello_first_fragment">Hello first fragment</string>
    <string name="hello_second_fragment">Hello second fragment. Arg: %1$s</string>
</resources>
```

내용을 보면 

hello_first_fragment를 볼 수 있음

고로 strings.xml에 있는 name을 사용해서 textview_first 의 text 속성 를 바꾼다는것

버튼도 똑같음 

위에 activity_main.xml에서본 것도 같은 방식 이나 단, text속성이 아닌

layout 속성에 @layout/content_main을 사용한것

MainActivity.java의 내용

```java
package com.example.week2_basic_activity;

import android.os.Bundle;

import com.google.android.material.snackbar.Snackbar;

import androidx.appcompat.app.AppCompatActivity;

import android.view.View;

import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.AppBarConfiguration;
import androidx.navigation.ui.NavigationUI;

import com.example.week2_basic_activity.databinding.ActivityMainBinding;

import android.view.Menu;
import android.view.MenuItem;

public class MainActivity extends AppCompatActivity {

    private AppBarConfiguration appBarConfiguration;
    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        setSupportActionBar(binding.toolbar);

        NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment_content_main);
        appBarConfiguration = new AppBarConfiguration.Builder(navController.getGraph()).build();
        NavigationUI.setupActionBarWithNavController(this, navController, appBarConfiguration);

        binding.fab.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();
            }
        });
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.menu_main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }

    @Override
    public boolean onSupportNavigateUp() {
        NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment_content_main);
        return NavigationUI.navigateUp(navController, appBarConfiguration)
                || super.onSupportNavigateUp();
    }
}
```

emptyActivity에 비해서 상당히 많은 양임

```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    // Inflate the menu; this adds items to the action bar if it is present.
    getMenuInflater().inflate(R.menu.menu_main, menu);
    return true;
}
```

옵션메뉴, 옆에 폴더들에서 menu폴더를 볼 수 있다

<img src="https://user-images.githubusercontent.com/69203345/132825644-273669ba-4716-4edf-baa4-1e85d19b8a6f.png" alt="image" style="zoom:80%;" />

내요을 이렇다

해당되는 메뉴 아이템중에 특정한 아이템이 선택 됐을때 내용을 처리하는함수

```java
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
```

실행화면중

<img src="https://user-images.githubusercontent.com/69203345/132826692-6e8418d2-5f17-4bf5-aba4-3a40f1f64122.png" alt="image" style="zoom:80%;" />

<img src="https://user-images.githubusercontent.com/69203345/132826807-d7a6f5af-eae6-4062-b153-c10b2e00891a.png" alt="image" style="zoom:80%;" />

## Bottom Navigation Activity

activity_main.xml

![image](https://user-images.githubusercontent.com/69203345/132828812-485fdefb-073d-40e1-b54c-d3dbad3d62a4.png)

Component Tree

![image](https://user-images.githubusercontent.com/69203345/132828924-0c62deca-817f-44d6-accf-a5f907d5478b.png)

여기선 안보이지만

nav_view의 menu 속성에는 @menu/bottom_nav_menu 이라고 돼있다

menu 폴더 밑에 bottom_nav_menu.xml

<img src="https://user-images.githubusercontent.com/69203345/132829818-54691547-0c78-4f80-a5b8-f2c3c79a817d.png" alt="image" style="zoom:67%;" />

mobile_navigation.xml

![image](https://user-images.githubusercontent.com/69203345/132830271-3e16951c-c091-43de-b6d0-418cd48a444b.png)

home

dashboard

notification

에 관련된 화면들이 디자인 돼있음

hosts 는 activity_main(nav_host_fragment_activity_main) 인데

activity_main.xml의 nav_host_fragment와 연관돼 있다는 정도만 알면됨

MainActivity.java

```java
package com.example.week2bottomnavigatoinactivity;

import android.os.Bundle;

import com.google.android.material.bottomnavigation.BottomNavigationView;

import androidx.appcompat.app.AppCompatActivity;
import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.AppBarConfiguration;
import androidx.navigation.ui.NavigationUI;

import com.example.week2bottomnavigatoinactivity.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {

    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        BottomNavigationView navView = findViewById(R.id.nav_view);
        // Passing each menu ID as a set of Ids because each
        // menu should be considered as top level destinations.
        AppBarConfiguration appBarConfiguration = new AppBarConfiguration.Builder(
                R.id.navigation_home, R.id.navigation_dashboard, R.id.navigation_notifications)
                .build();
        NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment_activity_main);
        NavigationUI.setupActionBarWithNavController(this, navController, appBarConfiguration);
        NavigationUI.setupWithNavController(binding.navView, navController);
    }

}
```

한번 쭉 읽어보면 될듯

실행화면

<img src="https://user-images.githubusercontent.com/69203345/132831853-842b7570-ca9d-49c1-a777-bf5500e03ea9.png" alt="image" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/69203345/132831907-79a1adf4-1339-4a41-82ee-a5ef4bb4e22e.png" alt="image" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/69203345/132832001-3b30444d-37be-450c-be0f-d4dcbe62ed6d.png" alt="image" style="zoom:67%;" />

## Fragment View model

main_fragment.xml

![image](https://user-images.githubusercontent.com/69203345/132834264-f95500c3-4612-4e6d-aea6-bbc077a10344.png)

fragment view model은 기본적인 emply activity와 별차이가 없음

## Fullscreen Activity

activity_fullscreen.xml

![image](https://user-images.githubusercontent.com/69203345/132834946-f1dd359d-efbe-4f82-b2e9-62497b5a7c93.png)

FullscreenActivity.java를 살펴보기엔 너무 많아서 훑어만 보고 바로 실행

<img src="https://user-images.githubusercontent.com/69203345/132835306-66f4848d-b64b-4925-8f24-e6ad54d304e2.png" alt="image" style="zoom:67%;" />

한번 터치 하면

<img src="https://user-images.githubusercontent.com/69203345/132835363-f6c075ec-86ec-48e4-850e-3eea6f31ae8b.png" alt="image" style="zoom: 67%;" />

이렇게 바뀜

![image](https://user-images.githubusercontent.com/69203345/132835675-c58ab232-2170-478a-860e-d9b2ce85f0b0.png)

FrameLayout을 2개 사용

FrameLayout이란 같은영역에 다른것들을 겹쳐서 볼수 있게 하는 레이아웃

fullscreen_content를 보면 text속성이 @string/dummy_content라고 돼있다

앞에 했던것과 같은 방식이니 설명은 패스한다

fullscreen_content_controls - LinearLayout (horizontal)사용

## Master Detail Flow(Primary Detail Flow)

activity_item_detail.xml

![image](https://user-images.githubusercontent.com/69203345/132848578-0c8cad7d-4960-4f28-996e-766d49b15656.png)

fragment_item_list.xml

![image](https://user-images.githubusercontent.com/69203345/132848696-914acbdf-9e17-448f-9290-14b7810f568b.png)

fragment_item_list의 Component Tree

![image](https://user-images.githubusercontent.com/69203345/132849645-41dd2310-379b-40ca-9f79-f4a93fe8f0ec.png)

실행화면

키면 바로 보이는 화면임

![image](https://user-images.githubusercontent.com/69203345/132852401-ce3bade9-9598-46f6-9f5f-547e944ff278.png)

아이템 리스트를 눌렀을때 나오는 화면

![image](https://user-images.githubusercontent.com/69203345/132852463-e1332b38-87e9-41ac-8308-37f1f8ee76f1.png)

내일 더 추가 할 예정입니니ㅣㅣㅣㅣ당ㅇㅇ
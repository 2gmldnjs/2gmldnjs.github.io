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

activity_item_detail의 Component Tree

![image](https://user-images.githubusercontent.com/69203345/132939088-6da360bb-a657-473f-a589-4a351ceda3df.png)

nav_host_frament_item_detail 의 layout속성을 보면

@layout/fragment_item_detail 로 되어있다

살펴보자

fragment_item_detail.xml

<img src="https://user-images.githubusercontent.com/69203345/132939155-aa6a5dea-12ea-4c63-a3d5-d12ba3453862.png" alt="image" style="zoom: 67%;" />

점선으로 돼있는 부분은 화면을 내렸을때 보여줄 부분이다 내용은 아무것도 없다

fragment_item_list.xml

![image](https://user-images.githubusercontent.com/69203345/132848696-914acbdf-9e17-448f-9290-14b7810f568b.png)

fragment_item_list의 Component Tree

![image](https://user-images.githubusercontent.com/69203345/132849645-41dd2310-379b-40ca-9f79-f4a93fe8f0ec.png)

itemDetailHostActivity.java

```java
package com.example.week2_primary_detail_flow;

import android.os.Bundle;

import androidx.appcompat.app.AppCompatActivity;
import androidx.navigation.fragment.NavHostFragment;
import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.AppBarConfiguration;
import androidx.navigation.ui.NavigationUI;

import com.example.week2_primary_detail_flow.databinding.ActivityItemDetailBinding;

public class ItemDetailHostActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        ActivityItemDetailBinding binding = ActivityItemDetailBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        NavHostFragment navHostFragment = (NavHostFragment) getSupportFragmentManager()
                .findFragmentById(R.id.nav_host_fragment_item_detail);
        NavController navController = navHostFragment.getNavController();
        AppBarConfiguration appBarConfiguration = new AppBarConfiguration.
                Builder(navController.getGraph())
                .build();

        NavigationUI.setupActionBarWithNavController(this, navController, appBarConfiguration);
    }

    @Override
    public boolean onSupportNavigateUp() {
        NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment_item_detail);
        return navController.navigateUp() || super.onSupportNavigateUp();
    }
}
```

실행화면

키면 바로 보이는 화면임

![image](https://user-images.githubusercontent.com/69203345/132852401-ce3bade9-9598-46f6-9f5f-547e944ff278.png)

itemListFragment.java

```java
package com.example.week2_primary_detail_flow;

import android.content.ClipData;
import android.content.ClipDescription;
import android.os.Build;
import android.os.Bundle;

import androidx.core.view.ViewCompat;
import androidx.fragment.app.Fragment;
import androidx.navigation.Navigation;
import androidx.recyclerview.widget.RecyclerView;

import android.view.KeyEvent;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;
import android.widget.Toast;

import com.example.week2_primary_detail_flow.databinding.FragmentItemListBinding;
import com.example.week2_primary_detail_flow.databinding.ItemListContentBinding;

import com.example.week2_primary_detail_flow.placeholder.PlaceholderContent;

import java.util.List;

/**
 * A fragment representing a list of Items. This fragment
 * has different presentations for handset and larger screen devices. On
 * handsets, the fragment presents a list of items, which when touched,
 * lead to a {@link ItemDetailFragment} representing
 * item details. On larger screens, the Navigation controller presents the list of items and
 * item details side-by-side using two vertical panes.
 */
public class ItemListFragment extends Fragment {

    /**
     * Method to intercept global key events in the
     * item list fragment to trigger keyboard shortcuts
     * Currently provides a toast when Ctrl + Z and Ctrl + F
     * are triggered
     */
    ViewCompat.OnUnhandledKeyEventListenerCompat unhandledKeyEventListenerCompat = (v, event) -> {
        if (event.getKeyCode() == KeyEvent.KEYCODE_Z && event.isCtrlPressed()) {
            Toast.makeText(
                    v.getContext(),
                    "Undo (Ctrl + Z) shortcut triggered",
                    Toast.LENGTH_LONG
            ).show();
            return true;
        } else if (event.getKeyCode() == KeyEvent.KEYCODE_F && event.isCtrlPressed()) {
            Toast.makeText(
                    v.getContext(),
                    "Find (Ctrl + F) shortcut triggered",
                    Toast.LENGTH_LONG
            ).show();
            return true;
        }
        return false;
    };

    private FragmentItemListBinding binding;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {

        binding = FragmentItemListBinding.inflate(inflater, container, false);
        return binding.getRoot();

    }

    @Override
    public void onViewCreated(View view, Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        ViewCompat.addOnUnhandledKeyEventListener(view, unhandledKeyEventListenerCompat);

        RecyclerView recyclerView = binding.itemList;

        // Leaving this not using view binding as it relies on if the view is visible the current
        // layout configuration (layout, layout-sw600dp)
        View itemDetailFragmentContainer = view.findViewById(R.id.item_detail_nav_container);

        /* Click Listener to trigger navigation based on if you have
         * a single pane layout or two pane layout
         */
        View.OnClickListener onClickListener = itemView -> {
            PlaceholderContent.PlaceholderItem item =
                    (PlaceholderContent.PlaceholderItem) itemView.getTag();
            Bundle arguments = new Bundle();
            arguments.putString(ItemDetailFragment.ARG_ITEM_ID, item.id);
            if (itemDetailFragmentContainer != null) {
                Navigation.findNavController(itemDetailFragmentContainer)
                        .navigate(R.id.fragment_item_detail, arguments);
            } else {
                Navigation.findNavController(itemView).navigate(R.id.show_item_detail, arguments);
            }
        };

        /*
         * Context click listener to handle Right click events
         * from mice and trackpad input to provide a more native
         * experience on larger screen devices
         */
        View.OnContextClickListener onContextClickListener = itemView -> {
            PlaceholderContent.PlaceholderItem item =
                    (PlaceholderContent.PlaceholderItem) itemView.getTag();
            Toast.makeText(
                    itemView.getContext(),
                    "Context click of item " + item.id,
                    Toast.LENGTH_LONG
            ).show();
            return true;
        };

        setupRecyclerView(recyclerView, onClickListener, onContextClickListener);
    }

    private void setupRecyclerView(
            RecyclerView recyclerView,
            View.OnClickListener onClickListener,
            View.OnContextClickListener onContextClickListener
    ) {

        recyclerView.setAdapter(new SimpleItemRecyclerViewAdapter(
                PlaceholderContent.ITEMS,
                onClickListener,
                onContextClickListener
        ));
    }

    @Override
    public void onDestroyView() {
        super.onDestroyView();
        binding = null;
    }

    public static class SimpleItemRecyclerViewAdapter
            extends RecyclerView.Adapter<SimpleItemRecyclerViewAdapter.ViewHolder> {

        private final List<PlaceholderContent.PlaceholderItem> mValues;
        private final View.OnClickListener mOnClickListener;
        private final View.OnContextClickListener mOnContextClickListener;

        SimpleItemRecyclerViewAdapter(List<PlaceholderContent.PlaceholderItem> items,
                                      View.OnClickListener onClickListener,
                                      View.OnContextClickListener onContextClickListener) {
            mValues = items;
            mOnClickListener = onClickListener;
            mOnContextClickListener = onContextClickListener;
        }

        @Override
        public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {

            ItemListContentBinding binding =
                    ItemListContentBinding.inflate(LayoutInflater.from(parent.getContext()), parent, false);
            return new ViewHolder(binding);

        }

        @Override
        public void onBindViewHolder(final ViewHolder holder, int position) {
            holder.mIdView.setText(mValues.get(position).id);
            holder.mContentView.setText(mValues.get(position).content);

            holder.itemView.setTag(mValues.get(position));
            holder.itemView.setOnClickListener(mOnClickListener);
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                holder.itemView.setOnContextClickListener(mOnContextClickListener);
            }
            holder.itemView.setOnLongClickListener(v -> {
                // Setting the item id as the clip data so that the drop target is able to
                // identify the id of the content
                ClipData.Item clipItem = new ClipData.Item(mValues.get(position).id);
                ClipData dragData = new ClipData(
                        ((PlaceholderContent.PlaceholderItem) v.getTag()).content,
                        new String[]{ClipDescription.MIMETYPE_TEXT_PLAIN},
                        clipItem
                );

                if (Build.VERSION.SDK_INT >= 24) {
                    v.startDragAndDrop(
                            dragData,
                            new View.DragShadowBuilder(v),
                            null,
                            0
                    );
                } else {
                    v.startDrag(
                            dragData,
                            new View.DragShadowBuilder(v),
                            null,
                            0
                    );
                }
                return true;
            });
        }

        @Override
        public int getItemCount() {
            return mValues.size();
        }

        class ViewHolder extends RecyclerView.ViewHolder {
            final TextView mIdView;
            final TextView mContentView;

            ViewHolder(ItemListContentBinding binding) {
                super(binding.getRoot());
                mIdView = binding.idText;
                mContentView = binding.content;
            }

        }
    }
}
```

아이템 리스트를 눌렀을때 나오는 화면

![image](https://user-images.githubusercontent.com/69203345/132852463-e1332b38-87e9-41ac-8308-37f1f8ee76f1.png)

itemDetailFragment.java

```java
package com.example.week2_primary_detail_flow;

import android.content.ClipData;
import android.os.Bundle;
import android.view.DragEvent;

import androidx.fragment.app.Fragment;

import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;

import com.google.android.material.appbar.CollapsingToolbarLayout;
import com.example.week2_primary_detail_flow.placeholder.PlaceholderContent;
import com.example.week2_primary_detail_flow.databinding.FragmentItemDetailBinding;

/**
 * A fragment representing a single Item detail screen.
 * This fragment is either contained in a {@link ItemListFragment}
 * in two-pane mode (on larger screen devices) or self-contained
 * on handsets.
 */
public class ItemDetailFragment extends Fragment {

    /**
     * The fragment argument representing the item ID that this fragment
     * represents.
     */
    public static final String ARG_ITEM_ID = "item_id";

    /**
     * The placeholder content this fragment is presenting.
     */
    private PlaceholderContent.PlaceholderItem mItem;
    private CollapsingToolbarLayout mToolbarLayout;
    private TextView mTextView;

    private final View.OnDragListener dragListener = (v, event) -> {
        if (event.getAction() == DragEvent.ACTION_DROP) {
            ClipData.Item clipDataItem = event.getClipData().getItemAt(0);
            mItem = PlaceholderContent.ITEM_MAP.get(clipDataItem.getText().toString());
            updateContent();
        }
        return true;
    };
    private FragmentItemDetailBinding binding;

    /**
     * Mandatory empty constructor for the fragment manager to instantiate the
     * fragment (e.g. upon screen orientation changes).
     */
    public ItemDetailFragment() {
    }

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        if (getArguments().containsKey(ARG_ITEM_ID)) {
            // Load the placeholder content specified by the fragment
            // arguments. In a real-world scenario, use a Loader
            // to load content from a content provider.
            mItem = PlaceholderContent.ITEM_MAP.get(getArguments().getString(ARG_ITEM_ID));
        }
    }

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {

        binding = FragmentItemDetailBinding.inflate(inflater, container, false);
        View rootView = binding.getRoot();

        mToolbarLayout = rootView.findViewById(R.id.toolbar_layout);
        mTextView = binding.itemDetail;

        // Show the placeholder content as text in a TextView & in the toolbar if available.
        updateContent();
        rootView.setOnDragListener(dragListener);
        return rootView;
    }

    @Override
    public void onDestroyView() {
        super.onDestroyView();
        binding = null;
    }

    private void updateContent() {
        if (mItem != null) {
            mTextView.setText(mItem.details);
            if (mToolbarLayout != null) {
                mToolbarLayout.setTitle(mItem.content);
            }
        }
    }
}
```

PlaceholderContent.java 파일

```java
package com.example.week2_primary_detail_flow.placeholder;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * Helper class for providing sample content for user interfaces created by
 * Android template wizards.
 * <p>
 * TODO: Replace all uses of this class before publishing your app.
 */
public class PlaceholderContent {

    /**
     * An array of sample (placeholder) items.
     */
    public static final List<PlaceholderItem> ITEMS = new ArrayList<PlaceholderItem>();

    /**
     * A map of sample (placeholder) items, by ID.
     */
    public static final Map<String, PlaceholderItem> ITEM_MAP = new HashMap<String, PlaceholderItem>();

    private static final int COUNT = 25;

    static {
        // Add some sample items.
        for (int i = 1; i <= COUNT; i++) {
            addItem(createPlaceholderItem(i));
        }
    }

    private static void addItem(PlaceholderItem item) {
        ITEMS.add(item);
        ITEM_MAP.put(item.id, item);
    }

    private static PlaceholderItem createPlaceholderItem(int position) {
        return new PlaceholderItem(String.valueOf(position), "Item " + position, makeDetails(position));
    }

    private static String makeDetails(int position) {
        StringBuilder builder = new StringBuilder();
        builder.append("Details about Item: ").append(position);
        for (int i = 0; i < position; i++) {
            builder.append("\nMore details information here.");
        }
        return builder.toString();
    }

    /**
     * A placeholder item representing a piece of content.
     */
    public static class PlaceholderItem {
        public final String id;
        public final String content;
        public final String details;

        public PlaceholderItem(String id, String content, String details) {
            this.id = id;
            this.content = content;
            this.details = details;
        }

        @Override
        public String toString() {
            return content;
        }
    }
}
```

여기서 More details ~~~를 바꿀수 있다

## Navigation Drawer Activity

contain_main.xml 이다

<img src="https://user-images.githubusercontent.com/69203345/132941454-bfa6038b-0a9a-44c7-981d-1334d8d287f1.png" alt="image" style="zoom:80%;" />

component Tree에 보면 nav_host_fragment_contenet_main이 @navigation/mobile_navigation와 연결 되있는것을 볼수 있다

mobile_navigation.xml

![image](https://user-images.githubusercontent.com/69203345/132941672-00523445-9b34-4898-9c53-02c963b28ee6.png)

nav_home, nav_gallay 등을 누르면 

fragment_gallery등 관련 xml로 이동함

fragment_gallery.xml

<img src="https://user-images.githubusercontent.com/69203345/132941720-068d0610-74cb-4880-a1d7-afec165da183.png" alt="image" style="zoom:80%;" />

다른 home, sildeshow 에서도 같은 디자인 이기때문에 사진은 생략하겠다

activity_main.xml

![image](https://user-images.githubusercontent.com/69203345/132942219-e5f8da98-fcec-44e2-bdc9-a2454e5f9133.png)

MainActivity.java의 내용

```java
package com.example.week2_navigation_drawer_activity;

import android.os.Bundle;
import android.view.View;
import android.view.Menu;

import com.google.android.material.snackbar.Snackbar;
import com.google.android.material.navigation.NavigationView;

import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.AppBarConfiguration;
import androidx.navigation.ui.NavigationUI;
import androidx.drawerlayout.widget.DrawerLayout;
import androidx.appcompat.app.AppCompatActivity;

import com.example.week2_navigation_drawer_activity.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {

    private AppBarConfiguration mAppBarConfiguration;
    private ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        setSupportActionBar(binding.appBarMain.toolbar);
        binding.appBarMain.fab.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();
            }
        });
        DrawerLayout drawer = binding.drawerLayout;
        NavigationView navigationView = binding.navView;
        // Passing each menu ID as a set of Ids because each
        // menu should be considered as top level destinations.
        mAppBarConfiguration = new AppBarConfiguration.Builder(
                R.id.nav_home, R.id.nav_gallery, R.id.nav_slideshow)
                .setOpenableLayout(drawer)
                .build();
        NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment_content_main);
        NavigationUI.setupActionBarWithNavController(this, navController, mAppBarConfiguration);
        NavigationUI.setupWithNavController(navigationView, navController);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }

    @Override
    public boolean onSupportNavigateUp() {
        NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment_content_main);
        return NavigationUI.navigateUp(navController, mAppBarConfiguration)
                || super.onSupportNavigateUp();
    }
}
```

한번 쓱 보고 가자

실행화면

<img src="https://user-images.githubusercontent.com/69203345/132941813-c51bd607-94e3-4b8a-ae8b-ec8957b0248e.png" alt="image" style="zoom:67%;" />

아까는 안보였는데 텍스트? 가 있다

텍스트속성을 바꿨는데도 적용이 안되는것을 봐선 어디선가 따로 뭘 해줘야 하나보다

GalleryViewModel.java 를 찾으면 바꿀수 있다

```java
package com.example.week2_navigation_drawer_activity.ui.gallery;

import androidx.lifecycle.LiveData;
import androidx.lifecycle.MutableLiveData;
import androidx.lifecycle.ViewModel;

public class GalleryViewModel extends ViewModel {

    private MutableLiveData<String> mText;

    public GalleryViewModel() {
        mText = new MutableLiveData<>();
        mText.setValue("This is gallery fragment");
    }

    public LiveData<String> getText() {
        return mText;
    }
}
```

다른 HomeViewModel, SlideshowViewModel을 찾으면 똑같이 바꿀수 있다

<img src="https://user-images.githubusercontent.com/69203345/132941939-94954c1b-952e-486a-89d8-a8fc029d4c91.png" alt="image" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/69203345/132941951-df692a93-d25a-43fc-95c2-638e6620397a.png" alt="image" style="zoom:67%;" />

달라보이는 건 없다

<img src="https://user-images.githubusercontent.com/69203345/132942189-c1373769-548e-4964-86bb-2f4bcb7236f7.png" alt="image" style="zoom:67%;" />

## Scrolling Activity

content_scrolling.xml

![image](https://user-images.githubusercontent.com/69203345/132945050-3112bf3c-e185-4eae-b344-d2593ba006f9.png)

오른쪽 블루프린트에 보이지만 

매우 많은 양의 내용을 볼수있다

이 내용은 

strings.xml에서 볼 수 있다

실행화면

<img src="https://user-images.githubusercontent.com/69203345/132945121-d90627f4-5bba-409a-90d8-8202325c91ae.png" alt="image" style="zoom:80%;" />

## Tabbed Activity

activity_main.xml

![ta-1](https://user-images.githubusercontent.com/69203345/132946156-56486ab8-7ebc-4b9b-90c3-11b06bbba54a.PNG)

fragment_main.xml

![ta-2](https://user-images.githubusercontent.com/69203345/132946170-70507172-8789-431a-9f09-164a78c8ad3b.PNG)

보이는 표시는 section_label이다, 보이는거 말고는 없다

실행화면

![ta-3](https://user-images.githubusercontent.com/69203345/132946174-7f293497-6585-4dd7-9ef6-1098749553b3.PNG)

PageViewModel.java

PlaceholderFragment.java

SectionPagerAdapter.java

를 보면 자세한 정보들을 볼수 있다
# AndroidTips
### 非root Android手机上无法使用ViewHierachy
####使用ViewServer

1. 在root build.gradle中添加

    ```
    allprojects {
        repositories {
            ...
            maven { url 'https://jitpack.io' }
        }
    }
    ```

2. 在具体的module添加依赖
    ```
    compile 'com.github.romainguy:ViewServer:017c01cd512cac3ec054d9eee05fc48c5a9d2de'
    ```
3. 在Activity中添加代码
```
public class MyActivity extends Activity {
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // Set content view, etc.
        ViewServer.get(this).addWindow(this);
    }

    public void onDestroy() {
        super.onDestroy();
        ViewServer.get(this).removeWindow(this);
    }

    public void onResume() {
        super.onResume();
        ViewServer.get(this).setFocusedWindow(this);
    }
}
```

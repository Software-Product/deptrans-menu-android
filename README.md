## Интеграция библиотеки "Единое Транспортное Меню" в проект:

- Скопируйте **lib-etp-menu-1.0.6.aar** файл библиотеки в папку **aars** Вашего проекта (или любую другую).
- Подключите **aar** библиотеку и необходимые библиотеки в файле **build.gradle**:

```gradle
repositories {
    flatDir {
        dirs 'aars'
    }
}

dependencies {
    ...
    compile(name:'lib-etp-menu-1.0.6', ext:'aar')
    
    compile 'com.squareup.okhttp:okhttp:2.2.0'
    compile 'com.squareup.picasso:picasso:2.5.0'
    ...
}
```

- Добавьте необходимые разрешения в **AndroidManifest.xml** файл:

```xml
    ...
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    ...
```

- Добавьте инициализацию меню в метод **onCreate** после вызова **setContentView**:

```java
    private EtpMenu mEtpMenu;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main_layout);

        mEtpMenu = new EtpMenu(this);

        ...
    }
```

- Теперь по нажатию на необходимую кнопку запустите анимацию открытия меню:

```java
        ...
        findViewById(R.id.btn).setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mEtpMenu.showMenu();
            }
        });
        ...
```

- Если вы используете темный фон для Toolbar (ActionBar), Вы можете использовать стандартную иконку и разметку с баджиком из библиотеки, для этого добавьте item в нужное меню:

```xml
    ...
    <item
        android:id="@+id/action_etp_menu"
        android:title="ETP Menu"
        app:actionLayout="@layout/menu_item_etp"
        app:showAsAction="always"
        tools:ignore="HardcodedText" />
    ...
```

- В методе **onCreateOptionsMenu** добавьте инициализацию пункта меню:

```java
    ...
    mEtpMenu.initOptionsMenuItem(menu.findItem(R.id.action_etp_menu), R.drawable.bg_menu_item);
    ...

```
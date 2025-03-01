# مقدمه‌ای بر Jetpack Compose

![image](https://github.com/user-attachments/assets/4dd81641-7056-4b82-aa47-ec0d0c865e7d)
![image](https://github.com/user-attachments/assets/1c538395-632e-4ee7-a64c-769cdf9fa397)




## مقدمه
Jetpack Compose فریمورک جدید گوگل برای ساخت رابط کاربری در اندروید است. این فریمورک بر پایه‌ی کاتلین ساخته شده و از برنامه‌نویسی دکلراتیو پشتیبانی می‌کند. در این جزوه، نحوه‌ی شروع کار با Compose و ایجاد اولین کامپوننت‌های UI را بررسی می‌کنیم.

---

## راه‌اندازی پروژه‌ی Jetpack Compose
برای شروع، باید یک پروژه جدید با پشتیبانی از Jetpack Compose ایجاد کنیم:
1. **ایجاد پروژه جدید در Android Studio**
   - Android Studio را باز کنید و گزینه‌ی "New Project" را انتخاب کنید.
   - الگوی **Empty Compose Activity** را انتخاب کنید.
   - تنظیمات اولیه را انجام دهید و روی "Finish" کلیک کنید.
2. **بررسی build.gradle.kts**
   - اطمینان حاصل کنید که Jetpack Compose فعال شده است:
     ```kotlin
     android {
         composeOptions {
             kotlinCompilerExtensionVersion = "latest_version"
         }
     }
     dependencies {
         implementation("androidx.activity:activity-compose:latest_version")
         implementation("androidx.compose.ui:ui:latest_version")
         implementation("androidx.compose.material:material:latest_version")
     }
     ```

---

## اولین کامپوننت در Jetpack Compose
Jetpack Compose از **کامپوزابل‌ها (Composables)** برای ساخت UI استفاده می‌کند. یک Composable تابعی است که رابط کاربری تولید می‌کند.

### نمایش متن ساده
```kotlin
@Composable
fun Greeting() {
    Text(text = "سلام، به Jetpack Compose خوش آمدید!")
}
```

برای نمایش این کامپوننت در صفحه، از تابع `setContent` در `MainActivity` استفاده کنید:

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Greeting()
        }
    }
}
```

---

## ایجاد دکمه در Jetpack Compose
می‌توان با استفاده از `Button` یک دکمه در UI اضافه کرد:

```kotlin
@Composable
fun MyButton() {
    Button(onClick = {
        Log.d("Compose", "دکمه کلیک شد!")
    }) {
        Text(text = "کلیک کن!")
    }
}
```

---

## نمایش Toast در Jetpack Compose
برای نمایش پیام `Toast` هنگام کلیک روی دکمه:

```kotlin
@Composable
fun MyToastButton(context: Context) {
    Button(onClick = {
        Toast.makeText(context, "دکمه کلیک شد!", Toast.LENGTH_SHORT).show()
    }) {
        Text(text = "نمایش Toast")
    }
}
```

**نحوه‌ی استفاده در Activity:**
```kotlin
setContent {
    MyToastButton(context = this)
}
```

---

## Modifier در Jetpack Compose چیست؟

`Modifier` در Jetpack Compose ابزاری است که برای تغییر و سفارشی‌سازی ظاهر و رفتار کامپوننت‌های UI استفاده می‌شود. به کمک `Modifier` می‌توان ویژگی‌هایی مانند **اندازه، فاصله، رنگ، انیمیشن، و تعاملات کاربری** را کنترل کرد.

### مثال استفاده از `Modifier`

```kotlin
@Composable
fun CustomText() {
    Text(
        text = "متن سفارشی",
        fontSize = 20.sp,
        fontWeight = FontWeight.Bold,
        color = Color.Blue,
        modifier = Modifier.padding(16.dp)
    )
}
```

### ترکیب چند `Modifier`

می‌توان چندین `Modifier` را به یک کامپوننت اعمال کرد:

```kotlin
@Composable
fun StyledButton() {
    Button(
        onClick = {},
        modifier = Modifier
            .padding(16.dp)
            .size(150.dp, 50.dp)
    ) {
        Text(text = "دکمه استایل‌شده")
    }
}
```

---

## دکمه‌ای که فقط لاگ می‌اندازد یا چیزی پرینت می‌کند
```kotlin
@Composable
fun LogButton() {
    Button(onClick = {
        println("دکمه کلیک شد!")
    }) {
        Text(text = "پرینت در Log")
    }
}
```

---

## تمرین‌ها

### تمرین ۱: نمایش لیستی از آیتم‌ها در Jetpack Compose
**سوال:**
یک لیست از نام‌ها را در UI نمایش دهید.

**پاسخ:**
```kotlin
@Composable
fun NameList() {
    val names = listOf("علی", "زهرا", "رضا", "مریم")
    Column(modifier = Modifier.padding(16.dp)) {
        names.forEach { name ->
            Text(text = name, fontSize = 18.sp, modifier = Modifier.padding(4.dp))
        }
    }
}
```

### تمرین ۲: استفاده از Modifier برای استایل دادن به یک دکمه
**سوال:**
یک دکمه طراحی کنید که دارای پس‌زمینه قرمز و متن سفید باشد.

**پاسخ:**
```kotlin
@Composable
fun StyledRedButton() {
    Button(
        onClick = {},
        modifier = Modifier.padding(16.dp),
        colors = ButtonDefaults.buttonColors(backgroundColor = Color.Red)
    ) {
        Text(text = "دکمه قرمز", color = Color.White)
    }
}
```

---

## نتیجه‌گیری
در این جلسه، با مقدمات Jetpack Compose آشنا شدیم. یاد گرفتیم که چگونه پروژه را راه‌اندازی کنیم، متن و دکمه ایجاد کنیم و رفتارهای مختلف مانند ثبت لاگ و نمایش Toast را پیاده‌سازی کنیم. همچنین با مفهوم `Modifier` آشنا شدیم که ابزار قدرتمندی برای سفارشی‌سازی UI در Jetpack Compose است. در کنار آن، چند تمرین کاربردی را حل کردیم. در جلسات بعدی، به مباحث پیشرفته‌تر مانند مدیریت وضعیت (State) و لیست‌های پویا می‌پردازیم.


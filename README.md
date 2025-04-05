# مقدمه‌ای بر Jetpack Compose

![image](https://github.com/user-attachments/assets/4dd81641-7056-4b82-aa47-ec0d0c865e7d)
![image](https://github.com/user-attachments/assets/1c538395-632e-4ee7-a64c-769cdf9fa397)



# آموزش کامل طراحی رابط کاربری در اندروید با Jetpack Compose

---

در این آموزش قدم‌به‌قدم با مفاهیم اولیه‌ی طراحی رابط کاربری در Jetpack Compose آشنا می‌شوید. این آموزش برای افرادی تهیه شده که تجربه‌ی زیادی در برنامه‌نویسی اندروید ندارند و قصد دارند طراحی UI را با روش مدرن Compose شروع کنند. تمرکز ما در این مرحله فقط روی چیدمان و نمایش عناصر بصری است و هنوز وارد مباحث پیچیده‌تری مانند state یا تعامل با داده‌ها نمی‌شویم.

---

## ✳️ چرا از Jetpack Compose استفاده کنیم؟

### ✅ مزایا:
- کدنویسی ساده و سریع‌تر نسبت به XML
- قابلیت پیش‌نمایش زنده (Live Preview)
- ترکیب راحت‌تر کد و رابط کاربری (UI = Code)
- سازگاری بالا با Kotlin و محیط Android Studio

### ❌ مشکلات روش قدیمی با XML:
- جدا بودن UI (XML) و منطق (Kotlin)
- پیچیدگی در کنترل وضعیت‌ها و آپدیت رابط کاربری
- نیاز به استفاده از ViewBinding یا findViewById

📌 در Compose، فقط با کد Kotlin می‌نویسیم و همه چیز در یکجا قابل مشاهده و تغییر است.

---

## ℹ️ Modifier چیست؟

در Jetpack Compose، بسیاری از ویژگی‌های ظاهری و چیدمان عناصر با استفاده از "Modifier" مشخص می‌شوند. هر کامپوزری (مثل Text یا Button) می‌تواند یک `modifier` داشته باشد که روی اندازه، موقعیت، رنگ، حاشیه، پس‌زمینه و ... تأثیر می‌گذارد.

### قابلیت‌های مهم Modifier:
- `.padding()` → افزودن فاصله داخلی
- `.background()` → تعیین رنگ پس‌زمینه
- `.fillMaxWidth()` و `.fillMaxSize()` → پر کردن کل عرض یا فضا
- `.height()` و `.width()` → تعیین اندازه
- `.align()` → تنظیم موقعیت داخل عناصر مانند `Box`

### مثال ترکیبی:
```kotlin
Text(
    text = "نمونه متن",
    modifier = Modifier
        .padding(16.dp)
        .background(Color.Yellow)
        .fillMaxWidth()
)
```

> 📝 نکته: شما می‌توانید چندین ویژگی modifier را به صورت زنجیره‌ای بنویسید، چون Modifier از نوع تابعی و قابل ترکیب است.

---

## 🧱 ۱. Text — نمایش متن

### توضیح:
برای نمایش متن در صفحه از تابع `Text()` استفاده می‌کنیم. با استفاده از پارامترهایی مثل `fontSize`، `color`، `fontWeight` و `modifier` می‌توان ظاهر متن را سفارشی‌سازی کرد.

### شخصی‌سازی:
- `fontSize`: اندازه فونت (مثلاً `20.sp`)
- `fontWeight`: ضخامت فونت (مانند `FontWeight.Bold`)
- `color`: رنگ متن
- `modifier`: برای افزودن padding، تنظیم موقعیت و غیره

```kotlin
Text(
    text = "سلام!",
    fontSize = 20.sp,
    fontWeight = FontWeight.Bold,
    color = Color.Blue,
    modifier = Modifier.padding(16.dp)
)
```

### تمرین:
یک متن با محتوای دلخواه بنویس که در وسط صفحه قرار بگیرد.

### پاسخ:
```kotlin
@Composable
fun CenteredText() {
    Box(modifier = Modifier.fillMaxSize(), contentAlignment = Alignment.Center) {
        Text("من در وسط صفحه‌ام")
    }
}
```

---

## 🧱 ۲. Button — دکمه‌ها

### توضیح:
برای نمایش دکمه از تابع `Button()` استفاده می‌کنیم. درون دکمه می‌توان از `Text()` یا عناصر دیگر برای نمایش محتوا استفاده کرد. ظاهر دکمه قابل سفارشی‌سازی است.

### شخصی‌سازی:
- `colors`: رنگ دکمه
- `shape`: شکل گوشه‌های دکمه (مثلاً گرد یا مربعی)
- `modifier`: کنترل padding، اندازه، موقعیت و غیره

```kotlin
Button(
    onClick = {},
    colors = ButtonDefaults.buttonColors(containerColor = Color.Green),
    shape = RoundedCornerShape(12.dp),
    modifier = Modifier.padding(8.dp)
) {
    Text("دکمه سفارشی", color = Color.White)
}
```

### تمرین:
یک دکمه با عنوان "شروع" بساز که پایین یک متن قرار بگیرد.

### پاسخ:
```kotlin
@Composable
fun TextWithButton() {
    Column(modifier = Modifier.padding(16.dp)) {
        Text("خوش آمدید!")
        Spacer(modifier = Modifier.height(16.dp))
        Button(onClick = {}) {
            Text("شروع")
        }
    }
}
```

---

## 🧱 ۳. Column — چینش عمودی عناصر

### توضیح:
از `Column` برای چیدن عناصر به صورت عمودی استفاده می‌شود. هر عنصر در یک سطر قرار می‌گیرد.

### مثال:
```kotlin
Column(modifier = Modifier.padding(16.dp)) {
    Text("آیتم اول")
    Text("آیتم دوم")
}
```

### تمرین:
یک لیست اطلاعات کاربر بساز (نام، سن، دانشگاه).

### پاسخ:
```kotlin
@Composable
fun UserInfo() {
    Column(modifier = Modifier.padding(16.dp)) {
        Text("نام: علی")
        Text("سن: ۲۱")
        Text("دانشگاه: شریف")
    }
}
```

---

## 🧱 ۴. Row — چینش افقی عناصر

### توضیح:
از `Row` برای چیدن عناصر به صورت افقی استفاده می‌شود. مناسب برای منوها، آیتم‌های کنار هم و ردیف‌های اطلاعاتی است.

### مثال:
```kotlin
Row(modifier = Modifier.fillMaxWidth(), horizontalArrangement = Arrangement.SpaceBetween) {
    Text("خانه")
    Text("پروفایل")
    Text("تنظیمات")
}
```

### تمرین:
یک نوار بالایی طراحی کن که شامل ۳ آیتم باشد: خانه | جستجو | پیام‌ها

### پاسخ:
```kotlin
@Composable
fun TopNavigation() {
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp),
        horizontalArrangement = Arrangement.SpaceAround
    ) {
        Text("خانه")
        Text("جستجو")
        Text("پیام‌ها")
    }
}
```

---

## 🧱 ۵. Box — قرار دادن عناصر روی هم یا در گوشه‌ها

### توضیح:
`Box` مانند قاب یا ظرفی است که می‌توان عناصر را داخل آن قرار داد و با `Alignment` مشخص کرد که در کجای آن قرار بگیرند.

### مثال:
```kotlin
Box(modifier = Modifier.fillMaxSize()) {
    Text("زیرین")
    Text("رویی", modifier = Modifier.align(Alignment.Center))
}
```

### تمرین:
یک `Box` طراحی کن که یک متن در مرکز صفحه و یک متن در گوشه پایین سمت راست باشد.

### پاسخ:
```kotlin
@Composable
fun BoxExample() {
    Box(modifier = Modifier.fillMaxSize()) {
        Text("وسط صفحه", modifier = Modifier.align(Alignment.Center))
        Text("گوشه پایین راست", modifier = Modifier.align(Alignment.BottomEnd).padding(8.dp))
    }
}
```

---

## 🧪 تمرین نهایی ترکیبی

### شرح:
در این تمرین شما باید با ترکیب `Row`, `Column`, `Text`, `Button` و `Box` یک صفحه ساده طراحی کنید:

- یک نوار بالا با متن در دو سمت
- یک متن خوش‌آمدگویی در وسط
- چند دکمه زیر هم

### پاسخ:
```kotlin
@Composable
fun FullUIScreen() {
    Column(modifier = Modifier
        .fillMaxSize()
        .padding(16.dp)) {

        // Header
        Row(modifier = Modifier.fillMaxWidth(), horizontalArrangement = Arrangement.SpaceBetween) {
            Text("سلام علی!")
            Text("تنظیمات")
        }

        Spacer(modifier = Modifier.height(32.dp))

        // Content
        Column(modifier = Modifier.fillMaxWidth()) {
            Text("خوش آمدید")
            Text("این اولین پروژه‌ی شماست")
        }

        Spacer(modifier = Modifier.height(32.dp))

        // Buttons
        Button(onClick = {}) {
            Text("شروع")
        }
        Spacer(modifier = Modifier.height(8.dp))
        Button(onClick = {}) {
            Text("راهنما")
        }
    }
}
```

---

## 🔚 جمع‌بندی
در این آموزش یاد گرفتید چگونه با Jetpack Compose رابط کاربری بسازید و کامپوزهای مهمی مانند `Text`, `Button`, `Column`, `Row`, و `Box` را به کار ببرید. با تمرین‌های مختلف، مهارت طراحی صفحات ساده را بدون نیاز به XML یا ساختارهای پیچیده یاد گرفتید.

👉 در آموزش بعدی به سراغ مباحث پویا مثل **state** و تعامل با کاربر خواهیم رفت.



---

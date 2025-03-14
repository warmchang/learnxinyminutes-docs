---
contributors:
    - ["Mohammad Valipour", "https://github.com/mvalipour"]
---

<p dir='rtl'>برین فاک زبان برنامه نویسی تورینگ کامل بی نهایت ساده ایست که دارای فقط هشت</p>
<p dir='rtl'>دستور است.</p>

<p dir='rtl'>هر کارکتری به جر کارکتر های زیر در این زبان در نظر گرفته نمیشود.</p>


`>` `<` `+` `-` `.` `,` `[` `]`

<p dir='rtl'>برین فاک به صورت یک آرایه ی سی هزار خانه ای کار میکند که در ابتدا تمامی خانه های آن صفر هستند.</p>
<p dir='rtl'>همچنین یک اشاره گر در این برنامه به خانه ی فعلی اشاره میکند.</p>

<p dir='rtl'>در زیر هشت دستور این زبان شرح داده شده است:</p>

<p dir='rtl'>`+` : یک عدد به خانه ی فعلی اضافه می کند.
<p dir='rtl'>`-` : یک عدد از خانه ی فعلی کم می کند.  </p>
<p dir='rtl'>`>` : اشاره گر به خانه ی بعدی میرود -- به راست</p>
<p dir='rtl'>`<` : اشاره گر به خانه ی قبلی میرود -- به چپ</p>
<p dir='rtl'>`.` : کارکتر اسکی معادل مقدار خانه ی فعلی را چاپ میکند. -- به عنوان مثال 65 برای A</p>
<p dir='rtl'>`,` : یک کارکتر را از ورودی خوانده و مقدار آن را در خانه ی فعلی زخیره میکند.</p>
<p dir='rtl'>`[` : اگر مقدار خانه ی فعلی صفر باشد به محل بسته شدن کروشه جهش میکند. -- و از همه ی دستور های بین آن صرف نظر میشود.</p>
<p dir='rtl'>در غیر این صورت به دستور بعدی میرود.</p>
<p dir='rtl'>`]` : اگر مقدار خانه ی فعلی صفر باشد به خانه ی بعدی و در غیر این صورت به محل باز شدن کروشه جهش می کند. -- به عقب</p>

<p dir='rtl'>دو علامت کروشه امکان ایجاد حلقه را فراهم میکنند.</p>

<p dir='rtl'>در اینجا یک برنامه ی ساره برین فاک را مشاهده میکنید.</p>

```bf
++++++ [ > ++++++++++ < - ] > +++++ .
```

<p dir='rtl'>این برنامه کارکتر A را بر روی خروجی چاپ میکند.</p>
<p dir='rtl'>در این برنامه خانه ی اول به عنوان متغیر حلقه و خانه ی دوم برای مقدار عددی A</p>
<p dir='rtl'>ابتدا عدد شش در خانه ی اول ایجاد شده. سپس  برنامه  وارد یک حلقه میشود که در هر بار </p>
<p dir='rtl'>تکرار آن اشاره گر به خانه ی دوم رفته و ده بار به خانه ی فعلی اضافه می کند.</p>
<p dir='rtl'>-- و در انتهای حلقه به خانه ی اول برگشته تا حلقه کنترل شود</p>
<p dir='rtl'>بعد از اتمام حلقه به خانه ی دوم میرود و پنج بار به این خانه اضافه کرده و سپس آنرا چاپ میکند.</p>

```bf
, [ > + < - ] > .
```

<p dir='rtl'>در این برنامه ابتدا یک کارکتر از ورودی خوانده می شود. سپس یک حلقه به تعداد بار مقدار</p>
<p dir='rtl'>عددی کارکتر، یک عدد به خانه ی دوم اضافه می کند. با این کار در واقع برنامه مقدار ورودی را در خانه ی </p>
<p dir='rtl'>دوم کپی می کند. و در نهایت آن را برروی خروجی چاپ می کند.</p>

<p dir='rtl'>توجه داشته باشید که ردر بالا فواصل بین دستور ها فقط برای خوانایی بیشتر گذاشته شده اند.</p>
<p dir='rtl'>در واقع برنامه بالا به شکل زیر صحیح می باشد.</p>

```bf
,[>+<-]>.
```

<p dir='rtl'>حال سعی کنید ببینید که برنامه ی زیر چه کاری انجام می دهد؟</p>

```bf
,>,< [ > [ >+ >+ << -] >> [- << + >>] <<< -] >>
```

<p dir='rtl'>این برنامه دو عدد را از ورودی خوانده و با هم ضرب می کند.</p>

<p dir='rtl'>ابتدا دو عدد از ورودی خوانده می شوند. سپس حلقه ی بیرونی بر روی خانه شماره یک شروع میشود.</p>
<p dir='rtl'>و درون آن حلقه ی دیگری بر روی خانه ی دوم شروع میشود که خانه ی 3 را زیاد میکند.</p>
<p dir='rtl'>ولی مشکلی که در اینجا به وجود می آید اینست که در پایان حلقه ی دوم مقدار خانه ی 2 صفر شده</p>
<p dir='rtl'>و مقدار اولیه ی آن از دست رفته است. برای حل این مشکل خانه ی شماره چهار هم زیاد میشود</p>
<p dir='rtl'>و در پایان حلقه مقدار آن به خانه 2 کپی میشود.</p>
<p dir='rtl'>در پایان خانه ی شماره 2  حاوی حاصلضرب خواهد بود.</p>

<hr>

<p dir='rtl'>و این همه ی برین فاک بود! خیلی ساده برای یادگیری ولی سنگین برای به کار بردن.</p>
<p dir='rtl'>حال می توانید برای تفریح مشغول نوشتن برنامه ی های مختلف با آن شوید.</p>
<p dir='rtl'>و یا یک اجرا کننده برین فاک را با یک زبان دیگر پیاده سازی کنید.</p>
<p dir='rtl'>و یا اگر خیلی دوست داشتید یک اجرا کننده ی برین فاک با برین فاک بنویسید!!</p>

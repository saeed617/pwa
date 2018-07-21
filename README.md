_در این سوال قصد داریم به کمک کتابخانه DjangoRestFramework یک RESTful API برای وبلاگ خود طراحی کنیم._


می خواهیم یک API برای وبلاگ خود طراحی کنیم
 به طوری که کاربران بتوانند از طریق این API پست ها و کامنت های
  خود را مدیریت کنند و همچنین ادمین وبلاگ بتواند
   به تمام فعالیت ها نظارت داشته باشد
    و در صورت لزوم دست به کار شده و خودی نشان دهد.

# پروژه اولیه 

پروژه اولیه را از اینجا دانلود کنید. ساختار این پروژه به شرح زیر است:

```
blog
├── app
│   ├── migrations
│   │   ├── __init__.py
│   │   └── 0001_initial.py
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── urls.py
│   ├── serializers.py
│   ├── permissions.py
│   └── views.py
├── Blog
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── requirements.txt
```

# جزئیات 

در فایل `models.py` دو مدل به شرح زیر وجود دارد:

۱. مدل Post شامل فیلدهای زیر:
* نویسنده :‌ `owner`
* عنوان :‌‌ `title`
* متن پست :‌ `body`
* زمان انتشار پست :‌ `created`
* زمان ویرایش پست :‌ `updated`

۲. مدل Comment شامل فیلدهای زیر:
* نویسنده :‌ `owner`
* متن کامنت : `body`
* پست مربوطه : `post`
* زمان انتشار کامنت :‌ `created`
* زمان ویرایش کامنت : `updated`

در فایل 
`views.py`
چهار 
`view`
به شرح زیر وجود دارد:

* **`PostList`**

در صورتی که متد درخواست 
`GET`
باشد:
‌
لیست تمام پست ها را به صورت یک خروجی
`JSON`
به فرمت زیر بر می گرداند

```json
[
    {
        "title": "test",
        "body": "test_body",
        "created": "2018-07-18T11:27:40.074000Z",
        "owner": "admin"
    },
    {
        "title": "test",
        "body": "test_body",
        "created": "2018-07-18T11:28:00.152000Z",
        "owner": "test_author"
    },
    ...
]
```
و در صورتی که متد درخواست 
`POST`
باشد:

عنوان و متن پست را به عنوان ورودی به صورت 
`JSON`
می پذیرد و در صورتی که کاربر از قبل لاگین کرده باشد یک پست جدید به نام این کاربر می سازد


* `PostDetail`

`GET`:

جزئیات یک پست را به صورت یک خروجی 
`JSON`
به فرمت زیر بر می گرداند

```json
{
    "title": "test",
    "body": "test_body",
    "created": "2018-07-18T11:26:53.044000Z",
    "updated": "2018-07-18T11:26:53.044000Z",
    "owner": "admin",
    "comment_set": [
        "http://localhost:8000/api/comments/1/",
        "http://localhost:8000/api/comments/10/"
    ]
}
```

`PUT`:

عنوان و متن پست را به عنوان ورودی به صورت 
`JSON`
می پذیرد و در صورتی که کاربر **مالک** پست و یا **ادمین** باشد پست را ویرایش می کند.


‍`DELETE`:

در صورتی که کاربر **مالک** پست و یا **ادمین** باشد پست را حذف می کند.


* `CommentDetail`

`GET`:

جزئیات یک کامنت را به صورت یک خروجی 
`JSON`
به فرمت زیر بر می گرداند

```json
{
    "post": "http://localhost:8000/api/comments/1/",
    "owner": "hamid",
    "body": "test_body",
    "created": "2018-07-18T11:28:47.400000Z",
    "updated": "2018-07-18T11:28:47.401000Z"
}
```

`PUT`:

  متن کامنت را به عنوان ورودی به صورت 
`JSON`
می پذیرد و در صورتی که کاربر **مالک** کامنت و یا **ادمین** باشد کامنت را ویرایش می کند.


‍`DELETE`:

در صورتی که کاربر **مالک** کامنت و یا **ادمین** باشد کامنت را حذف می کند.


* `AddComment`

`POST`:

  متن کامنت را به عنوان ورودی به صورت 
`JSON`
می پذیرد و در صورتی که کاربر از قبل لاگین کرده باشد یک کامنت جدید به نام این کاربر و برای پست انتخاب شده می سازد 



اما کارهایی که شما باید تو این پروژه انجام بدید:

شما باید در دو فایل 
`serializers.py`
و
`permissions.py`
کلاس هایی که در این 
`view`
ها استفاده شده و پیاده سازی نشده اند را طوری پیاده سازی کنید که 
`view`
ها طبق توضیحات داده شده عمل کنند.

# نکات 

+ شما تنها مجاز به تغییر در `app/serializers.py` و `app/permissions.py` هستید.
اگر تغییری در سایر فایل‌ها ایجاد کنید، این تغییرات نادیده گرفته خواهد شد.
+ پس از اعمال تغییرات، کل پروژه را Zip کرده و ارسال کنید.
+ نام فایل Zip اهمیت ندارد.
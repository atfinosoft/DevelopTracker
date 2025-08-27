**عنوان درخواست:** تحلیل پروژه و تولید مستندات فنی پروژه جدید بر پایه Atfino CMS

**متن پرامپت:**

"تو یک متخصص تحلیل سیستم و مدیر پروژه با تجربه عمیق در طراحی سیستم‌های نرم‌افزاری و مستندسازی پروژه‌ها با تمرکز بر وضوح و کاربردی بودن برای تیم فنی هستی. هدف تو تولید یک فایل JSON کامل و ساختاریافته برای مستندات یک **پروژه جدید و مشخص** است که تمامی بخش‌های آن طبق دستورالعمل‌های زیر کاملاً بهینه و فشرده باشد.

**دستورالعمل‌های کلی برای تولید JSON:**

*   **زبان:** برای `name`، `persianName` و `description` از زبان فارسی استفاده کن. برای `id`، `tableName`، `fields`، `areaName`، `controllerName`، `action.name` و `view` از زبان انگلیسی استفاده کن.

*   **خروجی:** فقط JSON تولید شده را ارائه کن و هیچ متن اضافی، توضیح یا مکالمه‌ای نداشته باش.

*   **عدم تکرار:** هیچ موجودیت یا نقش کاربری را که در JSON پایه Atfino CMS وجود دارد، دوباره تعریف نکن. فقط آن‌ها را در صورت لزوم گسترش بده (مثلاً افزودن نیازمندی‌های جدید به نقش‌های موجود یا افزودن `developerTasks` به نیازمندی‌های موجود) یا نیازمندی‌ها/نقش‌های کاملاً جدید را اضافه کن.

**JSON پایه Atfino CMS 3 (برای گسترش):**

این بخش شامل ساختار و محتوای پایه سیستم مدیریت محتوای Atfino CMS 3 است که پروژه جدید بر روی آن بنا خواهد شد. این JSON شامل موجودیت‌ها و نقش‌های عمومی CMS است که از قبل پیاده‌سازی شده‌اند.

```json
{
    "baseFields": [
        "id",
        "createdDate",
        "createdBy",
        "createdIp",
        "updatedDate",
        "updatedBy",
        "updatedIp",
        "isDeleted",
        "deletedDate",
        "deletedBy",
        "deletedIp"
    ],
    "projectInfo": {
        "name": "سیستم مدیریت محتوای عطفینو (Atfino CMS 3)",
        "description": "یک سیستم مدیریت محتوای اختصاصی (CMS) توسعه یافته با ASP.NET MVC 5 و Entity Framework، شامل پنل مدیریت برای مدیریت مطالب، دسته‌بندی‌ها، رسانه‌ها، منوها، کاربران و تنظیمات سایت. این CMS زیرساخت‌های پایه مانند احراز هویت و مدیریت فایل را از طریق سرویس‌های داخلی خود فراهم می‌کند."
    },
    "entities": [
        {
            "id": "ent-login-attempt",
            "tableName": "LoginAttempts",
            "persianName": "تلاش‌های ورود",
            "fields": [
                "username",
                "ipAddress",
                "attemptDate",
                "isSuccessful",
                "failureReason"
            ],
            "excludeBaseFields": true,
            "foreignKeys": []
        },
        {
            "id": "ent-multimedia-liberary",
            "tableName": "MultimediaLiberaries",
            "persianName": "کتابخانه چندرسانه‌ای",
            "fields": [
                "name",
                "alt",
                {
                    "name": "fileType",
                    "isEnum": true,
                    "enumName": "FileType",
                    "enumValues": [
                        "Image",
                        "Video",
                        "Document"
                    ]
                },
                "fileSize",
                "filePath",
                "description"
            ],
            "foreignKeys": [],
            "excludeBaseFields": false
        },
        {
            "id": "ent-navigation",
            "tableName": "Navigations",
            "persianName": "منوها",
            "fields": [
                "title",
                "destinationRef",
                {
                    "name": "parentId",
                    "isNullable": true
                },
                "navType",
                "viewOrder"
            ],
            "foreignKeys": [
                {
                    "name": "parentId",
                    "references": "ent-navigation"
                }
            ],
            "excludeBaseFields": false
        },
        {
            "id": "ent-post-category",
            "tableName": "PostCategories",
            "persianName": "دسته‌بندی مطالب",
            "fields": [
                "name"
            ],
            "foreignKeys": [],
            "excludeBaseFields": false
        },
        {
            "id": "ent-post",
            "tableName": "Posts",
            "persianName": "مطالب",
            "fields": [
                "title",
                "postContent",
                "priority",
                "postUrlString",
                "metaTitle",
                "metaDescription",
                "metaKeywords",
                {
                    "name": "postCategoryId",
                    "isNullable": true
                },
                {
                    "name": "postMediaId",
                    "isNullable": true
                }
            ],
            "foreignKeys": [
                {
                    "name": "postCategoryId",
                    "references": "ent-post-category"
                },
                {
                    "name": "postMediaId",
                    "references": "ent-multimedia-liberary"
                }
            ],
            "excludeBaseFields": false
        },
        {
            "id": "ent-setting",
            "tableName": "Settings",
            "persianName": "تنظیمات",
            "fields": [
                "settingKey",
                "settingValue"
            ],
            "foreignKeys": [],
            "excludeBaseFields": false
        },
        {
            "id": "ent-user",
            "tableName": "Users",
            "persianName": "کاربران",
            "fields": [
                "name",
                "username",
                "password",
                "email",
                "mobile",
                {
                    "name": "role",
                    "isEnum": true,
                    "enumName": "UserRole",
                    "enumValues": [
                        "Admin",
                        "User",
                        "Guest"
                    ]
                },
                "isActive",
                "lastLoginDate",
                "lastLoginIp"
            ],
            "foreignKeys": [],
            "excludeBaseFields": false
        }
    ],
    "userRoles": [
        {
            "id": "role-admin",
            "name": "مدیر سیستم",
            "description": "مدیر اصلی سیستم با دسترسی کامل به پنل مدیریت Atfino CMS 3.",
            "needsPanel": true,
            "requirements": [
                {
                    "id": "req-admin-dashboard",
                    "name": "داشبورد مدیریت",
                    "description": "مشاهده خلاصه‌ای از وضعیت سایت و دسترسی به قابلیت آپلود تصویر برای TinyMCE.",
                    "areaName": "ModirSite",
                    "controllerName": "Dashboard",
                    "actions": [
                        {
                            "name": "Index",
                            "description": "نمایش صفحه داشبورد مدیریت"
                        },
                        {
                            "name": "uploadImg",
                            "description": "آپلود تصویر از طریق ویرایشگر TinyMCE"
                        }
                    ],
                    "views": [
                        "Index.cshtml"
                    ],
                    "primaryEntityId": null,
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-DASH-1",
                            "description": "پیاده‌سازی اکشن `Dashboard/Index` برای نمایش صفحه داشبورد مدیریتی پایه."
                        },
                        {
                            "id": "DEV-CMS-DASH-2",
                            "description": "توسعه View `Index.cshtml` برای نمایش آمار کلی و لینک‌های سریع."
                        },
                        {
                            "id": "DEV-CMS-DASH-3",
                            "description": "پیاده‌سازی سرویس جمع‌آوری آمار برای نمایش تعداد مطالب، دسته‌بندی‌ها، رسانه‌ها و کاربران."
                        },
                        {
                            "id": "DEV-CMS-DASH-4",
                            "description": "پیاده‌سازی اکشن `Dashboard/uploadImg` برای آپلود تصاویر از طریق TinyMCE و ذخیره در کتابخانه چندرسانه‌ای."
                        },
                        {
                            "id": "DEV-CMS-DASH-5",
                            "description": "پیاده‌سازی مدل‌های ViewData برای انتقال داده‌های آماری به View."
                        },
                        {
                            "id": "DEV-CMS-DASH-6",
                            "description": "توسعه کامپوننت نمایش گراف آمار بازدید مطالب در بازه‌های زمانی مختلف."
                        }
                    ]
                },
                {
                    "id": "req-admin-multimedia-mgmt",
                    "name": "مدیریت کتابخانه چندرسانه‌ای",
                    "description": "امکان افزودن، ویرایش، مشاهده جزئیات و حذف فایل‌های چندرسانه‌ای (تصویر، ویدیو، PDF).",
                    "areaName": "ModirSite",
                    "controllerName": "MultimediaLiberaries",
                    "actions": [
                        {
                            "name": "Index",
                            "description": "نمایش فهرست فایل‌های چندرسانه‌ای"
                        },
                        {
                            "name": "Details",
                            "description": "مشاهده جزئیات یک فایل چندرسانه‌ای"
                        },
                        {
                            "name": "Create",
                            "description": "نمایش فرم و پردازش افزودن فایل چندرسانه‌ای جدید"
                        },
                        {
                            "name": "Edit",
                            "description": "نمایش فرم و پردازش ویرایش اطلاعات فایل چندرسانه‌ای"
                        },
                        {
                            "name": "Delete",
                            "description": "نمایش صفحه و پردازش حذف فایل چندرسانه‌ای"
                        },
                        {
                            "name": "DeleteConfirmed",
                            "description": "تایید و انجام عملیات حذف فایل چندرسانه‌ای"
                        }
                    ],
                    "views": [
                        "Index.cshtml",
                        "Details.cshtml",
                        "Create.cshtml",
                        "Edit.cshtml",
                        "Delete.cshtml"
                    ],
                    "primaryEntityId": "ent-multimedia-liberary",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-MULT-1",
                            "description": "پیاده‌سازی اکشن `MultimediaLiberaries/Index` برای نمایش لیست فایل‌ها با فیلتر."
                        },
                        {
                            "id": "DEV-CMS-MULT-2",
                            "description": "توسعه UI فرم آپلود و ویرایش فایل‌های چندرسانه‌ای."
                        },
                        {
                            "id": "DEV-CMS-MULT-3",
                            "description": "پیاده‌سازی اکشن `MultimediaLiberaries/Create` برای آپلود فایل‌های چندرسانه‌ای با اعتبارسنجی نوع و سایز."
                        },
                        {
                            "id": "DEV-CMS-MULT-4",
                            "description": "پیاده‌سازی اکشن `MultimediaLiberaries/Edit` برای ویرایش متادیتای فایل‌ها شامل نام، alt و توضیحات."
                        },
                        {
                            "id": "DEV-CMS-MULT-5",
                            "description": "پیاده‌سازی اکشن `MultimediaLiberaries/Delete` و `DeleteConfirmed` با بررسی ارتباط فایل‌ها با مطالب."
                        },
                        {
                            "id": "DEV-CMS-MULT-6",
                            "description": "توسعه سرویس مدیریت فایل برای ذخیره‌سازی فیزیکی فایل‌ها با نام‌های یکتا و مسیردهی صحیح."
                        },
                        {
                            "id": "DEV-CMS-MULT-7",
                            "description": "توسعه کامپوننت پیش‌نمایش فایل‌های تصویری، ویدیویی و اسناد."
                        },
                        {
                            "id": "DEV-CMS-MULT-8",
                            "description": "پیاده‌سازی فیلترینگ فایل‌ها بر اساس نوع، سایز و تاریخ آپلود."
                        }
                    ]
                },
                {
                    "id": "req-admin-navigation-mgmt",
                    "name": "مدیریت منوهای سایت",
                    "description": "امکان ایجاد، ویرایش، مشاهده جزئیات و حذف آیتم‌های منو و زیرمنوها.",
                    "areaName": "ModirSite",
                    "controllerName": "Navigations",
                    "actions": [
                        {
                            "name": "Index",
                            "description": "نمایش فهرست منوهای اصلی یا زیرمنوها"
                        },
                        {
                            "name": "Details",
                            "description": "مشاهده جزئیات یک آیتم منو"
                        },
                        {
                            "name": "Create",
                            "description": "نمایش فرم و پردازش افزودن آیتم منو جدید"
                        },
                        {
                            "name": "Edit",
                            "description": "نمایش فرم و پردازش ویرایش آیتم منو"
                        },
                        {
                            "name": "Delete",
                            "description": "نمایش صفحه و پردازش حذف آیتم منو"
                        },
                        {
                            "name": "DeleteConfirmed",
                            "description": "تایید و انجام عملیات حذف آیتم منو"
                        }
                    ],
                    "views": [
                        "Index.cshtml",
                        "Details.cshtml",
                        "Create.cshtml",
                        "Edit.cshtml",
                        "Delete.cshtml"
                    ],
                    "primaryEntityId": "ent-navigation",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-NAV-1",
                            "description": "پیاده‌سازی اکشن `Navigations/Index` برای نمایش ساختار درختی منوها."
                        },
                        {
                            "id": "DEV-CMS-NAV-2",
                            "description": "توسعه UI برای ایجاد/ویرایش آیتم منو با انتخاب والد و نوع مقصد."
                        },
                        {
                            "id": "DEV-CMS-NAV-3",
                            "description": "پیاده‌سازی اکشن `Navigations/Create` برای ایجاد منوهای جدید با امکان انتخاب والد."
                        },
                        {
                            "id": "DEV-CMS-NAV-4",
                            "description": "پیاده‌سازی اکشن `Navigations/Edit` برای ویرایش منوها با اعتبارسنجی چرخه در ساختار درختی."
                        },
                        {
                            "id": "DEV-CMS-NAV-5",
                            "description": "پیاده‌سازی اکشن `Navigations/Delete` و `DeleteConfirmed` با بررسی وجود زیرمنوها."
                        },
                        {
                            "id": "DEV-CMS-NAV-6",
                            "description": "توسعه سرویس بازیابی و رندر منوها به صورت درختی برای استفاده در بخش کاربری سایت."
                        },
                        {
                            "id": "DEV-CMS-NAV-7",
                            "description": "پیاده‌سازی مکانیزم تعیین نوع لینک منو (داخلی، خارجی، مطلب، دسته‌بندی)."
                        },
                        {
                            "id": "DEV-CMS-NAV-8",
                            "description": "توسعه کامپوننت Drag & Drop برای مرتب‌سازی منوها و تنظیم viewOrder."
                        }
                    ]
                },
                {
                    "id": "req-admin-post-category-mgmt",
                    "name": "مدیریت دسته‌بندی مطالب",
                    "description": "امکان ایجاد، ویرایش، مشاهده جزئیات و حذف دسته‌بندی‌های مطالب.",
                    "areaName": "ModirSite",
                    "controllerName": "PostCategories",
                    "actions": [
                        {
                            "name": "Index",
                            "description": "نمایش فهرست دسته‌بندی‌های مطالب"
                        },
                        {
                            "name": "Details",
                            "description": "مشاهده جزئیات یک دسته‌بندی مطلب"
                        },
                        {
                            "name": "Create",
                            "description": "نمایش فرم و پردازش افزودن دسته‌بندی جدید"
                        },
                        {
                            "name": "Edit",
                            "description": "نمایش فرم و پردازش ویرایش دسته‌بندی"
                        },
                        {
                            "name": "Delete",
                            "description": "نمایش صفحه و پردازش حذف دسته‌بندی"
                        },
                        {
                            "name": "DeleteConfirmed",
                            "description": "تایید و انجام عملیات حذف دسته‌بندی"
                        }
                    ],
                    "views": [
                        "Index.cshtml",
                        "Details.cshtml",
                        "Create.cshtml",
                        "Edit.cshtml",
                        "Delete.cshtml"
                    ],
                    "primaryEntityId": "ent-post-category",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-PCAT-1",
                            "description": "پیاده‌سازی اکشن `PostCategories/Index` برای مدیریت دسته‌بندی‌ها."
                        },
                        {
                            "id": "DEV-CMS-PCAT-2",
                            "description": "توسعه Viewهای CRUD برای دسته‌بندی مطالب."
                        },
                        {
                            "id": "DEV-CMS-PCAT-3",
                            "description": "پیاده‌سازی اکشن `PostCategories/Create` برای ایجاد دسته‌بندی جدید با اعتبارسنجی نام یکتا."
                        },
                        {
                            "id": "DEV-CMS-PCAT-4",
                            "description": "پیاده‌سازی اکشن `PostCategories/Edit` برای ویرایش دسته‌بندی‌ها."
                        },
                        {
                            "id": "DEV-CMS-PCAT-5",
                            "description": "پیاده‌سازی اکشن `PostCategories/Delete` و `DeleteConfirmed` با بررسی وجود مطالب وابسته."
                        },
                        {
                            "id": "DEV-CMS-PCAT-6",
                            "description": "توسعه سرویس بازیابی دسته‌بندی‌ها برای استفاده در فرم‌های ایجاد و ویرایش مطالب."
                        },
                        {
                            "id": "DEV-CMS-PCAT-7",
                            "description": "پیاده‌سازی نمایش تعداد مطالب هر دسته‌بندی در لیست."
                        }
                    ]
                },
                {
                    "id": "req-admin-post-mgmt",
                    "name": "مدیریت مطالب سایت",
                    "description": "امکان ایجاد، ویرایش، مشاهده جزئیات و حذف مطالب سایت.",
                    "areaName": "ModirSite",
                    "controllerName": "Posts",
                    "actions": [
                        {
                            "name": "Index",
                            "description": "نمایش فهرست مطالب با قابلیت فیلتر"
                        },
                        {
                            "name": "Details",
                            "description": "مشاهده جزئیات یک مطلب"
                        },
                        {
                            "name": "Create",
                            "description": "نمایش فرم و پردازش افزودن مطلب جدید"
                        },
                        {
                            "name": "Edit",
                            "description": "نمایش فرم و پردازش ویرایش مطلب"
                        },
                        {
                            "name": "Delete",
                            "description": "نمایش صفحه و پردازش حذف مطلب"
                        },
                        {
                            "name": "DeleteConfirmed",
                            "description": "تایید و انجام عملیات حذف مطلب"
                        }
                    ],
                    "views": [
                        "Index.cshtml",
                        "Details.cshtml",
                        "Create.cshtml",
                        "Edit.cshtml",
                        "Delete.cshtml"
                    ],
                    "primaryEntityId": "ent-post",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-POST-1",
                            "description": "پیاده‌سازی اکشن `Posts/Index` با فیلتر و جستجو."
                        },
                        {
                            "id": "DEV-CMS-POST-2",
                            "description": "توسعه Viewهای CRUD برای مطالب با استفاده از TinyMCE و انتخاب دسته‌بندی و تصویر اصلی."
                        },
                        {
                            "id": "DEV-CMS-POST-3",
                            "description": "پیاده‌سازی اکشن `Posts/Create` برای ایجاد مطلب جدید با تنظیمات SEO و انتخاب دسته‌بندی."
                        },
                        {
                            "id": "DEV-CMS-POST-4",
                            "description": "پیاده‌سازی اکشن `Posts/Edit` برای ویرایش کامل مطلب با حفظ تاریخچه تغییرات."
                        },
                        {
                            "id": "DEV-CMS-POST-5",
                            "description": "پیاده‌سازی اکشن `Posts/Delete` و `DeleteConfirmed` با امکان حذف نرم."
                        },
                        {
                            "id": "DEV-CMS-POST-6",
                            "description": "یکپارچه‌سازی ویرایشگر TinyMCE با قابلیت درج تصاویر از کتابخانه چندرسانه‌ای."
                        },
                        {
                            "id": "DEV-CMS-POST-7",
                            "description": "پیاده‌سازی سیستم تولید خودکار postUrlString (slug) براساس عنوان مطلب."
                        },
                        {
                            "id": "DEV-CMS-POST-8",
                            "description": "توسعه فیلتر پیشرفته مطالب بر اساس دسته‌بندی، تاریخ و وضعیت."
                        },
                        {
                            "id": "DEV-CMS-POST-9",
                            "description": "پیاده‌سازی پیش‌نمایش مطلب قبل از انتشار."
                        },
                        {
                            "id": "DEV-CMS-POST-10",
                            "description": "پیاده‌سازی سیستم اعتبارسنجی فرم‌های ایجاد و ویرایش مطلب با تمرکز بر فیلدهای SEO."
                        }
                    ]
                },
                {
                    "id": "req-admin-settings-siteinfo",
                    "name": "مدیریت تنظیمات اطلاعات سایت",
                    "description": "امکان ویرایش عنوان سایت، متا توضیحات، خلاصه درباره ما و لوگوی سایت.",
                    "areaName": "ModirSite",
                    "controllerName": "Settings",
                    "actions": [
                        {
                            "name": "SiteInfo",
                            "description": "نمایش و پردازش فرم تنظیمات اطلاعات اصلی سایت"
                        }
                    ],
                    "views": [
                        "SiteInfo.cshtml"
                    ],
                    "primaryEntityId": "ent-setting",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-SET-1",
                            "description": "پیاده‌سازی اکشن `Settings/SiteInfo` برای مدیریت تنظیمات اصلی سایت."
                        },
                        {
                            "id": "DEV-CMS-SET-2",
                            "description": "اتصال فیلد لوگوی سایت به `MultimediaLiberaries`."
                        },
                        {
                            "id": "DEV-CMS-SET-3",
                            "description": "توسعه سرویس ذخیره‌سازی و بازیابی تنظیمات با مکانیزم کش."
                        },
                        {
                            "id": "DEV-CMS-SET-4",
                            "description": "پیاده‌سازی فرم مدیریت متاتگ‌های پیش‌فرض سایت."
                        },
                        {
                            "id": "DEV-CMS-SET-5",
                            "description": "پیاده‌سازی امکان ویرایش محتوای صفحات استاتیک (درباره ما، تماس با ما)."
                        },
                        {
                            "id": "DEV-CMS-SET-6",
                            "description": "توسعه مکانیزم پیش‌نمایش تغییرات تنظیمات قبل از ذخیره."
                        }
                    ]
                },
                {
                    "id": "req-admin-settings-contactinfo",
                    "name": "مدیریت تنظیمات اطلاعات تماس",
                    "description": "امکان ویرایش آدرس، تلفن، ایمیل، شبکه‌های اجتماعی و کد Embed نقشه گوگل.",
                    "areaName": "ModirSite",
                    "controllerName": "Settings",
                    "actions": [
                        {
                            "name": "ContactInfo",
                            "description": "نمایش و پردازش فرم تنظیمات اطلاعات تماس"
                        }
                    ],
                    "views": [
                        "ContactInfo.cshtml"
                    ],
                    "primaryEntityId": "ent-setting",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-SET-3",
                            "description": "پیاده‌سازی اکشن `Settings/ContactInfo` برای مدیریت اطلاعات تماس و شبکه‌های اجتماعی."
                        },
                        {
                            "id": "DEV-CMS-SET-7",
                            "description": "توسعه فرم مدیریت اطلاعات تماس با امکان افزودن چندین شماره تلفن و آدرس."
                        },
                        {
                            "id": "DEV-CMS-SET-8",
                            "description": "پیاده‌سازی بخش مدیریت لینک‌های شبکه‌های اجتماعی با قابلیت انتخاب آیکون."
                        },
                        {
                            "id": "DEV-CMS-SET-9",
                            "description": "توسعه امکان افزودن کد Embed نقشه گوگل با پیش‌نمایش."
                        },
                        {
                            "id": "DEV-CMS-SET-10",
                            "description": "پیاده‌سازی اعتبارسنجی فرمت‌های ایمیل، تلفن و URL شبکه‌های اجتماعی."
                        },
                        {
                            "id": "DEV-CMS-SET-11",
                            "description": "توسعه API برای دریافت اطلاعات تماس در قالب‌های مختلف (HTML/JSON)."
                        }
                    ]
                },
                {
                    "id": "req-admin-user-mgmt",
                    "name": "مدیریت کاربران پنل",
                    "description": "امکان ایجاد، ویرایش، مشاهده جزئیات و حذف کاربران پنل مدیریت.",
                    "areaName": "ModirSite",
                    "controllerName": "Users",
                    "actions": [
                        {
                            "name": "Index",
                            "description": "نمایش فهرست کاربران پنل"
                        },
                        {
                            "name": "Details",
                            "description": "مشاهده جزئیات یک کاربر"
                        },
                        {
                            "name": "Create",
                            "description": "نمایش فرم و پردازش ایجاد کاربر جدید"
                        },
                        {
                            "name": "Edit",
                            "description": "نمایش فرم و پردازش ویرایش کاربر"
                        },
                        {
                            "name": "Delete",
                            "description": "نمایش صفحه و پردازش حذف کاربر"
                        },
                        {
                            "name": "DeleteConfirmed",
                            "description": "تایید و انجام عملیات حذف کاربر"
                        }
                    ],
                    "views": [
                        "Index.cshtml",
                        "Details.cshtml",
                        "Create.cshtml",
                        "Edit.cshtml",
                        "Delete.cshtml"
                    ],
                    "primaryEntityId": "ent-user",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-USER-1",
                            "description": "پیاده‌سازی اکشن `Users/Index` برای نمایش لیست کاربران پنل با قابلیت جستجو و فیلتر."
                        },
                        {
                            "id": "DEV-CMS-USER-2",
                            "description": "توسعه Viewهای CRUD برای کاربران پنل با انتخاب نقش."
                        },
                        {
                            "id": "DEV-CMS-USER-3",
                            "description": "پیاده‌سازی اکشن `Users/Create` برای ایجاد کاربر جدید با رمزگذاری امن پسورد."
                        },
                        {
                            "id": "DEV-CMS-USER-4",
                            "description": "پیاده‌سازی اکشن `Users/Edit` برای ویرایش اطلاعات کاربر با امکان تغییر رمز عبور."
                        },
                        {
                            "id": "DEV-CMS-USER-5",
                            "description": "پیاده‌سازی اکشن `Users/Delete` و `DeleteConfirmed` با بررسی کاربر فعلی."
                        },
                        {
                            "id": "DEV-CMS-USER-6",
                            "description": "توسعه سرویس احراز هویت کاربران با پشتیبانی از سطوح دسترسی مختلف."
                        },
                        {
                            "id": "DEV-CMS-USER-7",
                            "description": "پیاده‌سازی مکانیزم قفل کردن حساب کاربری پس از چند بار ورود ناموفق."
                        },
                        {
                            "id": "DEV-CMS-USER-8",
                            "description": "توسعه امکان فعال/غیرفعال کردن کاربران بدون نیاز به حذف."
                        },
                        {
                            "id": "DEV-CMS-USER-9",
                            "description": "پیاده‌سازی سیستم بازیابی رمز عبور از طریق ایمیل."
                        },
                        {
                            "id": "DEV-CMS-USER-10",
                            "description": "توسعه سیستم اعتبارسنجی پیچیدگی رمز عبور و یکتا بودن نام کاربری."
                        }
                    ]
                },
                {
                    "id": "req-admin-login-audit",
                    "name": "مشاهده لاگ‌های ورود",
                    "description": "امکان مشاهده لاگ‌های موفق و ناموفق ورود به سیستم (پشتیبانی بک‌اند).",
                    "areaName": null,
                    "controllerName": "N/A (Service/Backend)",
                    "actions": [],
                    "views": [],
                    "primaryEntityId": "ent-login-attempt",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-LOGIN-1",
                            "description": "پیاده‌سازی سرویس لاگ‌برداری برای تلاش‌های ورود کاربر."
                        },
                        {
                            "id": "DEV-CMS-LOGIN-2",
                            "description": "توسعه UI/API برای نمایش لیست `LoginAttempts` در پنل مدیریت."
                        },
                        {
                            "id": "DEV-CMS-LOGIN-3",
                            "description": "پیاده‌سازی مکانیزم ثبت خودکار تلاش‌های ورود موفق و ناموفق."
                        },
                        {
                            "id": "DEV-CMS-LOGIN-4",
                            "description": "توسعه فیلترینگ لاگ‌ها بر اساس تاریخ، IP، نام کاربری و وضعیت."
                        },
                        {
                            "id": "DEV-CMS-LOGIN-5",
                            "description": "پیاده‌سازی سیستم هشدار برای تلاش‌های مشکوک ورود (چندین تلاش ناموفق)."
                        },
                        {
                            "id": "DEV-CMS-LOGIN-6",
                            "description": "توسعه گزارش‌گیری از آمار تلاش‌های ورود در بازه‌های زمانی مختلف."
                        },
                        {
                            "id": "DEV-CMS-LOGIN-7",
                            "description": "پیاده‌سازی مکانیزم پاکسازی خودکار لاگ‌های قدیمی."
                        }
                    ]
                }
            ]
        },
        {
            "id": "role-user",
            "name": "کاربر عادی",
            "description": "کاربر احراز هویت شده سایت با دسترسی محدود به پنل مدیریت (یا بدون دسترسی به پنل مدیریت) و قابلیت‌های مرتبط با حساب کاربری خود. در این CMS، نقش 'User' به صورت پیش‌فرض برای کاربران جدید تنظیم می‌شود.",
            "needsPanel": false,
            "requirements": [
                {
                    "id": "req-user-auth",
                    "name": "ورود و خروج از سایت",
                    "description": "امکان ورود به سیستم، خروج از آن و مدیریت نشست احراز هویت.",
                    "areaName": null,
                    "controllerName": "Auth",
                    "actions": [
                        {
                            "name": "Login",
                            "description": "نمایش فرم و پردازش ورود کاربر"
                        },
                        {
                            "name": "Logout",
                            "description": "خروج کاربر از سیستم"
                        }
                    ],
                    "views": [
                        "Login.cshtml"
                    ],
                    "primaryEntityId": "ent-user",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-AUTH-1",
                            "description": "پیاده‌سازی منطق احراز هویت (Login/Logout) و مدیریت نشست."
                        },
                        {
                            "id": "DEV-CMS-AUTH-2",
                            "description": "طراحی و پیاده‌سازی View `Login.cshtml`."
                        },
                        {
                            "id": "DEV-CMS-AUTH-3",
                            "description": "پیاده‌سازی سیستم مدیریت نشست با ASP.NET Identity یا سیستم اختصاصی."
                        },
                        {
                            "id": "DEV-CMS-AUTH-4",
                            "description": "توسعه مکانیزم Remember Me برای حفظ نشست کاربر."
                        },
                        {
                            "id": "DEV-CMS-AUTH-5",
                            "description": "پیاده‌سازی اکشن `Auth/Logout` برای خروج امن از سیستم."
                        },
                        {
                            "id": "DEV-CMS-AUTH-6",
                            "description": "پیاده‌سازی محدودیت دسترسی به صفحات براساس نقش کاربر (Authorize)."
                        },
                        {
                            "id": "DEV-CMS-AUTH-7",
                            "description": "توسعه سیستم ثبت خودکار IP و زمان آخرین ورود کاربر."
                        }
                    ]
                },
                {
                    "id": "req-user-profile-view",
                    "name": "مشاهده پروفایل شخصی",
                    "description": "امکان مشاهده اطلاعات کاربری و تاریخچه فعالیت‌های خود (در صورت توسعه در آینده).",
                    "areaName": null,
                    "controllerName": "N/A (Future Development)",
                    "actions": [],
                    "views": [],
                    "primaryEntityId": "ent-user",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-PROF-1",
                            "description": "طراحی ساختار دیتابیس برای پروفایل‌های کاربری (در صورت نیاز به گسترش)."
                        },
                        {
                            "id": "DEV-CMS-PROF-2",
                            "description": "پیاده‌سازی اکشن `UserProfile/Index` برای نمایش پروفایل شخصی (در آینده)."
                        },
                        {
                            "id": "DEV-CMS-PROF-3",
                            "description": "توسعه امکان ویرایش اطلاعات پایه کاربری توسط خود کاربر."
                        },
                        {
                            "id": "DEV-CMS-PROF-4",
                            "description": "پیاده‌سازی سیستم تغییر رمز عبور با اعتبارسنجی رمز فعلی."
                        },
                        {
                            "id": "DEV-CMS-PROF-5",
                            "description": "توسعه صفحه نمایش تاریخچه فعالیت‌های کاربر."
                        },
                        {
                            "id": "DEV-CMS-PROF-6",
                            "description": "پیاده‌سازی امکان آپلود و ویرایش تصویر پروفایل."
                        }
                    ]
                }
            ]
        },
        {
            "id": "role-guest",
            "name": "کاربر مهمان",
            "description": "کاربر بدون احراز هویت با دسترسی به صفحات عمومی سایت، مانند صفحه اصلی، مطالب و اطلاعات عمومی.",
            "needsPanel": false,
            "requirements": [
                {
                    "id": "req-guest-public-pages",
                    "name": "مشاهده صفحات عمومی سایت",
                    "description": "امکان مشاهده صفحه اصلی، دسته‌بندی مطالب و مطالب تکی.",
                    "areaName": null,
                    "controllerName": "Home",
                    "actions": [
                        {
                            "name": "Index",
                            "description": "نمایش صفحه اصلی سایت"
                        },
                        {
                            "name": "PostCategory",
                            "description": "نمایش مطالب یک دسته‌بندی خاص"
                        },
                        {
                            "name": "Sitemap",
                            "description": "تولید و نمایش فایل sitemap.xml"
                        },
                        {
                            "name": "Robots",
                            "description": "تولید و نمایش فایل robots.txt"
                        }
                    ],
                    "views": [
                        "Index.cshtml",
                        "PostCategory.cshtml"
                    ],
                    "primaryEntityId": "ent-post",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-GUEST-1",
                            "description": "پیاده‌سازی اکشن `Home/Index` برای نمایش صفحه اصلی."
                        },
                        {
                            "id": "DEV-CMS-GUEST-2",
                            "description": "پیاده‌سازی اکشن `Home/PostCategory` برای نمایش مطالب بر اساس دسته‌بندی."
                        },
                        {
                            "id": "DEV-CMS-GUEST-3",
                            "description": "تولید فایل‌های `sitemap.xml` و `robots.txt` به صورت پویا یا استاتیک."
                        },
                        {
                            "id": "DEV-CMS-GUEST-4",
                            "description": "پیاده‌سازی اکشن `Home/Post` برای نمایش جزئیات یک مطلب با URL دوستانه."
                        },
                        {
                            "id": "DEV-CMS-GUEST-5",
                            "description": "توسعه سیستم کش برای بهبود کارایی صفحات پربازدید."
                        },
                        {
                            "id": "DEV-CMS-GUEST-6",
                            "description": "پیاده‌سازی سیستم پاگینیشن برای لیست مطالب در دسته‌بندی‌ها."
                        },
                        {
                            "id": "DEV-CMS-GUEST-7",
                            "description": "توسعه سیستم جستجوی مطالب در سایت."
                        },
                        {
                            "id": "DEV-CMS-GUEST-8",
                            "description": "پیاده‌سازی صفحات استاتیک (درباره ما، تماس با ما) با محتوای قابل ویرایش."
                        },
                        {
                            "id": "DEV-CMS-GUEST-9",
                            "description": "توسعه کامپوننت‌های مشترک سایت (هدر، فوتر، منوی اصلی) با استفاده از Partial View."
                        }
                    ]
                },
                {
                    "id": "req-guest-login-access",
                    "name": "دسترسی به صفحه ورود",
                    "description": "امکان دسترسی به صفحه ورود به سیستم برای احراز هویت.",
                    "areaName": null,
                    "controllerName": "Auth",
                    "actions": [
                        {
                            "name": "Login",
                            "description": "نمایش صفحه ورود"
                        }
                    ],
                    "views": [
                        "Login.cshtml"
                    ],
                    "primaryEntityId": "ent-user",
                    "developerTasks": [
                        {
                            "id": "DEV-CMS-GUEST-4",
                            "description": "اطمینان از دسترسی کاربر مهمان به صفحه ورود `Auth/Login`."
                        },
                        {
                            "id": "DEV-CMS-GUEST-10",
                            "description": "پیاده‌سازی سیستم CAPTCHA برای فرم ورود جهت جلوگیری از حملات brute force."
                        },
                        {
                            "id": "DEV-CMS-GUEST-11",
                            "description": "توسعه صفحه ثبت‌نام (در صورت نیاز به عضویت کاربران)."
                        },
                        {
                            "id": "DEV-CMS-GUEST-12",
                            "description": "پیاده‌سازی فرم بازیابی رمز عبور فراموش شده."
                        }
                    ]
                }
            ]
        }
    ],
    "implementationRoadmap": [
        {
            "id": "cms-phase-1-core-setup",
            "step": "فاز ۱ (CMS پایه)",
            "title": "راه‌اندازی هسته CMS و مدیریت محتوا",
            "description": "پیاده‌سازی زیرساخت‌های اصلی CMS شامل احراز هویت، مدیریت کاربران پنل، مدیریت مطالب و دسته‌بندی‌ها.",
            "tasks": [
                {
                    "id": "CMS-T1.1",
                    "relatedRequirementId": "req-admin-user-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-USER-1"
                },
                {
                    "id": "CMS-T1.2",
                    "relatedRequirementId": "req-admin-user-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-USER-2"
                },
                {
                    "id": "CMS-T1.3",
                    "relatedRequirementId": "req-admin-post-category-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-PCAT-1"
                },
                {
                    "id": "CMS-T1.4",
                    "relatedRequirementId": "req-admin-post-category-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-PCAT-2"
                },
                {
                    "id": "CMS-T1.5",
                    "relatedRequirementId": "req-admin-post-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-POST-1"
                },
                {
                    "id": "CMS-T1.6",
                    "relatedRequirementId": "req-admin-post-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-POST-2"
                }
            ]
        },
        {
            "id": "cms-phase-2-media-and-navigation",
            "step": "فاز ۲ (CMS پایه)",
            "title": "مدیریت رسانه و منوهای سایت",
            "description": "پیاده‌سازی قابلیت‌های مدیریت کتابخانه چندرسانه‌ای و ساختار منوهای وب‌سایت.",
            "tasks": [
                {
                    "id": "CMS-T2.1",
                    "relatedRequirementId": "req-admin-multimedia-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-MULT-1"
                },
                {
                    "id": "CMS-T2.2",
                    "relatedRequirementId": "req-admin-multimedia-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-MULT-2"
                },
                {
                    "id": "CMS-T2.3",
                    "relatedRequirementId": "req-admin-navigation-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-NAV-1"
                },
                {
                    "id": "CMS-T2.4",
                    "relatedRequirementId": "req-admin-navigation-mgmt",
                    "relatedDeveloperTaskId": "DEV-CMS-NAV-2"
                }
            ]
        }
    ]
}
```

**دستورالعمل‌های اختصاصی برای پروژه جدید:**

مدل زبانی، لطفاً JSON پایه بالا را برای پروژه جدید زیر گسترش بده:

*   **نام پروژه:** "[عنوان پروژه جدید]"

*   **توضیحات پروژه:** "[توضیحات کامل پروژه]"

**بر اساس اطلاعات پروژه جدید (نام و توضیحات) و با در نظر گرفتن JSON پایه Atfino CMS 3، لطفاً موارد زیر را به صورت خودکار تحلیل و تولید کن:**

1.  **`projectInfo`:** بخش `name` و `description` را با اطلاعات پروژه جدید به‌روزرسانی کن.

2.  **`entities`:**

    *   تمامی موجودیت‌های جدید لازم برای سیستم جدید را به لیست موجودیت‌های پایه **اضافه کن**.

    *   برای هر موجودیت (موجود یا جدید)، آرایه `fields` را با نام فیلدهای عادی (به صورت رشته) و فیلدهای Enum (به صورت شیء با `name`, `isEnum`, `enumName`, `enumValues`) مشخص کن.

    *   آرایه `foreignKeys` را با آبجکت‌هایی شامل `name` (نام فیلد FK) و `references` (شناسه موجودیت مرجع) تکمیل کن. به `baseFields` و `excludeBaseFields` (اگر فیلدهای پایه را استفاده نمی‌کند) توجه کن.

3.  **`userRoles`:**

    *   **نقش‌های موجود Atfino CMS (`role-admin`, `role-guest`) را حفظ کن.** سپس نیازمندی‌های جدید و مرتبط با سیستم جدید را به لیست `requirements` هر یک از این نقش‌ها **اضافه کن**.

    *   **برای هر نیازمندی (موجود یا جدید) که مربوط به پروژه جدید است، یک آرایه جدید به نام `developerTasks` اضافه کن یا آن را کامل کن.** در این آرایه، وظایف توسعه‌دهندگان مرتبط با پیاده‌سازی آن نیازمندی را با `id` (مثلاً `DEV-REQ-ADM-NEWREQ-1`) و `description` (به زبان فارسی) به صورت کامل تعریف کن.

    *   در صورت نیاز به **نقش‌های کاربری جدید** آن‌ها را به لیست نقش‌ها **اضافه کن**.

    *   برای هر نقش جدید، `name`، `description` و `needsPanel` (true/false) را مشخص کن.

    *   لیست `requirements` هر نقش جدید را با جزئیات کامل (شامل `areaName`, `controllerName`, `actions`, `views`, `primaryEntityId` و آرایه `developerTasks`) تعریف کن. (برای منطق‌های بک‌اندی که مستقیماً به UI متصل نیستند، `controllerName` را `N/A (Service/Backend)` و `areaName` و `views` را `null` یا خالی قرار بده).

4.  **`implementationRoadmap`:**

    *   مدل زبانی باید **این بخش نمونه را به طور کامل با یک نقشه راه جدید** برای پیاده‌سازی نیازمندی‌های **پروژه جدید** جایگزین کند.

    *   ساختار نقشه راه باید شامل آرایه‌ای از آبجکت‌ها باشد که هر آبجکت شامل `id`, `step`, `title`, `description` و `tasks` است.

    *   این نقشه راه باید **فقط نیازمندی‌های جدیدی را که برای پروژه تعریف کرده‌ای** (چه نیازمندی‌های کاملاً جدید و چه نیازمندی‌های اضافه شده به نقش‌های موجود) شامل شود. نیازمندی‌های مربوط به خود Atfino CMS را در اینجا لحاظ نکن.

    *   **هر `task` در نقشه راه باید یک ارجاع باشد، نه تعریف مجدد.** لذا، هر `task` باید شامل `id` (شناسه وظیفه در نقشه راه، که می‌تواند یک شماره ترتیب باشد)، `relatedRequirementId` (شناسه نیازمندی والد که وظیفه توسعه‌دهنده به آن تعلق دارد) و `relatedDeveloperTaskId` (شناسه وظیفه توسعه‌دهنده درون آرایه `developerTasks` آن نیازمندی) باشد.

    *   توضیحات هر گام (`description` فاز) نیز باید بر پیاده‌سازی این نیازمندی‌های جدید تمرکز داشته باشد.

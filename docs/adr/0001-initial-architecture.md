# ADR-001: معماری اولیه و ساختار Repository

* **وضعیت:** Proposed
* **تاریخ:** 2026-09-29

## زمینه

Notification Center یک پلتفرم متمرکز برای ارسال اعلان است. MVP باید یک مسیر کامل و ساده برای دریافت، پردازش و ارسال Notification فراهم کند و در ادامه قابلیت توسعه برای DevOps/DevSecOps را داشته باشد.

## تصمیم

### معماری

از یک معماری شامل **Laravel API + Go Worker** استفاده می‌کنیم:

```text
Client
  |
  v
Laravel API
  |
  v
Redis Queue
  |
  v
Go Worker
  |
  +--> Email
  |
  +--> Bale
  |
  v
PostgreSQL
```

* **Laravel:** API، احراز هویت، مدیریت Notification و قرار دادن Job در Queue
* **Go:** پردازش Job و ارسال Notification
* **Redis:** Queue
* **PostgreSQL:** داده‌های دائمی
* **Email و Bale:** کانال‌های اولیه

### Repository

از **Monorepo** استفاده می‌کنیم:

```text
notification-center/
├── README.md
├── docs/
│   └── adr/
├── apps/
│   ├── api/
│   └── worker/
├── docker/
└── .gitignore
```

Docker و CI/CD در مراحل بعدی اضافه می‌شوند.

## گزینه‌های بررسی‌شده

### Laravel-only

ساده‌تر و سریع‌تر بود، اما Go Worker و تجربه معماری چندسرویسی را حذف می‌کرد.

### Repositoryهای جدا

برای تیم دو نفره نسبت به Monorepo سربار بیشتری ایجاد می‌کند.

### Kafka

برای MVP فعلی ضروری نیست و نسبت به Redis پیچیدگی عملیاتی بیشتری دارد. در صورت ایجاد نیاز واقعی به Event Streaming بازبینی می‌شود.

## پیامد

این معماری پیچیدگی بیشتری از یک Laravel Application ساده دارد، اما مرز مشخصی بین API و پردازش پس‌زمینه ایجاد می‌کند و بستر مناسبی برای Docker، CI/CD و توسعه‌های بعدی فراهم می‌کند.

در صورت افزایش قابل‌توجه پیچیدگی، حجم یا نیازهای Queue، این تصمیم بازبینی خواهد شد.

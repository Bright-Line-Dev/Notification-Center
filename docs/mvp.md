# Notification Center — MVP Scope

## هدف

ساخت یک سرویس متمرکز برای دریافت و ارسال Notification از طریق API، با پردازش غیرهمزمان و ثبت وضعیت ارسال.

MVP باید یک مسیر کامل و قابل استفاده از **API تا تحویل Notification** داشته باشد.

## MVP شامل

### 1. Application Management

* ثبت Application
* ایجاد و مدیریت API Key
* فعال/غیرفعال کردن Application

### 2. Notification API

* ارسال Notification از طریق API
* تعیین Channel
* تعیین گیرنده
* تعیین محتوای Notification
* دریافت شناسه Notification

### 3. Queue & Processing

```text
Client
  ↓
Laravel API
  ↓
Redis Queue
  ↓
Go Worker
  ↓
Provider
```

* قرار دادن Notification در Queue
* پردازش توسط Go Worker
* مدیریت موفقیت و خطا

### 4. Notification Channels

کانال‌های اولیه:

* Email
* Bale

ساختار Worker باید به‌گونه‌ای باشد که اضافه‌کردن Channel جدید در آینده بدون تغییر اساسی در معماری امکان‌پذیر باشد.

### 5. Delivery Status

برای هر Notification وضعیت ارسال نگهداری شود.

وضعیت‌های اولیه:

```text
pending
processing
sent
failed
```

در صورت نیاز در طول توسعه وضعیت‌های بیشتری اضافه می‌شوند.

### 6. Retry

برای خطاهای قابل Retry، ارسال مجدداً تلاش شود.

در MVP یک مکانیزم ساده و محدود برای Retry کافی است.

### 7. Testing

حداقل تست‌های لازم برای:

* Authentication
* Notification API
* Queueing
* Status handling
* موفقیت و خطای Provider

## خارج از محدوده MVP

موارد زیر عمداً در MVP پیاده‌سازی نمی‌شوند:

* Kafka
* Kubernetes
* Terraform
* Advanced Monitoring
* Analytics و Reporting
* Dashboard کامل
* Scheduling پیچیده
* Template Engine پیشرفته
* تعداد زیاد Notification Provider
* Multi-tenancy پیچیده
* قابلیت‌های پیشرفته مدیریت کاربران
* High Availability و Distributed Deployment

## معیار پایان MVP

MVP زمانی کامل است که بتوان:

```text
Register Application
        ↓
Authenticate with API Key
        ↓
Create Notification
        ↓
Queue Job
        ↓
Process with Go Worker
        ↓
Send via Email or Bale
        ↓
Store Delivery Result
        ↓
Query Notification Status
```

و مسیر بالا برای هر دو Channel اولیه، با تست‌های اصلی، قابل اجرا باشد.

## Post-MVP

پس از تکمیل MVP، توسعه به‌ترتیب نیاز پروژه می‌تواند شامل موارد زیر باشد:

1. Docker
2. CI/CD
3. Monitoring & Logging
4. Infrastructure as Code
5. Kubernetes
6. Security hardening
7. Threat Modeling
8. Channelهای بیشتر

این موارد تا زمانی که MVP کامل نشده، نباید وارد Scope اصلی شوند.

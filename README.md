# Django Facebook CAPI Dashboard

**A reusable Django package to fb Facebook (Meta) Conversions API events server-side, with built-in logging and admin dashboard.**

---

## 📦 Installation

```bash
pip install django-facebook-capi
```

---

## ⚙️ Setup

### 1. Add to `INSTALLED_APPS`

```python
INSTALLED_APPS = [
    ...
    'django_facebook_capi',
]
```

### 2. Add Required Settings

In your `settings.py`, add:

```python
FACEBOOK_PIXEL_ID = 'your_facebook_pixel_id'
FACEBOOK_CAPI_ACCESS_TOKEN = 'your_capi_access_token'
```

You can generate these from your [Meta Events Manager](https://business.facebook.com/events_manager2/).

### 3. Migrate Database

```bash
python manage.py migrate django_facebook_capi
```

This will create a model to log all fbed events in the admin.

### 4. Optional: Enable Django Admin

Ensure `django.contrib.admin` is enabled and your superuser is created:

```bash
python manage.py createsuperuser
```

Visit `/admin/` and look for **Facebook Event Logs**.

---

## 🚀 Usage

### Import utilities into your views

```python
from django_facebook_capi.capi_utils import (
    fb_page_view,
    fb_view_content,
    fb_lead_form,
    fb_add_to_cart,
    fb_initiate_checkout,
    fb_purchase,
    fb_custom_event,
)
```

---

### 📝 Event Tracking Examples

#### ✅ PageView

```python
fb_page_view(request)
```

#### 👀 ViewContent

```python
fb_view_content(
    request,
    content_name="Red T-Shirt",
    content_category="Apparel",
    content_ids=["sku123"]
)
```

#### 📝 Lead Form Submission

```python
fb_lead_form_submission(request)
```

#### 🛒 Add to Cart

```python
fb_add_to_cart(
    request,
    content_ids=["sku123"],
    value=799,
    currency='INR'
)
```

#### 💳 Initiate Checkout

```python
fb_initiate_checkout(
    request,
    content_ids=["sku123", "sku124"],
    value=1598,
    currency='INR'
)
```

#### 💰 Purchase

```python
fb_purchase(
    request,
    content_ids=["sku123", "sku124"],
    value=1598,
    currency='INR',
    transaction_id='txn_001'
)
```

#### ⚙️ Custom Event

```python
fb_custom_event(
    request,
    event_name="StartTrial",
    custom_data={"plan": "Pro", "value": 0}
)
```

---

## 📊 Logging & Admin Panel

All events sent via this package are **logged into your database** and can be viewed in the Django Admin dashboard. Each log includes:

- Event name
- Response status code
- Response from Meta
- Source URL
- Timestamp

---

## 🧠 Notes

- You must **share your Meta Pixel's Business Settings with your CAPI token** if using a system user.
- Make sure `_fbc` and `_fbp` cookies are available in requests for optimal matching.
- Email and phone values will be **hashed** with SHA256 before sending.

---

## 💡 Roadmap

- [ ] Retry failed events
- [ ] Custom signal support
- [ ] Admin filtering by status code
- [ ] Retry/resend via admin actions

---

## 🧑‍💻 Contributing

1. Fork the repo
2. Make changes
3. Submit a PR

---

## 📝 License

MIT @ 2025
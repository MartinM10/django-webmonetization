# Django Web Monetization

[![PyPI version](https://badge.fury.io/py/django-webmonetization-MartinM10.svg)](https://badge.fury.io/py/django-webmonetization-MartinM10)
[![Python Versions](https://img.shields.io/badge/python-3.7%2B-blue.svg)](https://www.python.org/downloads/release/python-370/)
[![Django Versions](https://img.shields.io/badge/django-3.2%2B-blue.svg)](https://docs.djangoproject.com/es/5.1/releases/3.2/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

A Django package that makes it easy to integrate the [Web Monetization](https://webmonetization.org/) specification into web applications. It enables developers to monetize their websites through real-time payments using the [Interledger Protocol (ILP)](https://interledger.org/).

## Features

- 🚀 Middleware to automatically add the payment pointer to HTTP headers
- 🎯 Template tag to insert the monetization meta tag in templates
- ⚙️ Simple configuration through settings.py
- 🔒 Compatible with Django 3.2+
- 📦 Easy installation with pip

## Resources

- [Web Monetization Specification](https://webmonetization.org/specification/)
- [Web Monetization Documentation](https://webmonetization.org/)
- [Interledger Protocol](https://interledger.org/)

## Installation

```bash
pip install django-webmonetization-MartinM10
```

## Configuration

1. Add 'django_webmonetization' to INSTALLED_APPS in settings.py:

```python
INSTALLED_APPS = [
    ...
    'django_webmonetization',
]
```

2. Configure your payment pointer in settings.py:

```python
WEBMONETIZATION_PAYMENT_POINTER = '$ilp.example.com/your-payment-pointer'
```

3. (Optional) Add the middleware to MIDDLEWARE in settings.py:

```python
MIDDLEWARE = [
    ...
    'django_webmonetization.middleware.WebMonetizationMiddleware',
]
```

## Usage

### In Django Templates

```html
{% load webmonetization %}
<!DOCTYPE html>
<html>
<head>
    {% webmonetization_meta %}
    <title>My Monetized Website</title>
</head>
<body>
    <h1>Welcome to my website</h1>
    <p>This site is monetized with Web Monetization</p>
</body>
</html>
```

### HTTP Headers Verification

The middleware automatically adds the `Web-Monetization-Pointer` header to all HTTP responses. You can verify it with curl:

```bash
curl -I https://your-site.com
```

You should see something like:
```
HTTP/1.1 200 OK
...
Web-Monetization-Pointer: $ilp.example.com/your-payment-pointer
```

## Integration Examples

### 1. Basic Monetization

```python
# settings.py
WEBMONETIZATION_PAYMENT_POINTER = '$ilp.example.com/basic'

# views.py
from django.shortcuts import render

def home(request):
    return render(request, 'home.html')
```

```html
<!-- templates/home.html -->
{% load webmonetization %}
<!DOCTYPE html>
<html>
<head>
    {% webmonetization_meta %}
</head>
<body>
    <h1>Home Page</h1>
</body>
</html>
```

## Requirements

### Main Dependencies
- Python 3.7+
- Django 3.2+

### Development Dependencies
- pytest>=7.0.0
- pytest-cov>=4.0.0

## Contributing

Contributions are welcome! Please feel free to submit a pull request.

## License

MIT License - see the [LICENSE](LICENSE) file for details.

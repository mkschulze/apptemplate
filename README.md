# Deloitte Flask App Template 🚀

A clean Flask application template with **Deloitte branding** – ready to use as a starting point for new web applications.

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-3.0+-green.svg)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-purple.svg)

---

## ✨ Features

- ✅ **Deloitte Branding** – Logo, Colors, Icons included
- ✅ **User Authentication** – Login/Logout with Flask-Login
- ✅ **Admin Dashboard** – Basic admin interface
- ✅ **Multi-Language** – German & English support
- ✅ **Audit Logging** – Track user actions
- ✅ **Responsive Design** – Bootstrap 5
- ✅ **Error Pages** – Custom 404/500 pages

---

## 🚀 Quick Start

### 1. Clone & Setup

```bash
# Copy the template folder to your new project
cp -r apptemplate/ /path/to/your/newproject/
cd /path/to/your/newproject/

# Install dependencies
pipenv install

# Activate virtual environment
pipenv shell
```

### 2. Configure Your App

Edit `config.py`:
```python
APP_NAME = 'Your App Name'
APP_VERSION = '1.0.0'
```

### 3. Initialize Database

```bash
python init_db.py
```

### 4. Run Development Server

```bash
flask run --debug
```

Open [http://localhost:5000](http://localhost:5000)

---

## 🔐 Default Login

| Role | Email | Password |
|------|-------|----------|
| Admin | `admin@example.com` | `admin123` |
| User | `user@example.com` | `user123` |

---

## 📁 Project Structure

```
apptemplate/
├── app.py              # Flask Application & Routes
├── config.py           # Configuration (APP_NAME, etc.)
├── models.py           # SQLAlchemy Models (User, AuditLog)
├── translations.py     # DE/EN Translations
├── init_db.py          # Database Setup Script
├── Pipfile             # Dependencies
│
├── templates/
│   ├── base.html       # Base Layout with Deloitte Branding
│   ├── index.html      # Home Page
│   ├── login.html      # Login Page
│   ├── admin/
│   │   ├── dashboard.html
│   │   └── users.html
│   └── errors/
│       ├── 404.html
│       └── 500.html
│
├── static/
│   ├── favicon/                    # Favicons
│   ├── Deloitte-Master-Logo/       # Deloitte Logo
│   ├── Deloitte Special Case Web Icons/  # Icon Font
│   └── Color Guide/                # Color Guidelines
│
└── instance/
    └── app.db          # SQLite Database (auto-created)
```

---

## 🎨 Deloitte Colors

| Color | Hex | CSS Variable |
|-------|-----|--------------|
| Black | #000000 | `--del-black` |
| Green | #86BC25 | `--del-green` |
| Teal | #0097A9 | `--del-teal-light` |
| Blue | #00A3E0 | `--del-blue-light` |
| Red | #DA291C | `--del-red` |
| Orange | #ED8B00 | `--del-orange` |
| Yellow | #FFCD00 | `--del-yellow` |

---

## 🔧 Customization Guide

### Add New Routes

In `app.py`:
```python
@app.route('/my-route')
@login_required
def my_route():
    return render_template('my_template.html')
```

### Add New Models

In `models.py`:
```python
class MyModel(db.Model):
    __tablename__ = 'my_model'
    
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    created_at = db.Column(db.DateTime, default=datetime.utcnow)
```

### Add Translations

In `translations.py`:
```python
TRANSLATIONS = {
    # ...existing translations...
    'my_key': {'de': 'Deutscher Text', 'en': 'English Text'},
}
```

Use in templates: `{{ t('my_key') }}`

---

## 📋 CLI Commands

```bash
# Initialize database
flask initdb

# Create admin user
flask createadmin

# Run development server
flask run --debug
```

---

## 🚧 What to Build Next

- [ ] Add your custom models
- [ ] Create CRUD routes
- [ ] Build your templates
- [ ] Add more translations
- [ ] Implement your business logic

---

## 📄 License

Internal use only – Deloitte branding assets included.

---

## 📬 Based on

This template is derived from [TaxTechCompass](https://github.com/mkschulze/TaxTechCompass).

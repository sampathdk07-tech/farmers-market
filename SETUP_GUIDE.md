# Farmers Market - Complete Setup & Run Guide

## Prerequisites

Before you start, make sure you have installed:
- **Python 3.8+** - [Download](https://www.python.org/downloads/)
- **Git** - [Download](https://git-scm.com/)
- **pip** - Usually comes with Python

**Verify installations:**
```bash
python --version
git --version
pip --version
```

---

## Step 1: Clone the Repository

```bash
# Clone the project
git clone https://github.com/sampathdk07-tech/farmers-market.git

# Navigate to project directory
cd farmers-market
```

---

## Step 2: Create Virtual Environment

A virtual environment isolates project dependencies from your system Python.

### On Windows:
```bash
python -m venv venv
venv\Scripts\activate
```

### On macOS/Linux:
```bash
python3 -m venv venv
source venv/bin/activate
```

**You should see `(venv)` at the beginning of your terminal line**, indicating the virtual environment is active.

---

## Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

**What gets installed:**
- Django 4.2.7 - Web framework
- Pillow 10.1.0 - Image handling
- python-decouple 3.8 - Environment variables

Wait for installation to complete (you'll see "Successfully installed...").

---

## Step 4: Create Database & Run Migrations

Migrations create database tables automatically.

```bash
# Create migrations for the app
python manage.py makemigrations

# Apply migrations to database
python manage.py migrate
```

**Output should look like:**
```
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, market, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  ...
```

---

## Step 5: Create Superuser (Admin Account)

The superuser can access Django admin panel.

```bash
python manage.py createsuperuser
```

**Follow the prompts:**
```
Username: admin
Email: admin@example.com
Password: ••••••••
Password (again): ••••••••
Superuser created successfully.
```

---

## Step 6: Run Development Server

```bash
python manage.py runserver
```

**Expected output:**
```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
September 10, 2026 - 10:30:00
Django version 4.2.7, using settings 'farmersmarket.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

---

## Step 7: Access the Application

### Open your browser and visit:
- **Home Page**: http://127.0.0.1:8000/
- **Register**: http://127.0.0.1:8000/register/
- **Login**: http://127.0.0.1:8000/login/
- **Admin Panel**: http://127.0.0.1:8000/admin/

---

## How to Use the Application

### 🌾 For Sellers:

1. **Register**
   - Go to `/register/`
   - Select "Seller" role
   - Fill in username, email, password
   - Click "Sign up"

2. **Login**
   - Go to `/login/`
   - Select "Seller" role
   - Enter credentials
   - Click "Login"

3. **Add Products**
   - After login, you'll be on `/dashboard/`
   - Click "Add Product"
   - Fill in:
     - Product Name
     - Description
     - Category (Vegetables, Fruits, etc.)
     - Price
     - Quantity
     - Upload Product Image
   - Click "Add"

4. **Manage Products**
   - View all your products on Dashboard
   - Edit or Delete products as needed

5. **Chat with Buyers**
   - Go to `/chat/` to see all conversations
   - Click on buyer name to open chat
   - Send/receive messages about products

### 👤 For Buyers:

1. **Register**
   - Go to `/register/`
   - Select "Buyer" role
   - Fill in username, email, password
   - Click "Sign up"

2. **Login**
   - Go to `/login/`
   - Select "Buyer" role
   - Enter credentials
   - Click "Login"

3. **Browse Products**
   - After login, you'll see `/marketplace/`
   - View all products from all sellers
   - Use Search to find products
   - Filter by Category

4. **View Product Details**
   - Click on any product to see full details
   - See seller information
   - View price and quantity

5. **Chat with Sellers**
   - Click "Chat with Seller" button on product page
   - Send your first message
   - Go to `/chat/` to see all conversations
   - Continue chatting with seller

---

## Project Structure

```
farmers-market/
│
├── manage.py                 # Django management script
├── requirements.txt          # Python dependencies
├── db.sqlite3               # SQLite Database (auto-created)
├── PROJECT_SYNOPSIS.md      # Project documentation
│
├── farmersmarket/           # Main Django Project
│   ├── __init__.py
│   ├── settings.py          # Project configuration
│   ├── urls.py              # Main URL routing
│   ├── wsgi.py              # WSGI config
│
├── market/                  # Main Django App
│   ├── migrations/          # Database migrations
│   ├── __init__.py
│   ├── admin.py            # Django admin configuration
│   ├── apps.py             # App configuration
│   ├── models.py           # Database models (User, Product, Message)
│   ├── views.py            # Business logic
│   ├── forms.py            # Form handling
│   ├── urls.py             # App URL routing
│
├── templates/              # HTML templates
│   ├── base.html
│   ├── home.html
│   ├── login.html
│   ├── register.html
│   ├── seller_dashboard.html
│   ├── add_product.html
│   ├── edit_product.html
│   ├── marketplace.html
│   ├── product_detail.html
│   ├── chat_list.html
│   ├── chat_detail.html
│
├── static/                 # CSS, JS, Images
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── script.js
│
└── media/                  # User uploads
    └── products/
    └── profiles/
```

---

## Database Models

### UserProfile
```
- user (User Account)
- user_type (Seller/Buyer)
- phone_number
- address
- profile_image
- created_at
```

### Product
```
- seller (Foreign Key to User)
- product_name
- description
- category (Vegetables, Fruits, Grains, etc.)
- price
- quantity
- product_image
- created_at
- updated_at
- is_active
```

### Message
```
- sender (Foreign Key to User)
- receiver (Foreign Key to User)
- product (Foreign Key to Product - optional)
- message_text
- timestamp
- is_read
```

---

## Common Django Commands

```bash
# Create new migrations (after model changes)
python manage.py makemigrations

# Apply migrations to database
python manage.py migrate

# Create a superuser for admin
python manage.py createsuperuser

# Run development server
python manage.py runserver

# Stop server
CTRL + C

# Access Django shell
python manage.py shell

# Create new app (if needed)
python manage.py startapp appname

# Collect static files (for production)
python manage.py collectstatic

# Reset database (deletes all data)
python manage.py flush
```

---

## Troubleshooting

### Issue: "No module named 'django'"
**Solution:** Make sure virtual environment is activated
```bash
# Windows
venv\Scripts\activate

# macOS/Linux
source venv/bin/activate
```

### Issue: "python: command not found"
**Solution:** Use `python3` instead on macOS/Linux
```bash
python3 manage.py runserver
```

### Issue: Port 8000 already in use
**Solution:** Use a different port
```bash
python manage.py runserver 8001
```

### Issue: Image upload not working
**Solution:** Make sure `media` folder exists
```bash
mkdir media
mkdir media/products
mkdir media/profiles
```

### Issue: Database error
**Solution:** Reset database and migrations
```bash
# Delete db.sqlite3
rm db.sqlite3

# Recreate migrations
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

---

## How to Stop the Server

Press `CTRL + C` in your terminal

```
^CKeyboardInterrupt
```

---

## Next Steps

1. ✅ Explore Django Admin: http://127.0.0.1:8000/admin/
2. ✅ Add sample products as seller
3. ✅ Browse marketplace as buyer
4. ✅ Test messaging system
5. ✅ Customize styling in `static/css/style.css`
6. ✅ Add more features as needed

---

## Production Deployment

For deploying to production:
1. Set `DEBUG = False` in settings.py
2. Change `SECRET_KEY` to a secure random value
3. Set `ALLOWED_HOSTS` to your domain
4. Use a production database (PostgreSQL recommended)
5. Use Gunicorn or uWSGI as WSGI server
6. Deploy on Heroku, PythonAnywhere, AWS, or DigitalOcean

---

## Support & Help

**For Django Documentation**: https://docs.djangoproject.com/
**For Python**: https://docs.python.org/
**For Issues**: Check GitHub repository issues

---

## Summary

```bash
# Quick Setup (Copy & Paste)
git clone https://github.com/sampathdk07-tech/farmers-market.git
cd farmers-market
python -m venv venv

# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver

# Open browser: http://127.0.0.1:8000/
```

---

**Happy Coding! 🚀**

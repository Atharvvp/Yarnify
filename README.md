# 🧶 Yarnify - Luxury Crochet E-Commerce Platform

![Version](https://img.shields.io/badge/version-1.0.0-pink)
![PHP](https://img.shields.io/badge/PHP-7.4+-D85D7A)
![MySQL](https://img.shields.io/badge/MySQL-5.7+-FFC0CB)
![License](https://img.shields.io/badge/license-Proprietary-pink)

> A premium, handcrafted e-commerce platform for luxury crochet products. Built with love using PHP, MySQL, and pure vanilla JavaScript.

![Yarnify Preview](https://via.placeholder.com/1200x400/FFE4E9/D85D7A?text=Yarnify+-+Handmade+Luxury)

---

## 🌸 Table of Contents

- [Features](#-features)
- [Demo](#-demo)
- [Technology Stack](#-technology-stack)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [API Endpoints](#-api-endpoints)
- [Security](#-security)
- [Customization](#-customization)
- [Deployment](#-deployment)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)
- [Support](#-support)

---

## ✨ Features

### 🎨 **Premium Design**
- **Luxury Pink Aesthetic** - Carefully crafted color palette with 6+ shades of pink
- **Glassmorphism UI** - Modern frosted glass navigation and cards
- **Smooth Animations** - Floating products, scroll reveals, hover effects
- **Wave Dividers** - Elegant section transitions
- **Responsive Design** - Perfect on desktop, tablet, and mobile
- **Instagram-Worthy** - Designed to attract and engage customers

### 🛍️ **Customer Features**
- **Product Browsing** - Filter by category, price, trending, bestsellers
- **Advanced Search** - Real-time search with instant results
- **Shopping Cart** - Live updates, quantity controls, session persistence
- **Wishlist System** - Save favorite items for later
- **User Accounts** - Registration, login, profile management
- **Order Tracking** - Complete order history and status updates
- **Product Reviews** - 5-star rating system with comments
- **Secure Checkout** - Multi-step checkout with form validation
- **Payment Options** - Cash on Delivery, Card (ready for integration)

### 👑 **Admin Panel**
- **Dashboard Analytics** - Sales, orders, customers, revenue metrics
- **Product Management** - Add, edit, delete products with ease
- **Inventory Control** - Stock tracking and low-stock alerts
- **Order Management** - Update order status (Pending → Delivered)
- **Customer Overview** - View customer data and purchase history
- **Review Moderation** - Approve or reject customer reviews
- **Sales Reports** - Visual charts and statistics

### 🔐 **Security Features**
- **Password Hashing** - BCrypt encryption (cost: 10)
- **SQL Injection Protection** - Prepared statements throughout
- **CSRF Protection** - Token-based form validation
- **Session Security** - Secure session handling
- **Input Sanitization** - All user inputs cleaned
- **Role-Based Access** - Customer vs Admin permissions
- **XSS Prevention** - Output escaping with htmlspecialchars

### 📱 **Technical Features**
- **SEO Optimized** - Semantic HTML5, meta tags ready
- **Performance** - Lazy loading, optimized queries
- **Accessibility** - WCAG 2.1 compliant
- **Progressive Enhancement** - Works without JavaScript
- **Cross-Browser** - Chrome, Firefox, Safari, Edge compatible
- **No Dependencies** - Pure vanilla JavaScript, no frameworks

---

## 🎬 Demo

### Live Preview
```
Homepage: https://your-domain.com
Admin Panel: https://your-domain.com/admin
```

### Demo Credentials
```
Customer Account:
Email: demo@customer.com
Password: demo123

Admin Account:
Email: admin@crochetluxury.com
Password: admin123
```

⚠️ **Important:** Change admin password immediately after installation!

---

## 💻 Technology Stack

### Backend
- **PHP 7.4+** - Server-side scripting
- **MySQL 5.7+** - Relational database
- **Apache/Nginx** - Web server

### Frontend
- **HTML5** - Semantic markup
- **CSS3** - Custom properties, Grid, Flexbox
- **JavaScript (ES6+)** - Vanilla JS, no frameworks
- **SVG** - Scalable vector graphics

### Fonts
- **Playfair Display** - Elegant serif for headings
- **Poppins** - Modern sans-serif for body text

### Tools & Libraries
- **BCrypt** - Password hashing
- **MySQLi** - Database connectivity
- **Session Management** - User authentication

---

## 🚀 Installation

### Prerequisites

Ensure you have the following installed:

```bash
✅ PHP 7.4 or higher
✅ MySQL 5.7 or higher
✅ Apache/Nginx web server
✅ Composer (optional)
✅ Git (optional)
```

### Step 1: Download Files

**Option A: Download ZIP**
```bash
# Extract the ZIP file to your web server directory
unzip crochet-luxury-shop.zip -d /var/www/html/yarnify
```

**Option B: Git Clone** (if using version control)
```bash
cd /var/www/html
git clone https://github.com/yourusername/yarnify.git
cd yarnify
```

### Step 2: Create Database

```bash
# Login to MySQL
mysql -u root -p

# Create database
CREATE DATABASE yarnify CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# Create user (recommended)
CREATE USER 'yarnify_user'@'localhost' IDENTIFIED BY 'your_secure_password';
GRANT ALL PRIVILEGES ON yarnify.* TO 'yarnify_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### Step 3: Import Database Schema

```bash
mysql -u yarnify_user -p yarnify < database.sql
```

### Step 4: Configure Database Connection

Edit `config/db.php`:

```php
<?php
define('DB_HOST', 'localhost');
define('DB_USER', 'yarnify_user');
define('DB_PASS', 'your_secure_password');
define('DB_NAME', 'yarnify');
```

### Step 5: Set Permissions

```bash
# Make directories writable
chmod 755 assets/images/products
chmod 640 config/db.php

# Set proper ownership
chown -R www-data:www-data /var/www/html/yarnify
```

### Step 6: Configure Web Server

**Apache (.htaccess)**

Create `.htaccess` in root:

```apache
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /yarnify/
    
    # Prevent directory browsing
    Options -Indexes
    
    # Protect config files
    <FilesMatch "^(config|database)\.">
        Require all denied
    </FilesMatch>
</IfModule>

# Compression
<IfModule mod_deflate.c>
    AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript
</IfModule>

# Browser caching
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType image/jpg "access plus 1 year"
    ExpiresByType image/jpeg "access plus 1 year"
    ExpiresByType image/png "access plus 1 year"
    ExpiresByType text/css "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 month"
</IfModule>
```

**Nginx Configuration**

Add to your nginx config:

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/html/yarnify;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\. {
        deny all;
    }
}
```

### Step 7: Test Installation

Visit: `http://localhost/yarnify` or `http://your-domain.com`

You should see the beautiful pink homepage with the floating hero product!

---

## ⚙️ Configuration

### Database Configuration

**File:** `config/db.php`

```php
// Database settings
define('DB_HOST', 'localhost');      // Database host
define('DB_USER', 'yarnify_user');   // Database username
define('DB_PASS', 'your_password');  // Database password
define('DB_NAME', 'yarnify');        // Database name

// Security settings
define('SESSION_LIFETIME', 3600);    // Session timeout (1 hour)
define('CSRF_TOKEN_LENGTH', 32);     // CSRF token length
```

### Email Configuration (Optional)

For order confirmations and notifications, configure SMTP in `config/email.php`:

```php
define('SMTP_HOST', 'smtp.gmail.com');
define('SMTP_PORT', 587);
define('SMTP_USER', 'your-email@gmail.com');
define('SMTP_PASS', 'your-app-password');
define('FROM_EMAIL', 'noreply@yarnify.com');
define('FROM_NAME', 'Yarnify');
```

### Payment Gateway Integration

**For Stripe:**
1. Get API keys from https://dashboard.stripe.com
2. Add to `config/payment.php`:

```php
define('STRIPE_PUBLIC_KEY', 'pk_test_xxxxx');
define('STRIPE_SECRET_KEY', 'sk_test_xxxxx');
```

**For PayPal:**
```php
define('PAYPAL_CLIENT_ID', 'your_client_id');
define('PAYPAL_SECRET', 'your_secret');
define('PAYPAL_MODE', 'sandbox'); // or 'live'
```

---

## 📖 Usage

### Customer Journey

1. **Browse Products** → Visit shop.php or collections.php
2. **View Details** → Click any product to see full details
3. **Add to Cart** → Select quantity and add to cart
4. **Save to Wishlist** → Heart icon to save for later
5. **Register/Login** → Create account or login
6. **Checkout** → Enter shipping details
7. **Place Order** → Complete purchase
8. **Track Order** → View status in profile

### Admin Workflow

1. **Login** → `/admin/dashboard.php`
2. **Add Products** → `/admin/add-product.php`
3. **Manage Orders** → Update status from pending → delivered
4. **Moderate Reviews** → Approve/reject customer reviews
5. **View Analytics** → Monitor sales and performance

### Adding Products

```php
// Via Admin Panel:
1. Go to Admin → Add Product
2. Fill in details:
   - Name
   - Description
   - Category (bags, tops, accessories, plushies)
   - Price
   - Stock quantity
   - Mark as trending/bestseller
3. Click "Add Product"
```

### Managing Orders

```php
// Update order status:
1. Admin → Orders
2. Select order
3. Change status dropdown:
   - Pending
   - Processing
   - Shipped
   - Delivered
   - Cancelled
4. Status auto-saves
```

---

## 📁 Project Structure

```
yarnify/
│
├── 📄 index.php                    # Homepage with hero
├── 📄 shop.php                     # Product listing
├── 📄 product.php                  # Product details
├── 📄 cart.php                     # Shopping cart
├── 📄 checkout.php                 # Checkout process
├── 📄 order-success.php            # Order confirmation
├── 📄 wishlist.php                 # Saved products
├── 📄 profile.php                  # User dashboard
├── 📄 collections.php              # Category browser
├── 📄 about.php                    # About page
├── 📄 reviews.php                  # Customer reviews
├── 📄 search.php                   # Search results
├── 📄 login.php                    # User login
├── 📄 register.php                 # Registration
├── 📄 logout.php                   # Logout handler
│
├── 📂 config/
│   ├── db.php                      # Database config
│   ├── email.php                   # Email config (optional)
│   └── payment.php                 # Payment config (optional)
│
├── 📂 admin/
│   ├── dashboard.php               # Admin dashboard
│   ├── products.php                # Product management
│   ├── add-product.php             # Add products
│   ├── orders.php                  # Order management
│   ├── customers.php               # Customer overview
│   ├── reviews.php                 # Review moderation
│   ├── sidebar.php                 # Admin navigation
│   └── admin-style.css             # Admin styles
│
├── 📂 assets/
│   ├── 📂 css/
│   │   └── style.css               # Main stylesheet (3,500+ lines)
│   ├── 📂 js/
│   │   └── main.js                 # JavaScript (500+ lines)
│   └── 📂 images/
│       ├── 📂 products/            # Product images
│       └── 📂 icons/               # Site icons
│
├── 📂 handlers/
│   ├── cart-handler.php            # Cart AJAX operations
│   ├── wishlist-handler.php        # Wishlist AJAX operations
│   └── submit-review.php           # Review submission
│
├── 📄 database.sql                 # Database schema
├── 📄 .htaccess                    # Apache config
├── 📄 README.md                    # This file
└── 📄 LICENSE                      # License file
```

---

## 🗄️ Database Schema

### Tables Overview

```sql
-- 7 Tables with relationships:
1. users          (Customers & Admins)
2. products       (Product catalog)
3. orders         (Customer orders)
4. order_items    (Order line items)
5. wishlist       (Saved products)
6. reviews        (Product reviews)
7. coupons        (Discount codes)
```

### Users Table

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    role ENUM('customer', 'admin') DEFAULT 'customer',
    status ENUM('active', 'blocked') DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Products Table

```sql
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(200) NOT NULL,
    description TEXT,
    category ENUM('bags', 'tops', 'accessories', 'plushies') NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    stock INT DEFAULT 0,
    image VARCHAR(255),
    is_trending BOOLEAN DEFAULT FALSE,
    is_bestseller BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Orders Table

```sql
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    total_amount DECIMAL(10, 2) NOT NULL,
    discount_amount DECIMAL(10, 2) DEFAULT 0,
    final_amount DECIMAL(10, 2) NOT NULL,
    status ENUM('pending', 'processing', 'shipped', 'delivered', 'cancelled') DEFAULT 'pending',
    shipping_name VARCHAR(100) NOT NULL,
    shipping_email VARCHAR(100) NOT NULL,
    shipping_phone VARCHAR(20) NOT NULL,
    shipping_address TEXT NOT NULL,
    shipping_city VARCHAR(100) NOT NULL,
    shipping_state VARCHAR(100) NOT NULL,
    shipping_zip VARCHAR(20) NOT NULL,
    payment_method VARCHAR(50) DEFAULT 'COD',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

### Relationships

```
users (1) ←→ (many) orders
users (1) ←→ (many) wishlist
users (1) ←→ (many) reviews
products (1) ←→ (many) order_items
products (1) ←→ (many) wishlist
products (1) ←→ (many) reviews
orders (1) ←→ (many) order_items
```

---

## 🔌 API Endpoints

### Cart Operations

**Add to Cart**
```javascript
POST /cart-handler.php
{
    action: "add",
    product_id: 123,
    quantity: 2
}
```

**Update Quantity**
```javascript
POST /cart-handler.php
{
    action: "update",
    product_id: 123,
    quantity: 5
}
```

**Remove Item**
```javascript
POST /cart-handler.php
{
    action: "remove",
    product_id: 123
}
```

**Get Cart Count**
```javascript
GET /cart-handler.php?action=count
Response: { success: true, count: 5 }
```

### Wishlist Operations

**Add to Wishlist**
```javascript
POST /wishlist-handler.php
{
    action: "add",
    product_id: 123
}
```

**Remove from Wishlist**
```javascript
POST /wishlist-handler.php
{
    action: "remove",
    product_id: 123
}
```

### Review Submission

**Submit Review**
```javascript
POST /submit-review.php
{
    product_id: 123,
    rating: 5,
    comment: "Amazing product!"
}
```

---

## 🔐 Security

### Best Practices Implemented

1. **Password Security**
   - BCrypt hashing with cost factor 10
   - Minimum 6 characters enforced
   - Strength indicator on registration

2. **SQL Injection Prevention**
   - All queries use prepared statements
   - No raw SQL concatenation
   - Input validation and sanitization

3. **CSRF Protection**
   - Token generation on all forms
   - Token verification on submission
   - Token regeneration after use

4. **Session Security**
   - HTTPOnly cookies
   - Secure flag in production
   - Session timeout (1 hour default)
   - Session regeneration on login

5. **XSS Prevention**
   - All output escaped with htmlspecialchars()
   - Content Security Policy headers
   - No eval() or dangerous functions

6. **Access Control**
   - Role-based permissions
   - Admin routes protected
   - User authentication required

### Security Checklist

```
✅ Change default admin password
✅ Use HTTPS in production
✅ Update PHP to latest version
✅ Enable error logging (disable display)
✅ Set strict file permissions
✅ Regular database backups
✅ Update dependencies regularly
✅ Monitor error logs
✅ Use environment variables for secrets
✅ Enable firewall (UFW/iptables)
```

---

## 🎨 Customization

### Changing Colors

Edit `assets/css/style.css`:

```css
:root {
    /* Change these values */
    --deep-rose: #YOUR_COLOR;
    --primary-pink: #YOUR_COLOR;
    --soft-pink: #YOUR_COLOR;
    /* ... etc */
}
```

### Changing Fonts

```css
/* In style.css */
@import url('https://fonts.googleapis.com/css2?family=YOUR_FONT');

body {
    font-family: 'YOUR_FONT', sans-serif;
}

h1, h2, h3 {
    font-family: 'YOUR_HEADING_FONT', serif;
}
```

### Adding Payment Gateway

**Stripe Example:**

1. Install Stripe PHP SDK
2. Create `process-payment.php`:

```php
<?php
require_once 'vendor/autoload.php';
\Stripe\Stripe::setApiKey(STRIPE_SECRET_KEY);

$charge = \Stripe\Charge::create([
    'amount' => $amount * 100,
    'currency' => 'usd',
    'source' => $_POST['stripeToken'],
    'description' => 'Order #' . $order_id
]);
```

### Custom Email Templates

Create `templates/email/order-confirmation.php`:

```php
<!DOCTYPE html>
<html>
<head>
    <style>
        /* Email styles */
    </style>
</head>
<body>
    <h1>Thank you for your order!</h1>
    <p>Order #<?php echo $order_id; ?></p>
    <!-- More content -->
</body>
</html>
```

---

## 🚢 Deployment

### Production Checklist

**1. Environment Setup**
```bash
# Disable error display
php_value display_errors Off
php_value log_errors On

# Set production mode
SetEnv APPLICATION_ENV production
```

**2. Security Hardening**
```bash
# File permissions
find . -type f -exec chmod 644 {} \;
find . -type d -exec chmod 755 {} \;
chmod 640 config/db.php

# Remove sensitive files
rm -f .git
rm -f database.sql
rm -f README.md
```

**3. SSL Certificate**
```bash
# Using Let's Encrypt
sudo certbot --apache -d yourdomain.com
```

**4. Database Optimization**
```sql
-- Add indexes
CREATE INDEX idx_products_category ON products(category);
CREATE INDEX idx_orders_user ON orders(user_id);
CREATE INDEX idx_orders_status ON orders(status);
```

**5. Caching Setup**
```apache
# Enable OPcache
opcache.enable=1
opcache.memory_consumption=128
opcache.max_accelerated_files=10000
```

**6. Backup Strategy**
```bash
# Daily database backup
0 2 * * * mysqldump -u user -p yarnify > /backups/yarnify_$(date +\%Y\%m\%d).sql
```

---

## 🔧 Troubleshooting

### Common Issues

**Issue: Database Connection Failed**
```
Solution:
1. Check credentials in config/db.php
2. Verify MySQL is running: sudo service mysql status
3. Test connection: mysql -u username -p
```

**Issue: Images Not Displaying**
```
Solution:
1. Check file permissions: chmod 755 assets/images/products
2. Verify image paths in database
3. Check .htaccess rewrite rules
```

**Issue: Session Not Working**
```
Solution:
1. Check session.save_path is writable
2. Verify session cookies are enabled
3. Clear browser cookies
```

**Issue: Admin Can't Login**
```
Solution:
1. Verify admin role in database
2. Reset password via database:
   UPDATE users SET password = '$2y$10$...' WHERE email = 'admin@...';
3. Check login.php error messages
```

**Issue: CSRF Token Invalid**
```
Solution:
1. Clear sessions
2. Check token generation in forms
3. Verify token verification in handlers
```

---

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Code Style

- **PHP**: Follow PSR-12 standards
- **CSS**: Use BEM naming convention
- **JavaScript**: ES6+ with semicolons
- **Comments**: Document complex logic

### Testing

- Test on multiple browsers
- Verify mobile responsiveness
- Check security implications
- Test with sample data

---

## 📜 License

This project is proprietary software for Yarnify.

**Copyright © 2025 Yarnify. All Rights Reserved.**

For licensing inquiries, contact: licensing@yarnify.com

---

## 💬 Support

### Documentation
- **Full Docs**: [docs.yarnify.com](https://docs.yarnify.com)
- **API Reference**: [api.yarnify.com](https://api.yarnify.com)
- **Video Tutorials**: [youtube.com/yarnify](https://youtube.com/yarnify)

### Community
- **Discord**: [discord.gg/yarnify](https://discord.gg/yarnify)
- **Forum**: [forum.yarnify.com](https://forum.yarnify.com)
- **Twitter**: [@yarnify](https://twitter.com/yarnify)

### Technical Support
- **Email**: support@yarnify.com
- **Issue Tracker**: [github.com/yarnify/issues](https://github.com/yarnify/issues)
- **Response Time**: 24-48 hours

### Hire Us
Need customization or support?
- **Website**: [yarnify.com/services](https://yarnify.com/services)
- **Email**: hello@yarnify.com

---

## 🙏 Acknowledgments

- **Design Inspiration**: Premium Shopify themes
- **Icons**: Heroicons
- **Fonts**: Google Fonts (Playfair Display, Poppins)
- **Color Palette**: Carefully curated pink shades
- **Community**: Thank you to all contributors!

---

## 📊 Statistics

- **Lines of Code**: 10,000+
- **PHP Files**: 25
- **CSS Lines**: 3,500+
- **JavaScript Lines**: 500+
- **Database Tables**: 7
- **Features**: 50+

---

## 🗺️ Roadmap

### Version 1.1 (Q2 2025)
- [ ] Multi-language support
- [ ] Advanced search filters
- [ ] Product comparisons
- [ ] Gift cards
- [ ] Social media integration

### Version 1.2 (Q3 2025)
- [ ] Mobile app (React Native)
- [ ] Email marketing integration
- [ ] Advanced analytics
- [ ] Inventory forecasting
- [ ] Subscription products

### Version 2.0 (Q4 2025)
- [ ] Multi-vendor marketplace
- [ ] Wholesale portal
- [ ] Advanced shipping options
- [ ] Multi-currency support
- [ ] AI-powered recommendations

---

## 📞 Quick Links

- [Installation Guide](#-installation)
- [Configuration](#-configuration)
- [Database Schema](#-database-schema)
- [Security](#-security)
- [Deployment](#-deployment)
- [Troubleshooting](#-troubleshooting)

---

<div align="center">

## Made with 💖 for Yarnify

**Handcrafted E-Commerce for Handcrafted Products**

[Website](https://yarnify.com) • [Documentation](https://docs.yarnify.com) • [Support](mailto:support@yarnify.com)

⭐ Star us on GitHub if you find this helpful!

</div>

---

**Last Updated**: February 2025  
**Version**: 1.0.0  
**Maintained By**: Yarnify Development Team

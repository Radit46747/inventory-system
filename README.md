# 🏪 Inventory Management System

![Laravel](https://img.shields.io/badge/Laravel-11.49.1-FF2D20?style=for-the-badge&logo=laravel)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4?style=for-the-badge&logo=tailwindcss)
![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?style=for-the-badge&logo=php)

A modern inventory management system built with Laravel 11 and Tailwind CSS for tracking goods, managing loans, maintenance schedules, and supplier information in one centralized platform.

‎**Note:** The interface for this project is in Indonesian. However, if you want a multi-language version, please contact us.

## 📋 About

This Inventory System provides businesses with comprehensive tools to manage their physical assets efficiently. From tracking stock levels and handling equipment loans to scheduling maintenance and managing supplier relationships, the system offers a complete solution for inventory control.

**Warning:** This inventory system project is still experimental, which means some features may still have errors, but we will try to fix the problems in future versions.

## ✨ Features

### 📊 Dashboard
- **Real-time Overview** - Key metrics and inventory status at a glance
- **Low Stock Alerts** - Automatic notifications for items below mininum levels (TBA)
- **Quick Actions** - Fast access to common operations

### 📦 Goods Management
- **Product Catalog** - Complete product database with images and details
- **Stock Tracking** - Real-time quantity tracking across locations
- **Category Organization** - Hierarchical product categorization

### 🔄 Loans Management
- **Equipment Loans** - Track borrowed items and due dates
- **Borrower Management** - Maintain borrower information and history
- **Loan Periods** - Set and track loan durations
- **Return Tracking** - Monitor item returns and condition
- **Overdue Alerts** - Automatic notifications for overdue items (TBA)

### 🔧 Maintenance Management
- **Maintenance Scheduling** - Plan and schedule equipment maintenance
- **Service History** - Complete maintenance records for each item
- **Technician Assignment** - Assign maintenance tasks (TBA)
- **Preventive Maintenance** - Schedule regular preventive checks (TBA)
- **Downtime Tracking** - Monitor equipment availability

### 🤝 Suppliers Management
- **Supplier Database** - Complete supplier information and contacts
- **Order History** - Track past orders and deliveries (TBA)
- **Contact Management** - Multiple contacts per supplier (TBA)

### 📝 Activities Log
- **Audit Trail** - Complete history of all system actions
- **User Activity** - Track user logins and actions
- **Inventory Changes** - Record all stock adjustments
- **Exportable Logs** - Export activity data for reporting (TBA)
- **Filter & Search** - Easily find specific activities

### ⚙️ System Features
- **Multi-user Support** - Multiple users with different access levels
- **Role-Based Permissions** - Granular access control system
- **Data Export** - Export to Excel, PDF, and CSV formats
- **Responsive Design** - Works on desktop, tablet, and mobile
- **Search & Filters** - Advanced search capabilities using datatables

## 🚀 Quick Start Guide

### Prerequisites
- PHP 8.2+
- Composer 2.5+
- MySQL 8.0+ or PostgreSQL 13+
- Node.js 18+
- NPM or Yarn

### Installation Steps

1. **Clone and setup**
```bash
git clone https://github.com/Radit46747/inventory-system.git
cd inventory-system
composer install
npm install
cp .env.example .env
php artisan key:generate
```

2. **Configure environment**
Edit `.env` file with your database credentials:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=inventory_db
DB_USERNAME=root
DB_PASSWORD=
```

3. **Setup database and assets**
```bash
php artisan migrate --seed
npm run build
php artisan serve
```

4. **Access the system**
Visit `http://localhost:8000`

## 🎨 UI Components

### Product Card Component
```html
// Show item examples
    <div id="showModal{{$item->id}}" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="text-xl font-bold">
                    <i class="fas fa-eye mr-2"></i> Detail Barang {{$item->name}}
                </h3>
                <button id="closeModalBtnS{{$item->id}}" class="btn-close">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="modal-body">
                <p><strong>Nama:</strong> {{ $item->name }}</p>
                <p><strong>Kode:</strong> {{ $item->serial_number ?? '-' }}</p>
                <p><strong>Deskripsi:</strong> {{ $item->description ?? 'Tidak ada' }}</p>
                <p><strong>Stok saat ini:</strong> {{ $item->stock }}</p>
                @if(Auth::user()->role != 3)
                    @if ($item->stock < 1)
                    <p class="text-red-500">Barang ini habis. silahkan untuk memasok barang.</p>
                    @elseif ($item->stock < $item->min_stock)
                    <p class="text-orange-500">Barang ini akan segera habis.</p>
                    @elseif ($item->max_stock && $item->stock > $item->max_stock)
                    <p class="text-blue-500">Barang ini melebihi batas stok yang dapat disimpan.</p>
                    @endif
                @endif
                @if ($item->image)
                    <p>Gambar :</p>
                    <img src="{{ asset('storage/' . $item->image) }}">
                @endif
            </div>
        </div>
    </div>
```

## 🔒 Security Features

### Login Protection
- **Brute Force Protection** - Account lockout after multiple failed attempts for 30 seconds. Duration doubles for every another multiple failed attempts.
- **Two-Factor Authentication** - Optional 2FA for enhanced security (TBA)
- **Session Management** - Secure session handling with timeout
- **Password Policies** - Enforce strong password requirements
- **Login Attempt Logging** - Track all login attempts

### Data Security
- **Role-Based Access Control (RBAC)** - Granular permissions system
- **CSRF Protection** - Built-in Laravel CSRF tokens
- **XSS Prevention** - Automatic data sanitization
- **SQL Injection Protection** - Using Eloquent ORM
- **Input Validation** - Comprehensive form validation
- **HTTPS Enforcement** - Force secure connections in production

## 🚢 Deployment

### Production Deployment Steps

1. **Optimize application**
```bash
composer install --optimize-autoloader --no-dev
php artisan config:cache
php artisan route:cache
php artisan view:cache
npm run production
```

2. **Set permissions**
```bash
chmod -R 755 storage bootstrap/cache
chown -R www-data:www-data /var/www/inventory-system
```

3. **Configure environment for production**
```env
APP_ENV=production
APP_DEBUG=false
APP_URL=https://your-domain.com

# Force HTTPS
FORCE_HTTPS=true

# Secure session settings
SESSION_SECURE_COOKIE=true
SESSION_HTTP_ONLY=true
```

4. **Set up cron job for scheduled tasks**
```bash
* * * * * cd /path-to-project && php artisan schedule:run >> /dev/null 2>&1
```

## 📚 Additional Documentation

### How to Add Goods
1. Navigate to **Goods → Add New Item**
2. Fill in required fields
3. Upload product image (optional)
4. Set minimum stock level for alerts
5. Add detailed description (optional)
6. Click "Save Item"

**Note:** At least 1 categories is added before add goods.

### How to Manage Loans
1. Go to **Loans → New Loan**
2. Select borrower from database
3. Choose items to loan with quantities
4. Set loan period and due date
5. Add special instructions or conditions
6. Save and generate loan agreement

### How to Add Maintenance
1. Access **Maintenance → Add Maintenance**
2. Select equipment/item needing maintenance
3. Choose maintenance type
4. Set estimated duration
5. Schedule date and save

### How to Add Suppliers
1. Navigate to **Suppliers → Add Supplier**
2. Enter company details and contact information
3. Add multiple contact persons if needed (TBA)
4. Save and categorize supplier

## 🔧 Troubleshooting

### Common Issues

**Can't Login or Register**
- Ensure database connection is working
- Check if user account is active
- Verify email and password are correct
- Clear browser cache and cookies
- Check if account is locked due to multiple failed attempts

**Can't Add Goods**
- Check if all required fields are filled
- Ensure item name is not a duplicate
- Verify stock quantity is a positive number
- Check database connection and storage
- Ensure minimum stock is lower than maximum stock

**Photo Upload Fails**
- Check file size limit (default: 2MB)
- Verify file type is allowed (jpg, png, gif)
- Ensure storage directory has write permissions
- Check PHP file_uploads setting is enabled
- Verify upload_max_filesize in php.ini

**Slow Performance**
- Clear application cache: `php artisan optimize:clear`
- Check database indexes on frequently queried tables
- Optimize images before upload
- Consider adding Redis for caching
- Check server resources (CPU, Memory)

**Export Not Working**
- Ensure PHP zip extension is installed
- Check write permissions in storage directory
- Verify memory_limit in php.ini is sufficient
- Check if any required fields are missing

## 🙏 Acknowledgements

- **Laravel Community** - For the amazing PHP framework
- **Tailwind CSS** - For the utility-first CSS framework
- **Livewire** - For making dynamic interfaces simpler
- **Alpine.js** - For lightweight JavaScript interactions
- **All Contributors** - Who helped improve this system

---

**Inventory System** © 2025 - Built with Laravel 11 & Tailwind CSS

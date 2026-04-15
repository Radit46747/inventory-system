# 🏪 Inventory Management System

![Laravel](https://img.shields.io/badge/Laravel-11.49.1-FF2D20?style=for-the-badge&logo=laravel)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4?style=for-the-badge&logo=tailwindcss)

A modern inventory management system built with Laravel 11 and Tailwind CSS for tracking goods, managing loans, maintenance schedules, and supplier information in one centralized platform.

This website is built in Indonesian language, so it will take time to edit this README. (deleted by mistake)

## 📋 About

This Inventory Management System provides businesses with comprehensive tools to manage their physical assets efficiently. From tracking stock levels and handling equipment loans to scheduling maintenance and managing supplier relationships, the system offers a complete solution for inventory control.

## ✨ Features

### 📊 Dashboard
- **Real-time Overview** - Key metrics and inventory status at a glance
- **Activity Feed** - Recent transactions and system activities
- **Low Stock Alerts** - Automatic notifications for items below reorder levels
- **Upcoming Maintenance** - Scheduled maintenance reminders
- **Quick Actions** - Fast access to common operations

### 📦 Goods Management
- **Product Catalog** - Complete product database with images and details
- **Stock Tracking** - Real-time quantity tracking across locations
- **Category Organization** - Hierarchical product categorization
- **Barcode Support** - Generate and scan barcodes for items
- **Batch Tracking** - Manage items by batches and expiry dates

### 🔄 Loans Management
- **Equipment Loans** - Track borrowed items and due dates
- **Borrower Management** - Maintain borrower information and history
- **Loan Periods** - Set and track loan durations
- **Return Tracking** - Monitor item returns and condition
- **Overdue Alerts** - Automatic notifications for overdue items

### 🔧 Maintenance Management
- **Maintenance Scheduling** - Plan and schedule equipment maintenance
- **Service History** - Complete maintenance records for each item
- **Technician Assignment** - Assign maintenance tasks to staff
- **Preventive Maintenance** - Schedule regular preventive checks
- **Downtime Tracking** - Monitor equipment availability

### 🤝 Suppliers Management
- **Supplier Database** - Complete supplier information and contacts
- **Performance Tracking** - Rate and review supplier performance
- **Order History** - Track past orders and deliveries
- **Contact Management** - Multiple contacts per supplier
- **Document Storage** - Store contracts and agreements

### 📝 Activities Log
- **Audit Trail** - Complete history of all system actions
- **User Activity** - Track user logins and actions
- **Inventory Changes** - Record all stock adjustments
- **Exportable Logs** - Export activity data for reporting
- **Filter & Search** - Easily find specific activities

### ⚙️ System Features
- **Multi-user Support** - Multiple users with different access levels
- **Role-Based Permissions** - Granular access control system
- **Data Export** - Export to Excel, PDF, and CSV formats
- **Responsive Design** - Works on desktop, tablet, and mobile
- **Search & Filters** - Advanced search capabilities throughout

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
Visit `http://localhost:8000` and login with:
- Email: `admin@example.com`
- Password: `password`

## 🎨 UI Components

### Product Card Component
```html
<div class="bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow duration-300">
    <div class="p-4">
        <div class="flex items-center justify-between mb-3">
            <span class="px-2 py-1 text-xs font-semibold rounded-full
                {{ $item->quantity < $item->min_stock ? 'bg-red-100 text-red-800' : 'bg-green-100 text-green-800' }}">
                {{ $item->quantity }} in stock
            </span>
            @if($item->is_loaned)
                <span class="px-2 py-1 text-xs font-semibold bg-yellow-100 text-yellow-800 rounded-full">
                    On Loan
                </span>
            @endif
        </div>
        
        <h3 class="text-lg font-semibold text-gray-900">{{ $item->name }}</h3>
        <p class="mt-1 text-sm text-gray-600">{{ $item->description }}</p>
        
        <div class="mt-4 flex items-center justify-between">
            <span class="text-lg font-bold text-gray-900">${{ number_format($item->price, 2) }}</span>
            <div class="flex space-x-2">
                <button class="px-3 py-1 text-sm bg-blue-600 text-white rounded hover:bg-blue-700">
                    Edit
                </button>
                <button class="px-3 py-1 text-sm bg-gray-100 text-gray-800 rounded hover:bg-gray-200">
                    View
                </button>
            </div>
        </div>
    </div>
</div>
```

## 🔒 Security Features

### Login Protection
- **Brute Force Protection** - Account lockout after multiple failed attempts
- **Two-Factor Authentication** - Optional 2FA for enhanced security
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

### User Permission Levels
```php
// Example permission structure
$permissions = [
    'admin' => [
        'manage_users',
        'manage_settings',
        'view_reports',
        'manage_inventory',
        'approve_loans'
    ],
    'manager' => [
        'manage_inventory',
        'view_reports',
        'approve_loans',
        'manage_maintenance'
    ],
    'staff' => [
        'view_inventory',
        'create_loans',
        'log_maintenance'
    ]
];
```

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
2. Fill in required fields: Name, Category, Quantity, Price
3. Upload product image (optional)
4. Set minimum stock level for alerts
5. Add detailed description and specifications
6. Click "Save Item"

### How to Manage Loans
1. Go to **Loans → New Loan**
2. Select borrower from database or add new
3. Choose items to loan with quantities
4. Set loan period and due date
5. Add special instructions or conditions
6. Save and generate loan agreement

### How to Schedule Maintenance
1. Access **Maintenance → Schedule Maintenance**
2. Select equipment/item needing maintenance
3. Choose maintenance type (Preventive/Corrective)
4. Assign to technician/staff member
5. Set priority and estimated duration
6. Schedule date and add notes

### How to Add Suppliers
1. Navigate to **Suppliers → Add Supplier**
2. Enter company details and contact information
3. Add multiple contact persons if needed
4. Upload company documents/contracts
5. Set payment terms and conditions
6. Save and categorize supplier

## 🔧 Troubleshooting

### Common Issues

**Can't Login or Register**
- Ensure database connection is working
- Check if user account is active
- Verify email and password are correct
- Clear browser cache and cookies
- Check if account is locked due to multiple failed attempts

**Can't Add Goods**
- Verify user has "manage_inventory" permission
- Check if all required fields are filled
- Ensure item name is not a duplicate
- Verify stock quantity is a positive number
- Check database connection and storage

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

**Inventory Management System** © 2026 - Built with Laravel 11 & Tailwind CSS

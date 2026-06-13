<div align="center">
  
# 🚀 Laravel Sensero
### Professional Server Monitoring Dashboard for Laravel Applications
</div>

<p align="center">
  <img src="https://azaran-code.ir/storage/134/sensero.png" height="480" alt="Laravel Sensero Dashboard Preview" width="100%">
</p>

<div align="center">

### 🔥 Real-time Monitoring • 💻 Web Terminal • 🛡️ Security Controls • 📊 Performance Insights

</div>

---

## ✨ Key Features

- **🚀 Real-time Monitoring**: Automatic AJAX refreshing for live updates.
- **🖥️ Server Statistics**: CPU, RAM, Disk usage, and system load average.
- **📝 DotEnv Editor**: View and modification of `.env` file variables directly from the UI.
- **💻 Web Terminal**: Execute Artisan and Composer commands securely from the browser.
- **🔍 Query Logs**: Monitor and analyze database queries (slow queries, etc.).
- **📂 File Permissions**: Check and fix file/folder permissions.
- **🛣️ Route Inspector**: View all registered application routes.
- **⚙️ PHP & Config Info**: detailed PHP extensions, verified config files syntax.
- **🎨 Modern UI**: Responsive Glassmorphism design with Dark/Light modes.
- **🔒 Secure**: IP Whitelisting and optional simplified authorization.

<div align="center">

<table>
<tr>
<th>Feature</th>
<th>Description</th>
<th>Status</th>
</tr>
<tr>
<td>🖥️ <strong>Real-time Server Stats</strong></td>
<td>Monitor CPU, RAM, Disk usage & system load with live updates</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>📝 <strong>DotEnv Editor</strong></td>
<td>Edit environment variables directly from UI with backup options</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>💻 <strong>Web Terminal</strong></td>
<td>Execute Artisan & Composer commands securely from browser</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🔍 <strong>Query Analyzer</strong></td>
<td>Monitor & analyze database queries with performance insights</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🗂️ <strong>File Permissions</strong></td>
<td>Check & fix file/folder permissions with one-click solutions</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🛣️ <strong>Route Inspector</strong></td>
<td>View all registered application routes with detailed information</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>⚙️ <strong>PHP & Config Info</strong></td>
<td>Detailed PHP extensions, packages & config syntax validation</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🎨 <strong>Modern UI</strong></td>
<td>Responsive Glassmorphism design with Dark/Light modes</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🔒 <strong>Security</strong></td>
<td>IP Whitelisting, user authorization & role-based access</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🚀 <strong>Queue Manager</strong></td>
<td>Monitor and manage Laravel queues with job control</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>📦 <strong>Composer Editor</strong></td>
<td>Manage composer.json dependencies and configurations</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🌐 <strong>Connection Checker</strong></td>
<td>Monitor internet connectivity to multiple endpoints</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>🔄 <strong>Environment Switcher</strong></td>
<td>Toggle between local and production environments</td>
<td>✅ Ready</td>
</tr>
<tr>
<td>📊 <strong>Performance Metrics</strong></td>
<td>Track application performance with detailed analytics</td>
<td>✅ Ready</td>
</tr>
</table>

</div>

---

## 🚀 Quick Start

### Prerequisites
- PHP 8.2 or higher
- Laravel 11.0 or 12.0
- Composer

### Installation

#### Via Composer (Recommended)
```bash
composer require saeedvir/laravel-sensero
```

#### For Local Development
Add to your project's `composer.json`:
```json
{
    "repositories": [
        {
            "type": "path",
            "url": "../path/to/packages/laravel-sensero",
            "options": {
                "symlink": true
            }
        }
    ]
}
```

Then install:
```bash
composer require saeedvir/laravel-sensero:@dev
```

### Setup

1. **Publish Configuration**
```bash
php artisan vendor:publish --provider="Saeedvir\LaravelSensero\LaravelSenseroServiceProvider" --tag="config"
```

2. **Publish Assets**
```bash
php artisan vendor:publish --provider="Saeedvir\LaravelSensero\LaravelSenseroServiceProvider" --tag="assets"
```

3. **Publish Language Files (Optional)**
```bash
php artisan vendor:publish --provider="Saeedvir\LaravelSensero\LaravelSenseroServiceProvider" --tag="lang"
```

4. **Access Dashboard**
Visit `http://your-app.test/sensero` (default route)

### Post-Installation Steps

1. **Configure Security Settings**
   - Set up IP whitelisting in `config/laravel-sensero.php`
   - Configure authorization if needed
   - Set up proper middleware

2. **Customize Dashboard**
   - Adjust update intervals based on your needs
   - Enable/disable sections as required
   - Configure database monitoring thresholds

3. **Set Up Environment Variables**
   - Add license ID if using premium features
   - Configure monitoring thresholds
   - Set up security settings

---

## ⚙️ Configuration

### Main Configuration Options
```php
// config/laravel-sensero.php
return [
    'route_prefix' => env('LARAVEL_SENSERO_ROUTE_PREFIX', '/sensero'),
    'update_interval' => env('LARAVEL_SENSERO_UPDATE_INTERVAL', 25),
    'server_usage_enabled' => env('LARAVEL_SENSERO_USAGE_ENABLE', true),
    'command_logger' => env('LARAVEL_SENSERO_LOG_COMMAND', false),
    
    // Database monitoring
    'database' => [
        'slow_query_threshold' => env('LARAVEL_SENSERO_QUERY_LOG_THRESHOLD', 300),
        'log_slow_queries' => env('LARAVEL_SENSERO_LOG_SLOW_QUERY', false),
        'log_any_queries' => env('LARAVEL_SENSERO_LOG_ANY_QUERY', false),
    ],
    
    // Security settings
    'security' => [
        'allowed_ips' => [], // Restrict access to specific IPs
        'authorize' => [
            'enable' => false,
            'admin_ids' => [],
        ],
    ],
];
```

### Environment Variables
```env
# Basic Settings
LARAVEL_SENSERO_ROUTE_PREFIX=/sensero
LARAVEL_SENSERO_UPDATE_INTERVAL=25
LARAVEL_SENSERO_USAGE_ENABLE=true

# Database Monitoring
LARAVEL_SENSERO_QUERY_LOG_THRESHOLD=300
LARAVEL_SENSERO_LOG_SLOW_QUERY=false
LARAVEL_SENSERO_LOG_ANY_QUERY=false
LARAVEL_SENSERO_LOG_COMMAND=false

# Security
LARAVEL_SENSERO_LICENSE_ID=xxxxxxxxxxxxxxxxxx
```

---

## 🎯 Dashboard Sections

### 🖥️ Server Information
- Real-time CPU, Memory, and Disk usage
- System load averages
- Uptime monitoring
- Project size calculation

### 📝 Environment Variables
- View and edit `.env` variables
- Add new variables
- Delete existing variables
- Backup before changes

### ⚙️ Configuration Editor
- Edit Laravel config files
- Syntax highlighting
- Validation before saving
- File backup options

### 🗄️ Database Monitoring
- Active database processes
- Kill individual or all processes
- Query execution time analysis
- Slow query detection

### 💻 Command Center
- Execute Artisan commands
- Run Composer operations
- Internal class execution
- Command history tracking

### 🔍 Query Logs
- Monitor all database queries
- Analyze slow queries
- Export query logs
- Performance recommendations

### 🚀 Queue Management
- Monitor queued jobs
- Retry failed jobs
- Remove pending jobs
- Queue statistics

### 🛡️ Security Overview
- Laravel version checks
- Security vulnerability scanning
- Permission analysis
- Health status monitoring

### 📁 Permissions Manager
- Visual representation of file permissions
- One-click permission fixes
- Storage health checks
- Directory structure analysis

### 🔄 Environment Switcher
- Toggle between local and production modes
- Automatic configuration updates
- Cache clearing and optimization
- Service restart capabilities

### 📦 Composer Editor
- Edit composer.json dependencies
- Manage repositories and packages
- Configure autoload settings
- Update scripts and configurations

### 🌐 Connection Checker
- Monitor connectivity to multiple endpoints
- Download speed testing
- Service availability checking
- Network performance metrics

### 📊 Performance Monitoring
- Real-time CPU, memory, and disk usage graphs
- Historical usage logging and analysis
- Performance trend identification
- Alert thresholds for critical metrics

---

## 🔐 Security Features

### IP Whitelisting
Restrict dashboard access to specific IP addresses:
```php
'security' => [
    'allowed_ips' => ['127.0.0.1', '192.168.1.10'],
],
```

### User Authorization
Enable user-based access control:
```php
'security' => [
    'authorize' => [
        'enable' => true,
        'admin_ids' => [1, 2, 3],
        'auth_url' => '/login', // Redirect URL for unauthorized users
    ],
],
```

### Middleware Protection
Apply custom middleware:
```php
'middleware' => ['web', 'auth', 'role:admin'],
```

---

## 🎨 Customization

### Enable/Disable Sections
Control which dashboard sections are visible:
```php
'active_sections' => [
    'sysinfo' => ['enable' => true],
    'environment' => ['enable' => true],
    'database' => ['enable' => true],
    // ... other sections
],
```

### Custom Commands
Add custom Artisan or Composer commands:
```php
'custom_commands' => [
    'artisan' => [
        'inspire' => 'inspire',
        'cache:clear' => 'cache:clear',
    ],
    'composer' => [
        'install' => 'install',
        'update' => 'update',
    ],
],
```

### Theme Configuration
Switch between light/dark themes and RTL/LTR layouts:
```php
'language' => env('LARAVEL_SENSERO_LANGUAGE', 'en'), // en, fa, etc.
'use_cdn_for_assets' => false, // Use local or CDN assets
```

---

## 🛠️ Advanced Features

### Environment Mode Switching
Quickly switch between local and production environments:
```php
'switch_mode' => [
    'production' => [
        'envVariables' => [
            'APP_ENV' => 'production',
            'APP_DEBUG' => 'false',
            'CACHE_STORE' => 'redis',
        ],
        'artisan' => [
            'optimize:clear',
            'queue:restart',
        ],
    ],
    'local' => [
        'envVariables' => [
            'APP_ENV' => 'local',
            'APP_DEBUG' => 'true',
            'CACHE_STORE' => 'file',
        ],
        'artisan' => [
            'optimize:clear',
        ],
    ],
],
```

### Query Analysis
Automatic query optimization suggestions:
- MySQL EXPLAIN analysis
- PostgreSQL query plan analysis
- Index recommendation engine
- Performance bottleneck detection

### Connection Monitoring
Monitor internet connectivity to various services:
- Google, Cloudflare, Packagist
- CDN services (jsDelivr, unpkg, cdnjs)
- Custom endpoints

---

## 📊 Performance Optimization

### Caching Strategy
- Intelligent caching of system information
- Configurable cache TTL
- Cache warming mechanisms
- Cache tag organization

### Resource Monitoring
- Efficient CPU and memory usage tracking
- Optimized disk space calculation
- Reduced I/O operations
- Asynchronous data collection

### Query Optimization
- Sampling-based query monitoring
- Threshold-based analysis
- Cached query results
- Reduced EXPLAIN overhead

---

## 🏗️ Architecture Overview

Laravel Sensero follows a modular architecture with dedicated services for each feature:

### Core Components
- **ServiceProvider**: Handles package registration, configuration merging, and asset publishing
- **ServerMonitorController**: Central hub for all dashboard functionality and API endpoints
- **Services**: Specialized classes for different monitoring aspects (System, Database, Commands, etc.)

### Service Layer
- **SystemInformationService**: Handles server stats, resource usage, and system info
- **QueryLogService**: Monitors database queries and analyzes performance
- **CommanderService**: Executes Artisan and Composer commands
- **EnvEditorService**: Manages environment variable operations
- **ConfigFileService**: Handles Laravel configuration file operations

### Security Layer
- IP-based access control
- User authentication and authorization
- Input validation and sanitization
- CSRF protection


### Code Standards
- Follow PSR-12 coding standards
- Write comprehensive tests for new features
- Update documentation as needed
- Ensure backward compatibility

---

## 🛠️ Troubleshooting

### Common Issues

#### Dashboard Not Loading
- Check if assets were published correctly
- Verify that the route prefix doesn't conflict with existing routes
- Ensure required middleware is properly configured

#### Query Monitoring Not Working
- Make sure database logging is enabled in config
- Check that the database connection is working
- Verify log file permissions

#### Performance Issues
- Disable unused dashboard sections
- Increase cache TTL values
- Adjust update intervals to reduce server load

#### Permission Errors
- Ensure the web server has write access to storage/logs
- Check that config files have proper permissions
- Verify .env file permissions

### Debugging Tips
- Enable debug mode in configuration for detailed error messages
- Check Laravel logs for any related errors
- Use the built-in command center to run diagnostic commands

## 📄 License

purchase license from https://azaran-code.ir

---

## 🆘 Support & Issues

If you encounter any problems or have suggestions:
- 🐛 Report bugs on [GitHub Issues](https://github.com/saeedvir/laravel-sensero/issues)
- 💬 Ask questions in the discussions
- 📧 Contact the author: [saeed.es91@gmail.com](mailto:saeed.es91@gmail.com)

---

<div align="center">

### Made with ❤️ by [Saeed Abdollahian](https://github.com/saeedvir)

⭐ Star this repo if you find it helpful!

</div>

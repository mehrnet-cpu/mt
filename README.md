# mehditanekar.ir — انتشار خودکار روی هاست شخصی

سایت روی هاست خودتان (`mehditanekar.ir`) در کنار وردپرس اجرا می‌شود؛ GitHub Pages دیگر استفاده نمی‌شود.

## نحوهٔ استقرار

با هر پوش روی شاخهٔ `main`، ورک‌فلوی `.github/workflows/deploy.yml` به‌صورت خودکار اجرا می‌شود و فایل‌های ریپو را با FTP در مسیر `public_html/` روی هاست آپلود می‌کند (اکشن [`SamKirkland/FTP-Deploy-Action`](https://github.com/SamKirkland/FTP-Deploy-Action)).

مسیرها و فایل‌های زیر از آپلود مستثنا هستند تا وردپرس دست‌نخورده بماند:
`.git`، `.github`، `wp-admin/`، `wp-includes/`، `wp-content/`، فایل‌های `wp-*.php`، `wp-config.php`، `.htaccess`، `xmlrpc.php`.

یعنی این ریپو فقط `index.html` و `assets/` را روی ریشهٔ هاست می‌نویسد؛ چون `index.html` معمولاً بر `index.php` وردپرس در `DirectoryIndex` اولویت دارد، همین صفحهٔ استاتیک روی ریشهٔ دامنه نمایش داده می‌شود و بقیهٔ مسیرها (مثل `/بلاگ`) همچنان به‌دست وردپرس سرو می‌شوند.

### سکرت‌های لازم (`Settings → Secrets and variables → Actions`)

- `FTP_SERVER`
- `FTP_USERNAME`
- `FTP_PASSWORD`

این سه از قبل تنظیم شده‌اند؛ اگر رمز FTP روی هاست عوض شود، باید `FTP_PASSWORD` هم همین‌جا به‌روزرسانی شود.

## بررسی بعد از هر پوش

بعد از هر پوش، تب **Actions** ریپو را چک کنید تا اجرای `Deploy to hosting` سبز شود؛ سپس `https://mehditanekar.ir/` را برای دیدن تغییرات باز کنید (ممکن است به‌خاطر کش هاست/CDN چند دقیقه طول بکشد).

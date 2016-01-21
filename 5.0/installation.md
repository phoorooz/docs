# نصب

- [نصب کامپوزر](#install-composer)
- [نصب لاراول](#install-laravel)
- [نیازمندیهای سرور](#server-requirements)

<a name="install-composer"></a>
## نصب کامپوزر

لاراول برای مدیریت وابستگیهای پروژه از  [کامپوزر](http://getcomposer.org) استفاده میکند. بنابراین پیش از استفاده از لاروال، باید از نصب بودن کامپوزر بر روی سیستم خود مطمئن شوید.

<a name="install-laravel"></a>
## نصب لاراول

### از طریق نصب کننده لاروال

برای قدم اول لاراول را با استفاده از کامپوزر بر روی سیستم خود نصب کنید.

	composer global require "laravel/installer=~1.1"

دایرکتوری `~/.composer/vendor/bin` را در متغیر محیطی PATH قرار دهید تا سیستم محل قرار گرفتن`laravel` را بداند.

پس از نصب لاراول، اجرای دستور ساده `laravel new` در خط فرمان یک نسخه خام از یک پروژه لاراول را در مکانی که معرفی میکنید نصب میکند. برای مثال `laravel new blog` یک دایرکتوری با نام `blog` شامل یک نسخه خام پروژه لاراول با تمام بسته های مورد نیاز ایجاد مینماید. این روش نصب بسیار سریعتر از استفاده از کامپوزر است:

	laravel new blog

### با استفاده از دستور create-project کامپوزر

همچنین میتوان با استفاده از دستور `create-project` کامپوزر در خط فرمان یک پروژه خام لاراول ایجاد نمایید:

	composer create-project laravel/laravel {directory} "~5.0.0" --prefer-dist

پس از نصب، باید پروژه را با آخرین بسته های لاراول به روزرسانی نمایید. ابتدا، فایل `{directory}/vendor/compiled.php` را حذف نمایید. در خط فرمان دایرکتوری خود را به `{directory}` تغییر دهید و دستور `composer update` را اجرا کنید.

### Scaffolding

لاراول از ابتدا برای ثبت کاربران و سنجش هویت کاربران scaffolding را با خود دارد. اگر میخواهید این امکانات را حذف نمایید، از دستور `fresh` در آرتیزان استفاده کنید:

	php artisan fresh

<a name="server-requirements"></a>
## نیازمندیهای سرور

سرور لاراول مورد استفاده برای این نسخه نیازمندیهای زیر را دارد:

- PHP >= 5.4
- Mcrypt PHP Extension
- OpenSSL PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension

بعد از PHP 5.5، در برخی توزیعهای سیستم عاملها اکستنشن PHP JSON را باید دستی نصب نمود. وقتی از اوبونتر استفاده میکنید، این کار را میتوان با استفاده از دستور `apt-get install php5-json` انجام داد.

<a name="configuration"></a>
## پیکربندی

اولین کاری که پس از انجام لاراول باید انجام دهید، مقداردهی کلید اپلیکیشن با رشته ای تصادفی است. اگر کامپوزر را با استفاده از کامپوزر نصب کرده اید، این کلید احتمالا با استفاده از فرمان `key:generate` مقداردهی شده باشد.

این رشته باید 32 کاراکتر داشته باشد. این کلید را میتوانید در فایل متغیرهای محیطی لاراول با پسوند `.env` مقداردهی کنید.
**اگر کلید اپلیکیشن را مقداردهی نکنید، نشست و دیگر داده های کدگذاری شده کاربر امن نخواهند بود**

لاراول تقریبا نیازی به تنظیمات دیگری ندارد. میتوانید شروع به توسعه نرم افزارهای کاربردی تحت وب نمایید! هرچند میتوانید فایل `config/app.php`  و مستندات آن را مرور نمایید. این فایل شامل گزینه ها بسیار زیادی مانند `timezone` یا `ناحیه زمانی` و `locale` یا `تنظیمات محلی` میباشد که میتوانید متناسب با نرم افزار تحت وب خود تغییر دهید.

پس از نصب لاراول، همچنین باید   [تنظیمات محلی خود را هم تغییر دهید](/docs/{{version}}/configuration#environment-configuration).
> **نکته:** هیچگاه برای نرم افزارهای کاربردی واقعی مقدار `app.debug` را  `true` نگذارید.

<a name="permissions"></a>
### دسترسی ها

شاید نیاز باشد برخی دسترسی ها برای لاراول تعریف شود: وب سرور برای اعمال تغییرات در پوشه های `storage` و `vendor` نیازمند دسترسی کافی برای نوشتن میباشد.

<a name="pretty-urls"></a>
## Pretty URL - آدرسهای خوانا

### آپاچی

لاراول به همراه یک فایل `public/.htaccess` به منظور ایجاد امکان وجود URLهای بدون `index.php` ارائه میشود.

اگر فایل `.htaccess` ارائه شده در کنار لاراول کار نمیکند، میتوانید راه حل زیر را امتحان کنید.

	Options +FollowSymLinks
	RewriteEngine On

	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteRule ^ index.php [L]

### Nginx

بر روی Ngnix راهنمای سرور زیر در تنظیمات سرور امکان pretty URL (آدرسهای خوانا) را فراهم میکند.

	location / {
		try_files $uri $uri/ /index.php?$query_string;
	}

البته هنگامی که از [Homestead](/docs/{{version}}/homestead) استفاده میکنید، آدرسهای خوانا به شکل خودکار تنظیم می شوند.
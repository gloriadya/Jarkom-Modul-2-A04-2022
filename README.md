# JARKOM-MODUL 2-A04-2022

- SAMUEL (5025201187)
- MOHAMAD KHOLID BUGHOWI (5025201253)
- GLORIA DYAH PRAMESTI (5025201033)

## Soal 1

## Soal 2

## Soal 3

## Soal 4

## Soal 5

## Soal 6

## Soal 7

## Soal 8

## Soal 9

## Soal 10

## Soal 11

Pada soal ini diminta untuk hanya membuat directory listing pada folder `public` di webserver **www.eden.wise.a04.com**.

**Penjelasan**

1. Buka **Eden**
2. Ubah **/etc/apache2/sites-available/eden.wise.a04.com.conf**

```bash
nano /etc/apache2/sites-available/eden.wise.a04.com.conf
```

3. Sesuaikan sehingga isinya seperti berikut

```
<VirtualHost *:80>
    ServerName eden.wise.a04.com
    ServerAlias www.eden.wise.a04.com
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/eden.wise.a04.com

    <Directory /var/www/eden.wise.a04.com/public>
        Options +Indexes
    </Directory>

    <Directory /var/www/eden.wise.a04.com/public/css>
        Options -Indexes
    </Directory>

    <Directory /var/www/eden.wise.a04.com/public/images>
        Options -Indexes
    </Directory>

    <Directory /var/www/eden.wise.a04.com/public/js>
        Options -Indexes
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

4. Restart apache2

```bash
service apache2 restart
```

**Testing**

1. Buka **SSS**
2. Ketik command `lynx www.eden.wise.a04.com/public`
   [gambar]
3. Klik pada salah satu directory (`js/`)
   [gambar]

## Soal 12

Pada soal ini diminta untuk mengganti error kode pada webserver **www.eden.wise.a04.com** dengan file `404.html` yang berada dalam folder `error`.

**Penjelasan**

1. Buka **Eden**
2. Ubah **/etc/apache2/sites-available/eden.wise.a04.com.conf**
   ```bash
   nano /etc/apache2/sites-available/eden.wise.a04.com.conf
   ```
3. Sesuaikan isinya seperti berikut

   ```
   <VirtualHost *:80>
       ServerName eden.wise.a04.com
       ServerAlias www.eden.wise.a04.com
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/eden.wise.a04.com

       <Directory /var/www/eden.wise.a04.com/public>
           Options +Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/css>
           Options -Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/images>
           Options -Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/js>
           Options -Indexes
       </Directory>

       ErrorDocument 404 /error/404.html

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

4. Restart apache2
   ```
   service apache2 restart
   ```

## Soal 13

Pada soal ini diminta untuk membuat konfigurasi vitual host yang dapat memberikan akses **www.eden.wise.a04.com/js** kepada **www.eden.wise.a04.com/public/js**.

**Penjelasan**

1. Buka **Eden**
2. Ubah **/etc/apache2/sites-available/eden.wise.a04.com.conf**

   ```bash
   nano /etc/apache2/sites-available/eden.wise.a04.com.conf
   ```

3. Sesuaikan isinya seperti berikut

   ```
   <VirtualHost *:80>
       ServerName eden.wise.a04.com
       ServerAlias www.eden.wise.a04.com
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/eden.wise.a04.com

       <Directory /var/www/eden.wise.a04.com/public>
           Options +Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/css>
           Options -Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/images>
           Options -Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/js>
           Options -Indexes
       </Directory>

       ErrorDocument 404 /error/404.html

       Alias "/js" "/var/www/eden.wise.a04.com/public/js"

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

4. Restart apache2
   ```
   service apache2 restart
   ```

**Testing**

- Buka **SSS**
- Ketik command `lynx www.eden.wise.a04.com/js` (dilakukan sebelum nomor 11)
  ![image]

## Soal 14

Pada soal ini diminta untuk melakukan konfigurasi pada webserver **www.strix.operation.wise.a04.com** dengan port `15000` dan `15500` serta DocumentRoot terletak pada `/var/www/strix.operation.wise.a04.com`.

**Penjelasan**

1. Buka **Eden**
2. Copy **/etc/apache2/sites-available/000-default.conf** ke **/etc/apache2/sites-available/strix.operation.wise.a04.com.conf**

   ```bash
   cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/strix.operation.wise.a04.com.conf
   ```

3. Ubah **/etc/apache2/sites-available/strix.operation.wise.a04.com.conf**

   ```bash
   nano /etc/apache2/sites-available/strix.operation.wise.a04.com.conf
   ```

4. Sesuaikan isinya seperti berikut

   ```
   <VirtualHost *:15000 *:15500>
       ServerName strix.operation.wise.a04.com
       ServerAlias www.strix.operation.wise.a04.com
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/strix.operation.wise.a04.com

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

   ![image]

5. Ubah **/etc/apache2/ports.conf**

   ```bash
   nano /etc/apache2/ports.conf
   ```

6. Sesuaikan isinya seperti berikut

   ```
   # If you just change the port or add more ports here, you will likely also
   # have to change the VirtualHost statement in
   # /etc/apache2/sites-enabled/000-default.conf

   Listen 80
   Listen 15000
   Listen 15500

   <IfModule ssl_module>
           Listen 443
   </IfModule>

   <IfModule mod_gnutls.c>
           Listen 443
   </IfModule>

   # vim: syntax=apache ts=4 sw=4 sts=4 sr noet
   ```

   ![image]

7. Buat folder **strix.operation.wise.a04.com** di dalam **/var/www**

   ```bash
   mkdir /var/www/strix.operation.wise.a04.com
   ```

8. Unduh file website

   ```bash
   wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1bgd3B6VtDtVv2ouqyM8wLyZGzK5C9maT' -O strix.operation.wise.zip
   ```

9. Unzip file website

   ```bash
   unzip strix.operation.wise.zip
   ```

10. Pindahkan semua file website ke **/var/www/strix.operation.wise.a04.com**

    ```bash
    mv strix.operation.wise/* /var/www/strix.operation.wise.a04.com
    ```

    ![image]

11. Aktifkan konfigurasi website

    ```bash
    a2ensite strix.operation.wise.a04.com.conf
    ```

12. Restart apache

    ```bash
    service apache2 restart
    ```

**Testing**

- Buka **SSS**
- Ketik command `lynx 10.1.2.3:15000`
  ![image]

## Soal 15

Pada soal ini diminta untuk memberikan autentikasi dengan username `Twilight` dan password `opStrix` pada webserver **www.strix.operation.wise.a04.com**.

**Penjelasan**

1. Buka **Eden**
2. Buat username dan password

   ```bash
   htpasswd -b -c /etc/apache2/.htpasswd Twilight opStrix
   ```

   ![image]

3. Ubah **/etc/apache2/sites-available/strix.operation.wise.a04.com.conf**
   ```bash
   nano /etc/apache2/sites-available/strix.operation.wise.a04.com.conf
   ```
   ![image]
4. Buat file **.htaccess** di dalam **/var/www/strix.operation.wise.a04.com**

   ```bash
   nano /var/www/strix.operation.wise.a04.com
   ```

5. Sesuaikan isinya seperti berikut

   ```bash
   AuthType Basic
   AuthName "Restricted Content"
   AuthUserFile /etc/apache2/.htpasswd
   Require valid-user
   ```

   ![image]

6. Restart apache

   ```bash
   service apache2 restart
   ```

**Testing**

- Buka **SSS**
- Ketik command `lynx 10.1.2.3:15500`
- Masukkan username `Twilight`
  ![15t1]
- Masukkan password `opStrix`
  ![15t2]
- Tampil halaman web
  ![15t3]

## Soal 16

Pada soal ini diminta untuk mengarahkan IP Eden (**10.1.2.3**) ke **www.wise.a04.com**.

**Penjelasan**

1. Buka **Eden**
2. Buat file .htaccess pada /var/www/html

   ```bash
   nano /var/www/html/.htaccess
   ```

   ```
   RewriteEngine On
   RewriteBase /
   RewriteCond %{HTTP_HOST} ^10\.1\.2\.4$
   RewriteRule ^(.*)$ http://www.wise.a04.com [L,R=301]
   ```

   ![image]

3. Ubah /etc/apache2/sites-available/000-default.conf

   ```bash
   nano /etc/apache2/sites-available/000-default.conf
   ```

4. Sesuaikan isinya seperti berikut

   ```bash
   <VirtualHost *:80>
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/html

       <Directory /var/www/html>
           Options +FollowSymLinks -Multiviews
           AllowOverride All
       </Directory>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

   ![image]

5. Restart apache

   ```bash
   service apache2 restart
   ```

**Testing**

- Buka **SSS**
- Ketik command `lynx 10.1.2.3`
  ![16t]

## Soal 17

Pada soal ini diminta untuk mengarahkan request gambar yang memiliki substring `eden`ke `eden.png` pada webserver **www.eden.wise.a04.com**.

**Penjelasan**

1. Buka **Eden**
2. Buat file **.htaccess** pada **/var/www/eden.wise.a04.com**

   ```bash
   nano /var/www/eden.wise.a04.com/.htaccess
   ```

3. Sesuaikan isinya seperti berikut

   ```bash
   RewriteEngine On
   RewriteRule ^(.*)eden(.*)$ http://www.eden.wise.a04.com/public/images/eden.png [L,R]
   ```

   ![17a]

4. Ubah **/etc/apache2/sites-available/eden.wise.a04.com.conf**

   ```bash
   nano /etc/apache2/sites-available/eden.wise.a04.com.conf
   ```

   ```
   <VirtualHost *:80>
       ServerName eden.wise.a04.com
       ServerAlias www.eden.wise.a04.com
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/eden.wise.a04.com

       <Directory /var/www/eden.wise.a04.com>
           Options +FollowSymLinks -Multiviews
           AllowOverride All
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public>
           Options +Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/css>
           Options -Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/images>
           Options -Indexes
       </Directory>

       <Directory /var/www/eden.wise.a04.com/public/js>
           Options -Indexes
       </Directory>

       ErrorDocument 404 /error/404.html

       Alias "/js" "/var/www/eden.wise.a04.com/public/js"

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

   ![17b]

5. Restart apache

   ```bash
   service apache2 restart
   ```

**Testing**

- Buka **SSS**
- Ketik command `lynx www.eden.wise.a04.com/aeden12.png` (dilakukan sebelum nomor 11)
  ![image](https://user-images.githubusercontent.com/76677130/139530612-82ad6716-e7f6-4edd-b12a-b49ed61a1381.png)

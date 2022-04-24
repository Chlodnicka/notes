# Konfiguracja Xdebuga (macOS, PhpStorm, Docker, Symfony)

# Docker:

## docker/Dockerfile
```dockerfile
FROM php:8.0-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl

RUN apt-get update && apt-get install -y procps && rm -rf /var/lib/apt/lists/*

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# XDEBUG
RUN pecl install xdebug-3.0.3
RUN docker-php-ext-enable xdebug

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
```

## docker/default.conf

```
server {
    index index.php index.html;
    server_name test.local;
    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
    root /var/www/html/public;
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass php-fpm:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
}
```

## docker/conf.d/xdebug.ini

```
zend_extension=xdebug

[xdebug]
xdebug.mode=develop,debug
xdebug.client_host=host.docker.internal
xdebug.client_port=9003
xdebug.start_with_request=yes
xdebug.max_nesting_level=1500
```

## docker/conf.d/error_reporting.ini

```
error_reporting=E_ALL
```

## docker-compose.yaml

```
version: '3'

services:
    web:
        image: nginx:latest
        ports:
            - "80:80"
            - "443:443"
        volumes:
            - ./:/var/www/html
            - ./docker/default.conf:/etc/nginx/conf.d/default.conf
        networks:
            - super-umbrella
    php-fpm:
        build:
            context: .
            dockerfile: docker/Dockerfile
        volumes:
            - ./:/var/www/html
            - ./docker/conf.d/xdebug.ini:/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
            - ./docker/conf.d/error_reporting.ini:/usr/local/etc/php/conf.d/error_reporting.ini
        networks:
            - super-umbrella

networks:
    super-umbrella:
        driver: bridge
```

# Konfiguracja PhpStorm

1. Ustaw interpreter
    ![](./resources/1.png)
    ![](./resources/2.png)

2. Upewnij się, że ścieżki mapowania między kontenerem a lokalnymi plikami są poprawne
    ![](./resources/3.png)

3. Ustaw konfigurację Debuggera
    ![](./resources/10.png)
    ![](./resources/11.png)

4. Ustaw konfigurację Serwera (upewnij się że ścieżki są zmapowane poprawnie)
    ![](./resources/18.png)

5. Ustaw konfigurację Composera
    ![](./resources/4.png)

6. Ustaw konfigurację PhpUnita
    ![](./resources/5.png)
    ![](./resources/6.png)
    ![](./resources/7.png)

7. Można zrestartować PHPStorma i odpalić Dockera po restarcie

8. Można odpalać testy z poziomu IDE
    ![](./resources/8.png)
9. Można odpalać testy z poziomu IDE razem z Coverage
    ![](./resources/9.png)
10. Można odpalać debugowanie z poziomu testów
    ![](./resources/12.png)
    ![](./resources/13.png)
11. Naciskamy ikonkę z "Start Listening for PHP Debug Connection" - prawy górny róg
    ![](./resources/14.png)
12. Odpalamy w przeglądarce aplikację (zgodnie z tym co wpisaliśmy w pkt. 4)
    ![](./resources/19.png)
13. Wywalamy nasze `xdebug_info()` i wracamy do pierwotnej wersji
    ![](./resources/15.png)
14. Stawiamy kropy, odświeżamy stronę, w PhpStormie powinna nam się odpalić zakładka z Debbugerem 
(aby przejść do kolejnego breakpointa - fachowa nazwa na czerwoną kropę - klikamy na zieloną strzałkę - pierwsza po lewej w okienku Debuggera)
    ![](./resources/16.png)
15. Jak dotrzemy do końca (klikając zieloną strzałkę) to w końcu pozwolimy na wykonanie requestu do końca
    ![](./resources/17.png)
16. Możemy testować również z poziomu klienta http wbudowanego w PhpStorma
17. Odpalamy dokumentację w formacie np. OpenApi
    ![](./resources/20.png)
18. Ustawiamy autoryzację (Authorize)
    ![](./resources/21.png)
    ![](./resources/22.png)
19. Generujemy cURLa requestu na podstawie dokumentacji OpenApi (Try it out -> Execute)
    ![](./resources/23.png)
    ![](./resources/24.png)
    ![](./resources/25.png)
    ![](./resources/26.png)
20. Konwertujemy cURLa na format klienta http PhpStorma
    ![](./resources/27.png)
    ![](./resources/28.png)
21. Jeśli chemy odpalić request trzeba wyłączyć nasłuchiwanie Xdebuga i odpalić request
    ![](./resources/29.png)
    ![](./resources/30.png)
22. Jeśli chemy odpalić debugger z requestu trzeba włączyć nasłuchiwanie Xdebuga, 
odpalić request, odpali się okienko Debuggera i leci z koksem (zielona strzałka -> Resume program)
    ![](./resources/31.png)
    ![](./resources/32.png)
    ![](./resources/33.png)
    ![](./resources/34.png)


## Jeśli docker skonfigurowany poza projektem 

1. Trzeba doinstalować tam Xdebuga 
2. Skonfigurować częśc rzeczy w PhpStormie jak poniżej (reszta tak samo)

![](./resources/35.png)
![](./resources/36.png)
![](./resources/37.png)
![](./resources/38.png)




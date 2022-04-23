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
    ![](./resources/Screenshot 2022-04-21 at 19.09.14.png)
    ![](./resources/Screenshot 2022-04-21 at 19.09.46.png)

2. Upewnij się, że ścieżki mapowania między kontenerem a lokalnymi plikami są poprawne
    ![](./resources/Screenshot 2022-04-21 at 19.10.10.png)

3. Ustaw konfigurację Debuggera
    ![](./resources/Screenshot 2022-04-21 at 19.47.56.png)
    ![](./resources/Screenshot 2022-04-21 at 19.50.04.png)

4. Ustaw konfigurację Serwera (upewnij się że ścieżki są zmapowane poprawnie)
    ![](./resources/Screenshot 2022-04-21 at 20.40.49.png)

5. Ustaw konfigurację Composera
    ![](./resources/Screenshot 2022-04-21 at 19.11.42.png)

6. Ustaw konfigurację PhpUnita
    ![](./resources/Screenshot 2022-04-21 at 19.12.14.png)
    ![](./resources/Screenshot 2022-04-21 at 19.12.22.png)
    ![](./resources/Screenshot 2022-04-21 at 19.12.33.png)

7. Można zrestartować PHPStorma i odpalić Dockera po restarcie

8. Można odpalać testy z poziomu IDE
    ![](./resources/Screenshot 2022-04-21 at 19.28.21.png)
9. Można odpalać testy z poziomu IDE razem z Coverage
    ![](./resources/Screenshot 2022-04-21 at 19.28.38.png)
10. Można odpalać debugowanie z poziomu testów
    ![](./resources/Screenshot 2022-04-21 at 19.52.44.png)
    ![](./resources/Screenshot 2022-04-21 at 19.52.56.png)
11. Naciskamy ikonkę z "Start Listening for PHP Debug Connection" - prawy górny róg
    ![](./resources/Screenshot 2022-04-21 at 19.56.01.png)
12. Odpalamy w przeglądarce aplikację (zgodnie z tym co wpisaliśmy w pkt. 4)
    ![](./resources/Screenshot 2022-04-21 at 20.52.21.png)
13. Wywalamy nasze `xdebug_info()` i wracamy do pierwotnej wersji
    ![](./resources/Screenshot 2022-04-21 at 20.31.53.png)
14. Stawiamy kropy, odświeżamy stronę, w PhpStormie powinna nam się odpalić zakładka z Debbugerem 
(aby przejść do kolejnego breakpointa - fachowa nazwa na czerwoną kropę - klikamy na zieloną strzałkę - pierwsza po lewej w okienku Debuggera)
    ![](./resources/Screenshot 2022-04-21 at 20.32.02.png)
15. Jak dotrzemy do końca (klikając zieloną strzałkę) to w końcu pozwolimy na wykonanie requestu do końca
    ![](./resources/Screenshot 2022-04-21 at 20.32.12.png)
16. Możemy testować również z poziomu klienta http wbudowanego w PhpStorma
17. Odpalamy dokumentację w formacie np. OpenApi
    ![](./resources/Screenshot 2022-04-21 at 21.31.15.png)
18. Ustawiamy autoryzację (Authorize)
    ![](./resources/Screenshot 2022-04-21 at 21.32.03.png)
    ![](./resources/Screenshot 2022-04-21 at 21.32.06.png)
19. Generujemy cURLa requestu na podstawie dokumentacji OpenApi (Try it out -> Execute)
    ![](./resources/Screenshot 2022-04-21 at 21.32.22.png)
    ![](./resources/Screenshot 2022-04-21 at 21.32.25.png)
    ![](./resources/Screenshot 2022-04-21 at 21.32.28.png)
    ![](./resources/Screenshot 2022-04-21 at 21.32.56.png)
20. Konwertujemy cURLa na format klienta http PhpStorma
    ![](./resources/Screenshot 2022-04-21 at 21.33.14.png)
    ![](./resources/Screenshot 2022-04-21 at 21.33.18.png)
21. Jeśli chemy odpalić request trzeba wyłączyć nasłuchiwanie Xdebuga i odpalić request
    ![](./resources/Screenshot 2022-04-21 at 21.33.29.png)
    ![](./resources/Screenshot 2022-04-21 at 21.35.30.png)
22. Jeśli chemy odpalić debugger z requestu trzeba włączyć nasłuchiwanie Xdebuga, 
odpalić request, odpali się okienko Debuggera i leci z koksem (zielona strzałka -> Resume program)
    ![](./resources/Screenshot 2022-04-21 at 21.35.48.png)
    ![](./resources/Screenshot 2022-04-21 at 21.36.28.png)
    ![](./resources/Screenshot 2022-04-21 at 21.36.33.png)
    ![](./resources/Screenshot 2022-04-21 at 21.36.40.png)


## Jeśli docker skonfigurowany poza projektem 

1. Trzeba doinstalować tam Xdebuga 
2. Skonfigurować częśc rzeczy w PhpStormie jak poniżej (reszta tak samo)

![](./resources/Screenshot 2022-04-23 at 10.47.40.png)
![](./resources/Screenshot 2022-04-23 at 10.48.26.png)
![](./resources/Screenshot 2022-04-23 at 10.48.58.png)
![](./resources/Screenshot 2022-04-23 at 10.49.17.png)




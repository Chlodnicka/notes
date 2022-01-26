# Intro

https://github.com/legacyfighter/cabs-php
https://github.com/legacyfighter/cabs-java

## Dług techniczny

1. świadoma decyzja o poświęceniu jakości kodu dla innych celów, np szybki deploy jakiejś funkcjonalności
2. jak kredyt na mieszkanie -> mamy wcześniej mieszkanie, ale musimy spłacić odsetki 
3. czy dług jest zły? nie -> niespłacany dług jest problemem
4. każdy projekt ma dług techniczny
5. jeśli degradujemy jakość kodu świadomie i rozważnie, to możemy na tym wyjść bardzo dobrze
6. nieświadomy dług to w zasadzie nie jest dług - tylko bałagan w repo
7. refaktor to trochę spłata długu + odsetki
8. obserwowalne zachowania - czyli co to coś robi - przy refaktorze zmieniamy JAK coś działa/coś robi, nie CO to coś robi
9. rewrite / refaktor - rewrite na nową technologię, rewrite funkcji może być refaktorem klasy itd. - zakresy

## Obserwowalne zachowania

1. Duże systemy z dużą ilością obserwowalnych zachować budzą strach przed zmianą
2. Wydzielaj "pojedyncze" obserwowalne podzachowania -> tylko czasem jest smutno, bo patrzymy na funkcję, a tu klops - jest tak napisana że nie wiadomo co to robi
3. można wtedy szukać info w przypadkach użycia danej funkcji, testów (jeśli są), doświadczonych kolegów, użytkowników gui
4. gorzej, jak nie wiemy co dokładnie jest obserwowalnym zachowaniem naszego kodu i przywiązujemy się do istniejącej implementacji i z nią zaczynamy utożsamiać rozwiązanie
5. wydzielaj coraz drobniejsze obserwowalne zachowania dla kolejnych modułów/użytkowników
6. jeśli znamy jakieś pojedyncze obserwowalne zachowania i wiemy co ten kod robi -> możemy dopisać test
    * to nie jest łatwe, bo w legacy zazwyczaj logika zachowania jest bardzo rozmyta np. już w kontrolerach
    * więc może lepiej dopisać smutny test e2e / integracyjny na kontrolerze i mieć taki co sprawdza rzeczywiście, niż żaden
    * i lepiej taki, co możemy odpalić lokalnie, niż żaden

## Zwrot z inwestycji

1. Gdzie warto dbać o wysokiej jakości kod - tam gdzie się często zmienia / tam gdzie się rzeczywiście opłaca (np. wydajność)
2. `git log --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10`

## Generalna ścieżka refaktoryzacji

1. Nazwij problem - jak nie określimy problemy to zwrotu z inwestycji może nie będzie - 
    * potrzebujemy czytelności? wydajności? testowalności? mamy niespójne dane? mamy dużo duplikacji kodu, który zawsze zmienia się razem i wydłuża czas developmentu i ułatwia popełnienei błędu?
    * chcemy osiągnąć jakiś efekt
2. Dobierz rozwiązanie 
3. Zaplanuj zmiany - gdzie zacząć, jak zabezpieczyć się przed błędami -> przy dużych zmianach, po każdym kroku trzeba zrewidować, czy zbliżamy się do osiągnięcia celu / weryfikacji planu

## Event storming w legacy

...

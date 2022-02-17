# Refaktoryzacja do wzorca Value Object

## Problem powielonej walidacji 
* _Shotgun surgery_

Czy i jak? Pytania:
1. Jak duzym problemem dla projektu  i zespołu jest powielenie logiki walidacyjnej?
2. W ilu miejscach logika walidacyjna została powtórzona?
3. Jaka jest historia zmian tej logiki?
4. Czy w niedalekie jprzyszłości planowane są jej zmiany?
5. Czy potencjalna zmiana jest jednorazowa?
6. Czy korzystanie z silneg otypowania i nowego typu przyniesie zysk?

## Generalna ścieżka refaktoryzacji

1. Zapewnij bezpieczeństwo zmiany (testy oparte o odkryte obserwowalne zachowania)
2. Wprowadź nowy koncept i umieść w nim logikę walidacji
3. Podłącz nowy obiekt i upewnij się że obserwowalne zachownaia pozostały niezmienione
4. Zaobserwój efekt i podejmij decyzję odnośnie dalszych działań

Użycie narzędzi, technik, wzorców dopasowujemy do konkretnej sytuacji, problemów, projektu - nie bo chcemy, coś jest nowe, coś nam się podoba. 

## Zmienna reprezatacja konceptu domenowego (ceny - wartość, waluty - przykład jak z koszykiem xD)

1. Obiekt ukrywa swoją zmienność za stabilnym interfejsem, łatwiej się zmienia się kod stojący za nim, bez strachu o pominięcie czegoś
2. Stabliny interfejs, na którym opieramy test. Zmiany za interfejsem nie wpływają na jego klientów. TDD może być tu pomocne

### Wyłanianie stabilnego interfejsu

1. Zdefiniuj obserwowalne zachowania
2. Nie ujawniaj szczegółów implementacyjnych
3. Jak wpadniesz na lepszy pomysł to usuniesz gorszy bez żalu
4. Stabilny interfejs sprawia, że kod za nim jest łatwy do usunięcia / zastąpienia. Usuwalność kodu to dobra cecha - oznacza, że jest dobrze odseparowany od reszty. 
Może być driverem architektonicznym jak testowalność, czytelność czy skalowalność

* spirala refaktoryzacji
 
* zaczynaj od refaktoru najcieższego miejsca, najszybciej dowiesz się o rzeczach nieprzewidzianych, dodatkowych problemach

### Extract method
* do osobnej metody logiczny i spójny fragment

### Move method
* przeniesienie metody do klasy, wewnątrz której coś znaczy, zwiększenie spójności danej klasy, zaenkapsulowanie jej logiki

* zwiekszanie lokalnej czytelności kodu, zmniejszenie lokalnej złożoności, zwiększenie kohezji (spójności)

* małe kroki, łatwo zmienić decyzję, łatwo się wycofać

### Jak?

1. Czy dana cecha zawsze wygląda tak samo? 
2. Czy w najbliższym czasie się będzie zmieniać?
3. Ile miejsc trzeba zmienić?
4. Czy kilka różnych reprezentacji może funkcjonować równolegle? 

### Projektowanie nowego obiektu / stabilnego interfejsu

1. Przejrzyj kod kliencki, jaki jest powód do zmiany? 
2. Czy propozycja rozwiązania ma sens? Zasymuluj hipotetyczną zmianę wymagań i upewnij się, czy "dobrze myślisz"
+ Generalna ścieżka refaktoryzacji

* Zasada wspinacza - zmiana tylko kodu produkcyjnego lub tylko testowego

## Problem zmiennej prezentacji

1. Różnorodność prezentacji - gdy w systemie nie ma większego znaczenia jak reprezentujemy dystans (km, mile itd)
2. I mamy problem że chcemy wyświetlić nasz dystans w różny sposób w zależności od np. geolokalizacji naszego użytkownika
3. Czasem po zmianie kod wygląda podobnie, ale przeniesiony w inne miejsce poprawia czytelność.

### Jak?

1. Potrzebujemy prezentowania tej samej rzeczy na różne sposoby
2. Ile różnych sposobów prezentacji występuje?
3. Czy prezentacje są w wielu miejscach?
4. Czy będą nowe sposoby prezentacji?
5. Czy przeliczamy jedne w drugie z użyciem skomplikowanych obliczeń?
6. Nie uprawiaj overengeeneringu


## Problem ukrytego konceptu domenowego

### Jaki problem?

1. Powtórzenie logiki w dwóch / wielu różnych miejscach -> często zmieniają się w tym samym momencie
2. Silne przywiązanie do jednego sposobu działania
3. Nieczytelność

Niejawna duplikacja kodu -> może to osobny koncept / byt, zlepek kliklu pojedynczych pól to być może koncept wspólny

_Make the Implicit Explicit_ - jeśli jakiś koncept domenowy trzeba wywnioskować z kodu to czytelniej będzie ten koncept jawnie zamodelować

### Jak?

1. Problem wyjściowy: dyplikacja, niestabilność, wspacie tylko jednego sposobu działania, brak jasnego odwzorowania konceptu 
2. Czy wprowadzam zmianę i muszę zmieniać wiele miejsc w podobny sposów 
3. Jest jakieś logiczne połączenie między tymi danymi?
4. Jaka jest historia i częstotliwość zmian?
5. Szybka symulacja zmiany wymagań?

## Value object - Obiekt repreztujący wartość

1. Opisuje cechy konkretnego konceptu
2. niemutowalny
3. wiąże wiele atrybutów w logiczną całość
4. jest łatwo wymienialne z użyciem stabilnego interfejsu
5. nie posiada tożsamożci, jest identyfikowany przez właściwości atrybutów (dwa obiekty money o takiej samej cenie i walucie można zamieć i nic się nie stanie)
6. porównanie z innym obiektem następuje przez porównanie wartości atrybutów


* odwzorowuje w modelu konkrety element biznesowy
* enkapsuluje logikę
* poprawia czytelność, testowalność
* ułatwia prowadzanie dalszych zmian w systemie 
* sprzyja unikaniu przypadkowych błędów 

## Logika ortogonalna

[Better software design - O programowaniu aspektowym z Andrzejem Krzywdą - Mariusz Gil
](https://bettersoftwaredesign.pl/episodes/7)

1. Model aspektowy: 
    * joint point - zdefiniowany punkt w trakcie wykoania programu np. wywołanie metody, 
    * point cut - wyrażenie określające zbiór join pointów, 
    * advice - akcja wykonywana w konkretnym join pointcie, 
    * aspect - jednostka modularyzacji 
    
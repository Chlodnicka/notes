# Agregat

##  Jaki problem mamy - brak spójnej zmiany, brak spójności danych

1. Możliwość wprowadzenia systemu w dowolny stan
2. Możliwość ominięcia reguł
3. Wyciek wewnętrznej struktury obiektu na zewnątrz

Częste błędy jeśli zaczyna się od modelu bazy danych, rzeczowników.

1. Najłatwiej zapewnić spójnośc poprzez trzymanie reguł i danych w jednym miejscu za stablinym
interfejsem, który enkapsuluje reguły i dane
2. W ten sposób to tylko obiekt wie, jakie ma reguły i jakie ma pola
3. Pozwala to na jego lokalną refaktoryzację

### Przywracanie klasom należnej enkapsulacji
* jak przerzucamy zestaw setterów na konstruktor to powinniśmy się upewnić, że kolejność nie jest ważna lub została zachowana
* usuwanie setterów i enkapsulacja zachowań sprawia, że nie jesteśmy w stanie wprowadzić obiektu w dowolny stan
* co z refleksją? (dynamicznym tworzeniem i wywoływaniem metod)
* co z konsekwencjami decyzji (np notyfikacja, logi)

### Pytania
1. Czy mamy powtarzające się sekwencje setterów
2. Czy w przypadku zmiany należy zmodyfikować wiele róznych miejsc o wywołanie settera?
3. Czy pominięcie któregoś settra sprawia, że system będzie w stanie niespójnym, wywoła jakieś konsekwencje?
4. Czy za pomocą setterów można wprowadzić obiekt w dowolny (niespójny) stan?
5. Czy występują cykle: pobierz wartość - sprawdzć wartość - ustaw dane?

W legacy zachowania tego typu zazwyczaj odbywają sięw serwisach, nie w obiekcie dedykowanym

### Przywracanie enkapsulacji

1. Nowe metody dostępowe (mówiące explicite co robią, z intencją co robi np. )
    * jak biznes nazywa tę operację
    * czy nazwa ujawnia szczegóły implementacyjne 
    * czy nazwa nie sugeruje jednego konkretnego rozwiązania
    * jak nam nie idzie -> nie kmin za długo, wybierz coś - może nam to przyjdzie z czasem
2. Usuń możliwe gettery / settery
3. Wrzuć logikę i warunki do tych nowych metod dostępowych (pkt 1)

##  Jaki problem mamy - zbyt dużego obiektu / zbyt dużej transakcji bazodanowej

* metryki systemowe -> przegląd wywołań do bazy  danych
* przegląd logów, zrzuty wątków 
* problem często materializuje się przy większej skali (zachowanie dostępności przy zwiększaniu się skali)
* jeśli nasza klasa ma zbyt duży obszar odpowiedzialności to bardzo prawdopodobne, że przy większej skali dostaniemy w twarz problem ze współbieżnym dostępem do danych

### Strategie rozwiązania problemu write-write

1. Ostatni wygrywa -> dopuszczamy możliwość nadpisania nowszego stanu w bazie danych
2. Pierwszy wygrywa -> działamy na najświeższej wersji systemu, blokowanie optymistyczne (ORM) 
3. ACID + poziom izolacji transakcji + zapis, gdy wersja obiektu się zgadza z tym co mamy w bazie danych

### Write - read / write write

1. Długi czas zapisu może spowodować, że odczyt czeka, czasem też ready się mogą wzajemnie zlockować
2. Dobra praktyka jest dobra, dopóki ktoś nie znajdzie lepszej
3. Czy współbieżny dostęp do danych może doprowadzić do złamania reguł biznesowych?
4. Jakiego mechanizmu blokowania użyjemy? 
5. Czemu nasza aplikacja długo czyta / długo zapisuje dane?
6. Rozłączenie danych -> fizyczna zmiana granic danych - trzeba będzie ewentualnie czytać z dwóch miejsc
7. Niezależne biznesowo operacje powinny być niezależne technicznie (dosłownie: nie jest to ten sam rekord)

### Strategia podziału obiektu

1. Czy dane, które chcę separować są związane ze sobą jakąś regułą? 
2. Trzymanie bliskich sobie danych i reguł razem
3. Wynoś prawdziwych problematycznych sąsiadów, nie siebie 
(jak przeszkadza Ci sąsiad i blokuje dostęp do windy to przeprowadzasz się czy próbujesz coś innego zrobić? 
czy to rozwiąże twój problem - tak, czy innych sąsiadów - nie) - Separacja często zmieniającej się danej
4. _lost update_ - zgubiony update - trzeba zastanowić się jak działa orm
   * blokowanie optymistyczne vs pesymistyczne
   * inkrementacje są spoko czasem w sql
   * _dirty checking_
5. Niezależne funkcje biznesowe powinny być niezależne technicznie
6. O decyzji technicznej przy refaktorze można myśleć jak o dźwigni - poświęcamy mało w miniej istotnej częsci systemu, zyskujemy w innej, istotniejszej
7. Deadlocki -> ponawianie też generuje ruch na bazie (roundtripy bazodanowe -> może join?)

### Pytania pomocnicze
1. Co się dzieje z danymi? 
2. W jaki sposób są one wykorzystywane? 
3. W jakim celu zostały wyświetlone? 
4. Czy na ich podstawie podejmowane są ważne decyzje biznesowe?

Jeśli jakieś dane są ze sobą związane silną regułą, należy zapewnić ich spójność, zarówno podczas zapisu i odczytu. 

### Strategia migracji danych

1. Np. przerwa serwisowa: wyłączenie systemu -> migracja -> testy -> włączenie systemu
2. Zero downtime - aplikacja musi działać cały czas -> skrypt migracyjny w tle 
(zmiana danych podczas migracji, nałożenie się w czasie i niezapisanie np. akcji uzytkownika)
jeśli jest to problem -> to robimy to krokowo, zapisujemy w dwóch miejscach jednocześne -
możemy wtedy np. popełnić błąd i wycofać zmiany bez większego wpływu na cały system 
3. Migracji danych poświęcono całe książki xD

#### Nie naprawiaj wszystkiego na raz

1. Czy klient tego kodu nie nauczył się już żyć z tym błędem i nie wprowadzono procesów akcji kompensujących? - system informatyczny to część większego systemu biznesowaego
2. Zapytaj eksperta domenowego / biznesu co o tym myśli - decyzja o naprawie logiki powinna być świadoma
3. Odseparuj poprawkę logiki od refkatoryzacji (choćby commitem)

### Pytania

1. Czy użytkownicy zauważają okresy o większej / mniejszej dostępności funkcji systemu
2. Czy w logach można zauwazyć błędy potencjalnie związane z zapisami i  z blokowaniem optymistycznym
3. W jaki sposób projektpway/refaktoropwany obiekt będzie używany? Ile różnych akcji biznesowych będzie go zmieniać? Jak często się będą wykonywać?
4. Czy probelm dotyka wszsystkich czy wybranego klienta (klienta / działu)

### Kroki

1. Zidentyfikuj problematyczną daną
2. Odseparuj daną
3. Określ sposób migracji danych pomiędzy
4. Zastanów się nad potrzebą stosowania blokowania optymistycznego zapisu

#### Pisz testy na poziomie obserwowalnych zachowań i pokrywaj logikę biznesową  i jej reguły

## Pomieszanie logiki domenowej i procesowej

1. Często wtedy nie jesteśmy w stanie napisania testu jednostkowego
2. Próba napisania testu wyższego poziomu wymaga odcięcia wielu zależności i zaślepienia ich
3. Koszt i trudność napisania testu może powodować, że ten test nigdy nie powstanie 
4. Jak w takim przypadku pokryć obserwowalne zachowanie testem?

### Rodzaje logiki

Heurystyki:
1. Logika walidacyjna - potrzebuje jakich danych wejściowych, opisuje waruniki ich poprawności, 
nie wymaga ani nie sprawdza dodatkowych danych z systemu (np bazy danych), czy aktualnego stanu systemu
2. Logika biznesowa - opisuje spójną zmianę stanu pod pewnymi warunkami, 
pewne zmiany muszą być przeprowadzone od razu, pewne mogą zostać odroczone,
wymanage jest zablokowanie pewnych danych, w celu niknięcia utraty spójności
3. Logika procesowa (proces biznesowy - często jeśli coś to coś), często rozciągnięta w czasie (godzin, dni),
opisuje przebieg długotrwałego procesu biznesowego np. kolejno realizowane konsekwencje pewnych decyzji,
zawiera sformułowania w postaci "jeśli, to wtedy, następnie", 
można ją podzielić na szereg mniejszych kroków i wykonywać etapami, jakie działania kształtują ten proces 
(np. operator coś klika, ktoś coś zatwierdza, musi minąć jakiś czas od zgłoszenia itd)

### Jak rozwiązać problem?

1. Trzymaj dane i zachownia bliko siebie
2. Nadawaj intencje kaskadom zmian danych
3. Przenoś logikę do metod biznesowych

* Wprowadzając nowy koncept odroczmy nazwanie
* to podjęcie decyzji o sposobie rozwiązania reklamacji musi być wykonane spójnie
* kolejne działania w systemie to konsekwencje tych decyzji, mogą zostać odroczone w czasie
* _siły rozpychające nasz design_ - drivery architektoniczne

Kod odpowiada jednocześnie za podjęcie decyzji, odłożenie stanu i propagowanie/przetwarzanie jej konsekwencji

### Wyznaczenie granicy obiektu, częśc danych do parametrów
1. Jaka odpowiedzialność ma dany obiekt, jakich danych w tym celu potrzebujemy?
Czy dane są dodatkowe? Czy to dane istotne, wpływające na spójność zmiany? - odczytując dane bez blokowania godzimy się na roszczelnienie spójności
2. Zestaw blokowanych danyc hpowinien być podyktowany przede wszystkim kontrolą spójności
3. Można uniknąć blokowania zb byt wielu danyc hjednocześnie np. jeśli yżycie nieaktualnych danych nie jest problemem lub dopuszcza się ich zmianęw trakcie, w innych procesach


1. Logikę domenową warto wrzucić w deydkowany obiekt, który odpowiada za spójną zmianę stanu
2. Logikę procesową warto trzymać w wyższej warstwie, np. w  serwisie / handlerze / innym dedykowanym obiekcie (gdy jest rozbudowana / zmienna)

### Symptomy

1. Nagromazenie instrukcji warunkowych o różnym przeznaczeniu
2. Trudność implementacji testu logiki biznesowej, potrzeba tworzenia wielu zaślepek dla zewnętrznych komponentów

### Pomocne pytania

1. Które instrukcje są powiązane z podejmowaniem decyzji, które z obsługą konsekwencji?
2. Czy dopuszczalne jest opóźnienie wykoania fragmentów kodu? Których?
3. Jaki jest charakter zaślepek?

Załóż że żadne oprogramowanie nie istnieje, a wszystkie czynności są wykonywane ręcznie:
1. Kto w ogranizacji zajmuje sięwykonaniem testowanej czynności?
2. Jakie decyzje podejmuje taka osoba, a jakie działania zleca innym pracownikom?
3. Jakich informacji taka osoba potrzebuje w celu podjęcia decyzji? Jakie jest źródło pochodzenia tych danych?
4. Jak te informacje są utrwalane i dlaczego?
5. Jakie konsekwencje powoduje wykorzystanie przez taką osobę nieaktualnych danych?
6. W jaki spośób taka osoba współpracuje z innymi pracownikami? Jak się z nimi komunikuje?
7. Czy wynik wykonania tych zleconych rzeczy ma wpływ na finalną decyzję? Czy decyzja już zapadła i to, że ktoś czegoś nie zrobił nie ma na nią wpłuwu 

Czasem trafiamy na jednostkę koordynującą działania innych części organizacji zamiast na jednostkę podejmującą decyzję. 

## Problem dużej zmeinności reguł biznesowych

1. Mnogość reprezentacji - koncept może być reprezentowany na wiele róznych sposobów
2. NIespójność to efekt braku enkapsulacji i wyrzuca
3. Zmienność reprezentacji można ukryć za stablinym interfejsem
4. Reguły mogą być rozpięte na wiele obiektów różnego typu
5. Jednocześnie musimy obsługiwać różne reprezentacje (np. algorytmów wyliczania ceny, naliczania / wygaszania punktów lojalnościowych)

* Uproszczenie poprzez pozorne skomplikowanie 
* Cwiczenia wizualizacyjne - szkice reprezentujące przypadki - szukanie kolejnych przypadków w celu znalezienia nadrzędnej reguły 
na razie mamy dwa różne sposoby wygasania punktów lojalnościowych, ale w sumie moze za jakiś czas to się zmieni
możemy poćwiczyc wymyślanie różnych nowych przypadków, żeby odkryć jakąś "ogólną, nadrzędną" zasadę rządzącą tymi przypadkami
* algorytm ukryty za interfesjem przekazywany do metody (strategia liczenia ceny)
* zmiany addytywne są łatwiejsze do wprowadzania

* jedna metoda: sprawdza reguły, dostrojenia decyzji i wykonania decyzji (czasem te bloki są oddzielone, czasem pomieszane i trzeba je najpierw oddzielić)
* częściej zmienia się logika dostrojenia decyzji niż samo wykonanie 
* separacja kodu zmienego od stabilnego -> szukaj stabilnej części procedura, który mówi o tym "jak wykonuje się decyzji", ta stabilna część będzie dostarajana zmiennymi politykami:
* np. wybierz odpowiedni do warunków wstępnych algorytm sortowania, przekaż kontretny algorytm sortowania jako parametr do metody, wywołaj sortowanie w metodzie i jej wynik przekaż do kodu, ktory wykona decyzję (np. zapisze odpowiednie dane, zwróci output, wyśle eventy)
* polityki i strategie - dziel i rządź w warunkach programowania obiektowego
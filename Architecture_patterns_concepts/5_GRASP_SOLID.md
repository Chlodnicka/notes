# GRASP, SOLID

## OOP

### Abstrakcja

Bierz to co potrzebne w danym kontekście, ukryj to wewnątrz.

### Hermetyzacja, enkapsulacja

Ukryjże tę implementację, nie pozwól jej wyciec. Klientów nie interesuje jak to robisz, bylebyś zrobił poprawnie. Część
danych, których potrzebujesz do działania, nie może być zmieniana zzwesnątrz. Trzeba ich strzec.

### Polimorfizm

Po interfejsach (podstawiamy różne typy implementacji)

### Dziedziczenie

Po klasach

## SOLID

### Single responsibility principle

Klasa powinna mieć jeden zakres odpowiedzialności - robić jedną rzecz dobrze

### Open/closed principle

Otwarty na rozszerzenia, zamknięty na modyfikacje. Np. przy wprowadzaniu zmian w jakimś algorytmie możemy zmienić jego
działanie dodając implementację interfejsu / wywołanie jakiejś klasy, nie wprowadzając zmiany w klasie PriceAlgorithm
która ma 400 linijek zawiłego kodu z mnóstwem ifów i randomowych dzieleń przez 3.

### Liskov substitution principle

Jak coś zależy od interfejsu / klasy to musi działać poprawnie ze wszystkimi jego/jej implementacjami / podklasami.

### Interface segregation principle

Dziel interfejsy. Interfejs z 30 metodami to raczej średni interfejs. Klasy nie powinny być zależne od interfejsów,
których nie używają.

### Dependency inversion principle

Wysokopoziomowe moduły nie zależą od niskopoziomowych - zależność wynika z abstrakcji np. chowamy implementację za
interfejsem, który przekazujemy

## GRASP (General Responsibility Assignment Software Principles)

### Information Expert

Ta klasa ma odpowiedzialność, która posiada niezbędne do jej wykonania informacje: 
np. implementacja repozytorium wybiera dane z bazy bo ma informacje o konfiguracji połączenia.

### Creator

Kto powinien stworzyć klasę?
Klasa B powinna być odpowiedzialna za tworzenie instancji klasy A wtedy gdy: 
zawiera lub agreguje klasę A, posiada dane inicjujące klasę A, zapamiętuje klasę A lub intensywnie z niej korzysta.

### Controller

Kto jako pierwszy przyjmuje i koordynuje żądaniami?
Odpowiedzialność tą powinien otrzymać obiekt, który reprezentuje system, podsystem lub scenariusz przypadku użycia.

### Low Coupling

Przydzielaj odpowiedzialności tak, żeby zależności między obiektami byly jak najmniejsze. Konstruktor z 20 zależnościami to zły pomysł.

### High Cohesion

Klasy powinny być spójne, mieć podobne dane, robić zbliżone rzeczy -> trzymaj podobne rzeczy blisko siebie.
Agregat oferty produktowej może mieć dane dotyczące dostępnej ilości i aktualnej ceny, może zrobić rezerwację na te ilości, 
wyrzucić błąd, gdy zarequestowana ilość jest mniejsza niż 0, 
ale może niekoniecznie być odpowiedzialnym za stworzenie zamówienia i zapisanie go w bazie.

### Indirection

Nie wrzucaj bezpośrednich zależności. Można spróbować wrzucić obiekt pośredniczący np. Command / Query 

### Polymorphism

Interfejsy, abstrakcje ;)

### Pure Fabrication

Jak nie mamy w systemie bytu (np. klasy), któremu jesteśmy w stanie przypisać naszą odpowiedzialność (funkcjonalność)
to tworzymy byt sztuczny (pomocniczy), który nie opisuje jakiegoś konceptu z dziedziny problemu.
W DDD może to być np. serwis domenowy spinający zachowania na kilku agregatach.

### Protected Variations

Szukaj miejsc niestabilnych (podsystemów/systemów czy też niestabilnych obiektów, których interfejs może się zmieniać)
i okrywaj je stabilnym. Najwyżej będziesz grzebał za interfejsem, ale kod kliencki nie musi się zmieniać.
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

## Przywracanie klasom należnej enkapsulacji
* jak przerzucamy zestaw setterów na konstruktor to powinniśmy się upewnić, że kolejność nie jest ważna lub została zachowana
* usuwanie setterów i enkapsulacja zachowań sprawia, że nie jesteśmy w stanie wprowadzić obiektu w dowolny stan
* co z refleksją? (dynamicznym tworzeniem i wywoływaniem metod)
* co z konsekwencjami decyzji (np notyfikacja, logi)

## Pytania
1. Czy mamy powtarzające się sekwencje setterów
2. Czy w przypadku zmiany należy zmodyfikować wiele róznych miejsc o wywołanie settera?
3. Czy pominięcie któregoś settra sprawia, że system będzie w stanie niespójnym, wywoła jakieś konsekwencje?
4. Czy za pomocą setterów można wprowadzić obiekt w dowolny (niespójny) stan?
5. Czy występują cykle: pobierz wartość - sprawdzć wartość - ustaw dane?

W legacy zachowania tego typu zazwyczaj odbywają sięw serwisach, nie w obiekcie dedykowanym

## Przywracanie enkapsulacji

1. Nowe metody dostępowe (mówiące explicite co robią, z intencją co robi np. )
    * jak biznes nazywa tę operację
    * czy nazwa ujawnia szczegóły implementacyjne 
    * czy nazwa nie sugeruje jednego konkretnego rozwiązania
    * jak nam nie idzie -> nie kmin za długo, wybierz coś - może nam to przyjdzie z czasem
2. Usuń możliwe gettery / settery
3. Wrzuć logikę i warunki do tych nowych metod dostępowych (pkt 1)

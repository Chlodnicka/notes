# Agregat


##  Jaki problem mamy - brak spójnej zmiany

1. Możliwość wprowadzenia systemu w dowolny stan
2. Możliwość ominięcia reguł
3. Wyciek wewnętrznej struktury obiektu na zewnątrz

Częste błędy jeśli zaczyna się od modelu bazy danych, rzeczowników.

1. Najłatwiej zapewnić spójnośc poprzez trzymanie reguł i danych w jednym miejscu za stablinym
interfejsem, który enkapsuluje reguły i dane
2. W ten sposób to tylko obiekt wie, jakie ma reguły i jakie ma pola
3. Pozwala to na jego lokalną refaktoryzację

 
# Mikrocykle w refaktoryzacji

1. Zbudowanie bezpieczeństwa, zabezpieczenie testem
2. Rozbicie obiektu
3. Podłączenie nowych obiektów do klientów
4. Migrowanie danych 

Kroki czasem mogą być wykonywane równolegle / są od siebie zależne / któreś są zależne


* _fail fast_

## Generalna ścieżka refaktoryzacji

1. Nazwij problem
2. Dobierz rozwiązanie
3. Zaplanuj zmiany -> [mały krok (możliwość odwrotu) -> wykonanie kroku -> obserwacja efektu] - mikrocykl

## Układanie planu refkatoryzajic

1. Czy krok jest kluczowy?
2. Czy jest zależność między krokami?
3. Czy muszęwykonać wszystkie kroki?

## Sztuczka z proxy

1. Jak nauczyć klienty korzystania z nowego obiektu przed jego fizycznym rozdzieleniem od starego (i przed zmianami w bazie danych)? Często to najbardziej czasochłonny i błędogenny proces ;(
2. Używamy wzroca _proxy_ -> robi to samo co stary, ale inne komponenty mogą zacząć gadać z nowym obiektem i powoli możemy zacząć te zachowania przepisywać 
np. jeden po drugim - możemy podłączyć cały system do tego _proxy_ to dowiemy się szybko o rzeczach, których nie przewidzieliśmy (po jakimś czasie proxy przestaje być proxy a staje się pełnoprawnym obiektem)
3. Róbmy rzeczy najtrudniejsze na początku 

## Przeglądanie stosu wywołań :) - _call hierarchy_ - Control + Option + H

1. Przeglądanie stosu wywołań pozwala poznać biznesowy kontekst uzżycia danego konceptu w systemie


# Working with Feedback

1. Dwie drogi wprowadzania zmian
    * _edit and pray_ - standard w branży
    * _cover and modify_ - test i zmiana, szybki feedback
2. Zbyt obszerne i długie _feedback loop_
3. _Software vise_
4. Testy regresji - zły pomysł robić to manualnie 
5. Unit testy to odpowiedź na większość naszych problemów - szybki feedback i wymuszenie podziału odpowiedzialności w kodzie
6. "Żeby zmienić kod, potrzebujemy testów. Żeby otestować kod, często musimy zmienić kod" - dylemat _legacy code_
7. Po zmianach w kodzie legacy kod sam w sobie może "wyglądać" gorzej - ale może zostać przetestowany i szybciej zrozumiany, co opłaci się w przyszłości
8. _Test harness_ - oprogramowanie umożliwiające testowanie jednostkowe
9. Algorytm:
    * identyfikacja punktów zmian
    * Odnalezienie kandydatów do testów
    * odplątanie zależności
    * napisanie testów 
    * wprowadzenie zmian i  refaktor
10. Małe zmiany nie sprawią, że kod nagle stanie się piękny. Sprawią, że stanie się łatwiej (a przez to szybciej) utrzymywalny
# Circuit Breaker

[https://martinfowler.com/bliki/CircuitBreaker.html](https://martinfowler.com/bliki/CircuitBreaker.html)

1. Wywołania do zewnętrznych zasobów, często po sieci, to standard, który może zawieść
   (usługa może nie odpowiadać, mieć błąd, może być zbyt obciążona itd)
2. Jeśli wielokrotnie uderzasz do niedziałającego serwisu, blokujesz swoje zasoby, problem się nawarstwia 
co może doprowadzić do skraszowania twojego systemu
3. _Circuit Breaker_:
    * _wrappuje_ wywołanie do zewnętrzego systemu, wywołuje ją samodzielnie i monitoruje jej stan
    * jeśli usługa nie odpowiada (definicja co to znaczy "nie odpowiada może być różna - 10 razy błąd? 10 razy timeout? 
   kombinacja tego? coś jeszcze innego") _circuit breaker_ blokuje kolejne wywołania do usługi, każda kolejna próba jest ucinana, 
   zanim wywołamy niedziałającą usługę
    * raczej dużo monitoringu (logów) dookoła _circuit breakera_ - to newralgiczny punkt, chcemy wiedzieć, co się tam dzieje i
   jakiś trigger pewnie na zmianę stanu - dobrze jest jak jednak IT wie, że coś nie działa
4. Najprostrze trzeba resetować ręcznie (jak bezpieczniki elektryczne), może być tam zaszyte zdecydowanie więcej logiki:
   * automatyczne otwieranie -> stan "pół otwarty" w którym po jakimś czasie w końcu przepuszczamy request "testowy" i jeśli ileś tam przejdzie
   to uznajemy, że zewnętrzny system wstał i znów możemy go np. odpytywać o zasoby
   * wiadomo -> nie wszystkie błędy powinny odcinać usługę - niektóre są standardowym flow biznesowym (np. zapytanie o nieistniejący produkt - 404 to wtedy całkiem spoko odpowiedź)
   * za zamykaniem i otwieraniem obwodu może stać całkiem sporo logiki - kiedy uznajemy, że zewnętrzny serwis przestaje/zaczyna działać


Implementacja w PHP:

[https://github.com/ackintosh/ganesha](https://github.com/ackintosh/ganesha)
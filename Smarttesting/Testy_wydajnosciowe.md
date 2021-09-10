# Testy wydajnościowe

1. Po co - "żeby nie muliło"
1. Jak mierzyć wydajność - z perspektywy użytkownika końcowego
1. Kiedy jest wydajnie? Kiedy nie ma frustracji z powodu korzystania z rozwiązania
1. Jak mierzyć wydajność
    * dostępność - procent działania systemu w stosunku do czasu całkowitego
    * czas odpowiedzi
    * przepustowość - współczynnik interakcji np. liczba wejść / użyć
    * eksploatacja - procent użycia danego zasobu (sieci, pamięci, cpu)
1. Ilu użytkowników w ogóle? Ilu użytkowników jednocześnie? Jak i skąd będą się łączyć? Jak aplikacja będzie wgrywana,
   na ile serwerów? Jak aplikacja wpłynie na wysycanie łącza?
    * niedocenianie popularności usługi (USOS przy zapisie na cokolwiek xD)
1. Najlepiej idealna kopia produkcji, ale niezbyt łatwe - może stag
   (10 serwerów na produkcji to 10 serwerów na stagu, ta sama konfiguracja sieci, te same parametry uruchomieniowe, taki
   sam rozmiar w bazach itd.) - może wirtualizacja?
1. Kolejne problemy: nierównomierny rozkład żądań, load balancing może kierować żądania z tego samego ip na tę samą
   maszynę
1. Zaślepienie zewnętrznych usług - ale trzeba uwzględnić opóźnienie sieciowe
1. Aplikacja musi być stabilna
1. Wybieramy najczęściej realizowane czynności które są krytyczne z punktu widzenia użytkownika
1. Najpierw testujemy na mniejszej grupie, potem na większej
1. Wydajnościowych nie powinniśmy testować w izolacji - czasem trzeba zasymulować szum, np wysoką inteerakcję z bazą
   danych
1. Który rodzaj testu wybrać?
    * test punktu odniesienia (baseline test) - dla pojedynczego użytkownika - wyznacza pewne referencyjne wynika
    * testy obciążenia (load test) - test wydajności do wyznaczonego poziomu (np 100000 użytkowników) w stosunku do
      pojedynczego użycia
    * próba obciążeniowa (stress test) - celem jest określenie limitu systemu, test będzie działał tak długo, aż
      aplikacja się zepsuje, tj. np. przestanie odpowiadać
    * testy stabilności (soak lub stability) - wykrywają np. wycieki pamięci
    * próba dymna (smoke test) - tylko części systemu, które sięzmieniły
1. Rodzaje wkładu użytkowników: big bang - wszyscy na raz, ramp up - zaczynamy od określonej liczby która rośnie, ramp
   up z krokiem, ramp up / down
1. Analiza wyników - statystyka się kłania - średnia i mediana, odchylenie standardowe, rozkład normalny, nty precentyl,
   rozkład czasu odpowiedzi
1. _Coordinated ommision_ - nie mierzymy czasu odpowiedzi ale czas procesowania po stronie usługi, może wypaczyć wynik
   testu
    * wysyłanie żądań w sposób ciągły
    * wrk2
1. Narzędznia do monitoringu: honest profiler, micrometer
1. Jak rzetelnie uruchomić testy wydajnościowe danego fragmentu aplikacji - microbenchmark
   * cykl: projektowanie - opis celu, implementacja microbenchmarku, uruchomienie, analiza, ulepszenie 
1. Narzędzia testów wydajnosciowe: 
   * apache jmeter,gatling, vegeta, netlink, locust, k6
1. Bechmarki: jmh, benchmark .net
1. alternatywa - apm, monitoring produkcji
# Coupling i kohezja

1. Luźny _coupling_ i silna kohezja
1. _Coupling_ - jak bardzo klasy zależą od siebie na wzajem
1. Rodzaje _couplingu_ (wg Mayersa, jeszcze w czasach paradygmatu proceduralnego!)
   * _content coupling_ - klasa zmienia bezpośrednio zawartość drugiej
   * _common coupling_ - klasy zmieniają jakiś globalny/współdzielony stan
   * _external coupling_ - zależność od zewnętrznych narzędzi (czasem nie do przeskoczenia)
   * _control coupling_ - klasa wywołująca metodę ma wpływ na to, co klasa wywoływana zwraca (np. za pomocą dodatkowych
     flag), metoda wywoływana nie jest "czarną skrzynką"
   * _stamp coupling_ - klasy komunikują się za pomocą wewnętrznej struktury danych (DTOsy)
   * _data coupling_ - ogromne klasy typu _Product data_ z niebotyczną ilością danych w środku, służy jako śmietnik
     wszystkiego bez recyklingu - po co przesyłać całą, skoro metoda/klasa może potrzebować tylko kilku parametrów
1. _Decoupling_ - technika/metoda (jakakolwiek), dzięki którym rozluźniamy zależności między klasami
1. Słaby coupling - po interfejsach, silny - po implementacjach
1. Kohezja - "spójność" klasy, "powiązanie funkcjonalne - _functional relatedness_", "klejenie się" klasy
   * co powoduje, że dane elementy zgrupowane są w jedną klasę? jakimi kryteriami grupowania się kierujemy?
1. Rodzaje kohezji:
   * _coincidental_ - brak kryterium podziału, jest bo jest, ma 3000 lini, to dołożę 20, nic się nie stanie - brak
     jakiegokolwiek designu
   * _logical_ - elementy spaja to, że rozwiązują te samę klasę problemów (np. liczą jakąś funkcję matematyczną)
   * _temporal_ - elementy klasy spaja, czas, w którym są wywoływane (klasy inicjalizujące itp) - z tym ciężko walczyć
   * _procedural_ - koncentracja na algorytmie wykonania (przepływie kontroli), nie na domenie problemu, elementy są
     związane kolejnością występowania i czasem, charakterystyczne występowanie wielu pętli, warunków
   * _communicational_ - klasy operują na tych samych danych wejściowych / wyjściowych (np. repozytorium `get` zwraca
     obiekt tego samego typu, co `save` przyjmuje w inpucie)
   * _sequential_ - sekwencja przetwarzanych danych - np. dane wyjściowe jednego elementu to dane wejściowe kolejnego
     itd.
   * _functional_ - elementy w klasie są tak dobrane, by możliwie najlepiej realizować konkretne, pojedyncze zadanie,
     każdy element stanowi integralną i potrzebną do wykonania zadania część klasy
1. *Wagi kohezji (czyli ograniaj z ostrożnością, nie wszystko musi dążyć do kohezji funkcjonalnej, przerost formy nad
   treścią):
   0: coincidental, 1: logical, 3: temporal, 5: procedural, 7: communicational, 9: sequential, 10: functional.
1. Odpowiedź na pytanie (szczerze) - co robi ta klasa? pozwala zidentyfikować lub choćby zarysować typ kohezji

źródło:
https://devstyle.pl/2020/02/24/szesc-twarzy-couplingu/?utm_source=convertkit&utm_medium=email&utm_campaign=%5BDNA%5D+Dlaczego+Tw%C3%B3j+system+GNIJE%3F+%F0%9F%91%80+Trzy+rewelacyjne+teksty+na+weekend%21%20-%203245306
https://devstyle.pl/2020/03/09/o-kohezji-slow-kilka/?utm_source=convertkit&utm_medium=email&utm_campaign=%5BDNA%5D+Dlaczego+Tw%C3%B3j+system+GNIJE%3F+%F0%9F%91%80+Trzy+rewelacyjne+teksty+na+weekend%21%20-%203245306

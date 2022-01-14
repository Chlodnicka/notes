# Serwis domenowy

[https://podcasts.apple.com/pl/podcast/29-domain-driven-design-essentials-domain-service/id1508298430?i=1000547486946
](https://podcasts.apple.com/pl/podcast/29-domain-driven-design-essentials-domain-service/id1508298430?i=1000547486946)

1. Enkapsuluje logikę domenową a nie pasuje do tego co już mamy w autonomicznych 
wysepkach (agregaty i value objecty) i komunikuje je między sobą (np. agregaty)
2. Ta logika nie pasuje do encji (bo nie jest identyfikowalna), trochę koordynuje pracę agragatów między sobą
3. W idealnym świecie to jest jednak sewis DOMENOWY, 
więc powinien dostać dane wejściowe (agregaty, encje, value objecty) i wypluć dane na output, 
tak, żeby było łatwo go testować w izolacji, testem jednostkowym, raczej nie opuszcza się wątku, pamięci -> to jest funkcja, algorytm ;) 
4. Nie mylić z serwisem aplikacyjnym, który koordynuje moduły na innym poziomie - może sięgać do repo, do innych systemów, zapisać finalnie agregaty do repo
5. Serwis domenowy trochę "nie istnieje" w świecie rzeczywistym. Można go najbliżej porównać do osoby, która weryfikuje wniosek i przekłada papiery xD
6. [GRASP a SOLID](./../5_GRASP_SOLID.md)
7. Serwis domenowy powstaje przez dyskomfort - jak masz dwa agregaty i nowa funkcjonalność działa na obydwu 
i nie pasuje połączenie ich ani wrzucenie tej nowej logiki tylko do jednego bo wprowadzi [coupling](./../2_Coupling_kohezja.md) lub zaciemni kod - to może jest miejsce na serwis domenowy
8. "Dobra zasada zawsze jest dobra dopóki nie znajdziesz lepszej"
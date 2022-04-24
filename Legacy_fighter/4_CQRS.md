# CQRS

## Problem budownaia złożonych odczytów za pomocą encji

1. Mierz co to znaczy "powoli/wolno" - gdzie mierzyć, kiedy mierzyć, jak mierzyć? Czy to na konkretnym zasobie? Czy to o konkretnej godzinie?
2. Wąskie gardła: systemy memory-bound lub CPU-bound lub I/O-bound - profilowanie aplikacji
3. _Lazy loading_ przy ORMach mogą generować bardzo wiele requestów do bazy danych, więcej zużycia sieci, pamięci i procesora, niejawne zapytania do bazy - czasem zmiana _lazy_ na _eager_ jest ok - czasem nie bo załadujemy połowę bazy
4. Często trzeba rozdzielić zapis (model decyzyjny - agregat) od odczytu - może czysty SQL i ładujemy tylko te dane, których rzeczywiście potrzebujemy w mniejszej ilości zapytań 
5. DTO (_data transfer object_) - służą do transferu danych 

### DTO

1. CRUD ;)
2. DTO to kontrakt ale sposób ich utworzenia jest szczegółem implementacyjnym - DTO per encja może popwodować problem
3. DTO to kontrakt - można je tworzyć w dowolny sposób - nie tylko na podstawie encji
4. Geneza - modelowanie przez ekran użytkownika, modelowanie relacją zawierania, zaczynamy tworzyć obiekty będące workami na dane przemieszane z agregatami

* Czasem piszemy test, który sprawdza czy dane zwracane na dwa różne sposoby są takie same 
* Testy charakterystyki - wywołujemy kod, sprawdzamy co zwraca i ustawiamy to jako oczekiwany output

### Greenfield w brownfieldzie

1. Nazwanie "co to robi"?
2. Jak to zrobić inaczej?
3. Implementacja innego "JAK"
4. Podpięcie

* Jest łatwiej, gdzy zmianą jest query (i nie ma żadnych efektów ubocznych) i gdy klientów kodu jest mało


1. Czy dokonaliśmy poprawnych pomiarów?
2. Czy jest ORM i czy mamy dużo lazy lodaingu?
3. Ile wynosi N w potencjalnym problemie N+1
4. Czy dane są przyklejane do obiektów na zasadzie relacji zaweirania ze świata rzeczywistego?

### Kasowanie N+1

1. Na jakie pytanie odpowiadamy? Generujemy raport np.
2. Testy (charakterystyki)
3. Implementacja nowej odpowiedzi i ewentualne połaczenie ze starą
4. Podmienianie

* Niektóre dane w obiektach staną się niepotrzebne. Dzięki usunięciu zyskujemy czytelność

## Parallel Models - modele równoległe 

1. W złożonym systemie, który przechodzi refaktoryzację oraz jednocześnie jest rozwijany, utrzymanie dwóch równoległych modeli
to często jedyna bezpieczna droga
2. Zalety: bezpieczeństwo,, możliwość odwrotu do starego modelu, dowolność nowego modelu, testowalność nowego modelu poprzez porównianie ze starym, stopniowe wdrażanie
3. Wady: rozwijanie obu modeli, jeśli trwa długo, więcej kodu, migracja danych (efekt brzydkiego kaczątka - przez pewien czas stan obecny wygląda gorzej niż poprzednio "noc jest najciemniejsza przed świtem"), trudność połączneia
4. Czasem dobrze jest użyć Proxy (stary kod, już podłączony, wywołuje nowy kod) - a czasem jest problem nawet z tym, bo brakuje enkapsulacji, model jest rozmyty
5. Usuwalność kodu jest ważnym driverem architektonicznym - chowaj szczegóły implemntacyjne za klarownym api, jeśli implementacja jest brzydka to trudno, ale jeśli jest ukryta za stabilnym interfejsem to lepiej niż piękne, ale wymieszane koncepty
6. Feature flagi do starej/nowej implementacji ;) I można nagle włączać nowy model per klient, mamy testy A/B, dzien/noc, wnioskowanie na podstawie ostatniego wywołania
7. Test to weryfikacja naszych założeń - często założeniem jest: ma działać jak działało do tej pory - wtedy weryfikacją założeń (testem) jest porównanie wyników nowego i starego modelu
    * to nie jest technika zastępująca tylko dodatkowa - możliwość odpytania obydwu modeli i porównania wyników (_reconciliation_) - wywołuj stary, w tle nowy i porównujesz (na prodzie) 
    * poprawiaj
    * jak nie ma błędów przepinasz na nowy i w tle porównujesz ze starym
    * jak są błędy jednak - przepinasz feautre flagę na stare 
    * poprawiasz  "na spokojnie"
    * i od początku
8. Opór: odpytywanie dwóch modeli jest wolniejsze - tak, jest wolniejsze - ale różnica jest zazwyczaj znikoma (kilkaset milisekund do kilkunastu sekund),
można też odpytać asynchronicznie - a zapewniamy poprawność i ciągłość działania systemu, nie będzie _big bang_

# Sterowanie czasem

1. Rzeczy stają się możliwe po upływie określonego czasu, rzeczy wygasają po danym momencie w czasie 
2. Czas często wpływa na reguły: domenowe (oddać towar można do 14 dni od zakupu), procesowe (po 5 dniach wysyłamy maila z prośbą o ocenę), koordynacyjne (info o poniedziałkowych dostawach trzeba wysłać do starego systemu), zmienna w obliczeniach
3. Parametr czasu zmienia wynik równania - często trzeba się pozbyć wywołań typu NOW() - tylko sparametryzować metodę lub wprowadzić zależność do "dostawcy" czasu
4. Jak wchodzi baza danych to sytuacja jest trudniejsza - można spróbować zaślepić dane albo przenieść ustawianie czasu na wyższą warstwę
5. Schedulery - ustawia wartość na podstawie jakiegoś czasu (crony) - cięzko testowalne - czasem można się tego pozbyć 
6. timestamp to nie to samo co data, persystowwanie dat w bazie jest problematyczne (UTC ;)), zegar systemowy może oscylować (jak wymagamy dużej precyzji to może byc to problem), czas letni/zimowy (o boziu, flashbacki z wietnamu)
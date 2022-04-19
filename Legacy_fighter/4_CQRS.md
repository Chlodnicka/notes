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

## Parallel Models
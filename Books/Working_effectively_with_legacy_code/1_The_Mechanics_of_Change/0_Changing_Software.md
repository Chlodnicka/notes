# Changing Software

1. Dlaczego zmieniamy kod?
    * dodajemy feature, naprawiamy błąd, poprawiamy design, optymalizujemy
2. Co może się zmienić po zmianie kodu?
   * struktura kodu, funkcjonalność (nowa lub istniejąca) lub użycie zasobów
3. Przy jakiejkolwiek zmianie, w większości celem też jest zachowanie już istniejącej funkcjonalności - 
a to wcale nie takie oczywiste. W większości przypadków, nawet nie wiemy, ile istniejącego zachowania narażamy na zmianę. 
4. Należy zadać sobie trzy pytania:
   * Jakie zmiany chcemy zrobić?
   * Jak będziemy wiedzieć, że zrobiliśmy je poprawnie?
   * Jak dowiemy się, że nic nie zepsuliśmy po drodze?
5. Unikanie zmian i udawanie, że nie są potrzebne prowadzi tylko do kłopotów i kodu coraz cięższego w utrzymaniu
6. Wieczny refaktor małych części w zależności od dodawanej funkcjonalności
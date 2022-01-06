# PHP Storm

## Temat i cel

Jak zacząć sprawniej korzystać z PHP Storma czyli szybciej pisać i testować kod

## Główne rzeczy

1. Nawigacja i poruszanie się po:
    * IDE
    * projekcie
    * kodzie
2. Refaktor i generowanie kodu - co można zrobić automatycznie
3. Baza danych
    * konfiguracja (wielu baz danych w jednym projekcie)
    * pokazanie konsoli,
    * uruchamianie SQLi bezpośrednio z kodu
4. Klient HTTP
    * scratch file .http i proste POSTy, GETy, historia responsów, że można porównać
    * jak wrzucić w to .env i skrypty
    * test requestu pobranego z przeglądarki (eksportuj CURLa)
    * eksport bezpośrednio z openapi.yaml
5. Podpięcie Dockerów, konfiguracja interpreterów, debugowanie, testowanie (?)
6. Git (?)

## Brain dump

1. ulubiony skrót klawiszowy: zamyka wszystkie otwarte okna poza kodem, ponowne przyciśnięcie otwiera poprzednią
   konfigurację, zajebista sprawa
2. kwestia preferencji, ja usunęłam pasek z listą otwartych plików, cięzko mi się po niej poruszać, polecam cmd+e, poza
   plikami pokazuje też ostatio otwarte lokacje (okna np. listę plików projektu)
3. popularne lokacje (okna) mają przypisane skróty klawiszowe (jak cmd + 1 -> lista plików projektu) -> warto zapamiętać
   najpopularniejsze (lista plików, terminal...)
4. podwójny shift - kolejny bóg - otwiera wyszukiwarkę wszystkiego (tekstów w plikach, nazw klas /plików, akcji!) ->
   bardzo przytadtne jak się nie pamięta skrótów klawiszowych ale wiesz, co chesz zrobić. Ja zapominam notorycznie jak
   się unwrapuje. Zamiast klikać myszką polecam tę strategię, w końcu się zapamięta
5. ustawienie ścieżek i namespace'ów w projekcie - czasem łapie sam, czasem trzeba robić to ręcznie
6. Scratch file - jak zrobić, do czego mogą słuzyć
7. poruszanie się po kodzie ->
    * skok do implementacji,
    * skok do implementacji interfejsu,
    * skoki kolejna / poprzednia metoda,
    * na koniec / początek pliku
8. Surrounding i unwrapping
9. Zaznaczanie - sposoby (w szczególności option + strzałka w górę)
10. Postfix (autouzupełnienie wsteczne), autouzupełnienia
11. Refaktor -> control + T -> wyświetla się okno dialogowe i używamy albo numerów albo zapamiętujemy skróty klawiszowe
    standardowych refaktoryzacji - pokazać co można?
12. Inspections -> inspektor po prawej (ma być na zielono)
    * option + enter -> pokazuje co to jest za błąd
    * enter / select -> enter -> robi automatyczną poprawkę
13. Generowanie kodu
    * konstruktory, gettery / settery, implementacje metod, implementacji pól (option + enter)
    * generowanie klas testów
    * live templates
    * szablony plików
14. Skonfigurowanie bazy danych w projekcie -> (jednej lub wielu)
15. Konsola bazy danych - jak odpalić i korzystać
16. Uruchamianie SQLi bezpośrednio z kodu, nie trzeba nic przeklejać
17. Zaprezentowanie możliwości wbudowanego klienta HTTP (scratch file .http, prosty POST / GET, historia requestów,
    porównywanie)
18. Dorzucenie .enva, zmiennych, skryptów do klienta HTTP, asercje, można normalnie pliki z tego stworzyć, wrzucić w
    repo, stworzyć bardzo prostą suitę testów, załączyć do repo -> mamy najniższym kosztem wygenerowane jakieś testy
    end-to-end
19. Konwertowanie requestu bezpośrednio z przeglądarki i z openapi.yaml

## Dodatkowo
1. Udostępnić _cheetsheet_
2. Skróty klawiszowe ze zrzutów ekranu ponad paskiem play xD

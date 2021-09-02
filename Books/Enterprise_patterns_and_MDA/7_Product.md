# Product

1. Produkty unikalne, identyczne i _identifiable things_ - jak edycja limitowana np.
1. Produkt sprzedawany w ilości (np. prąd, woda)
1. _Product type_ vs _Product instance_
   * _Product type_ - co masz w specyfikacji, co reklamujesz, sprzedajesz, co klient przegląda / zamawia
   * _Product instance_ - co wytwarzasz, co trzymasz w magazynie, co dostarczasz, co klient dostaje
1. _Product identifier_ - do jednoznacznej identyfikacji _Product type_ id w bazie wewnątrz systemu, 
   EAN/UPC -> GTIN - do indentyfikacji z zwnętrznymi dostawcami, ISBN, ISSN   
1. _SerialNumber_ - do jednoznacznej identyfikacji _Product instance_
   * _Batch_
1. _Product specification_: _Product feature type_ i _Product feature instance_
1. _Package type_
1. _Product catalog_ - zbiór _Product types_, zapisanych jako _Catalog entry_ - kategorie, tagi -
   w większości przypadków przekładalne na siebie jeden do jeden (ale nie zawsze).
   Przykład aspiryna 16 tabletek - przy _product type_ ważny jest też np. producent.
   Kupujący często nie dba, o to od jakiego sprzedawcy kupi produkt, byle by cena/czas dostawy 
   mu się spinały (_catalog entry_). To sprzedawcy bardziej zależy, żeby zeszło to od konkretnego
   producenta/sprzedawcy (_product type_)
   * _This can be true for many different types of products. What you advertise for sale can be a more generalized description of what you hold in stock._
1. _Package_ - zbiór produktów jako jedna jednostka, (kompy poskładane, samochód z ubezpieczeniem itp)
   * _Package Type_ - zbiór _Product Type_, rodzaj _Product Type_, może zawierać zasady, w jaki sposób można łączyć produkty
   * _Package Instance_ - zbiór _Product Instance_, rodzaj _Product Instance_
   * możliwości łączenia trzeba ograniczać (wymaganiami klienta, regułami biznesowymi, prawnymi, sensownością itp) politykami jak i z czym
   produkty mogą się łączyć, żeby ilość możliwych kombinacji nie poszła nam silniowo w górę
   * Rozwiązanie: _Package specification process_: predefiniowane _Packages_ oferowane klientowi albo możliwość skonstruowania 
     własnej przez klienta na podstawie określonych przez biznes reguł (www.businessarchetypes.com) 
   * _Rule_ (rozdział 12)!
   * _Propositions of inclusion_ - _In our rules-based model, PackageTypes contain a number of PropositionsOfInclusion. These are statements of truth that define constraints about how ProductTypes in a PackageType may be combined to form PackageInstances._
   * _Conditional proposition of inclusion_ - ... (7.18 - 7.19)
1. _Product relationships_ - bardziej stabilne relacje między _Product types_ mogą być modelowane w ten sposób
   * _upgradableTo_, _substitutetBy_, _replacedBy_, _complementedBy_, _compatibleWith_, _incompatibleWith_ - 
1. _up-selling_ -> _upgradableTo_, _cross-selling_ -> produkt, który chesz kupić często idzie w parze z innymi, które
   w danej konfiguracji można kupić w niższej cenie
1. _Price_:
   * _Product type_ może mieć wiele różnych cen (np. od wielu różnych sprzedawców/dostawców)
   * _Price_ ma powiązany _Rule set_, który określa warunki jej dostępności (jeśli chcesz price x, musisz spełnić warunek y)
   * _Prices_ mogą mieć opcjonalną ważność (_validFrom_, _validTo_), które mogą zostać użyte przez _Rule set_ do decyzji,
     czy dana cena jest dostępna i może zostać użyta do stworzenia historii cen _Product Type_
   * _Product instance_ ma przypisaną _agreed Price_ ze zbioru _possible Prices_ dla _Prdocut type_ lub _applied Arbitrary Price*_
   * . 7.22.1
   * . ....
1. ..
1. ..
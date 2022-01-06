# Feature toggles (feature flags)

Source: https://martinfowler.com/articles/feature-toggles.html

## O co chodzi

1. Wzorzec pomaga dostarczać cząstki oprogramowania szybko, ale stosunkowo bezpiecznie
2. W kodzie wrzucamy _toggle point_, w którym rozchodzą się ścieżki tego "jak coś robimy"
```
  function reticulateSplines(){
    var useNewAlgorithm = false;
    // useNewAlgorithm = true; // UNCOMMENT IF YOU ARE WORKING ON THE NEW SR ALGORITHM
  
    if( useNewAlgorithm ){
      return enhancedSplineReticulation();
    }else{
      return oldFashionedSplineReticulation();
    }
  }
  
  function oldFashionedSplineReticulation(){
    // current implementation lives here
  }
  
  function enhancedSplineReticulation(){
    // TODO: implement better SR algorithm
  }

```
3. Flagi mogą być dynamiczne, np. przechowywane w bazie/env/pliku/itd.
4. Możemy używać _toggle routerów_ do dynamicznego ustawiania, której wersji używać i dzięki temu z łatwością odpalać 
testy na wszystkich rozgałęzieniach, wdrażać bezpiecznie nowe feature'y na produkcję z możliwością natychmiastowej 
zmiany _toggle configuration_, tak by wrócić do poprzedniej wersji (np. przez env, dane w bazie danych, flagę ustawialną przez administratora w UI, algorytm na podstwie np. ip/lokalizacji requestu, przekazanego ciostka itp.)
5. _Canary releasing_ - wypuszczanie wersji tylko dla części użytkowników, na podstawie jakichś warunków (_toggle router_)
   * można nauczyć _toggle router_ konceptu kohort użytkowników np. procentowo wyznaczając część użytkowników, 
   którym pokażemy nową wersję (np. randomowo wybierając ich po % z id) i porównujemy staty wizyty z całą resztą
6. Dzięki temu można łatwo przeprowadzać testy A/B 

## Kategorie

1. Główna zaleta - możliwość dostarczania alternatywnych ścieżek w kodzie w obrębie jednego deploy'u i możliwość wyboru między nimi w _runtime_
2. Różne rodzaje można podzielić ze względu na dwa główne czynniki: jak długo _feature toggle_ będzie żył i jak bardzo dynamiczne będzie to, jak się będzie zmieniać. 
Poza tym pod uwagę też trzeba wziąć to, kto się będzie zajmował tym _feature togge_ itp.

### _Release toggles_

1. pozwalają na wrzucenie do wspólnego brancha (np. developa) kodu funkcjonalności jeszcze nie gotowej na odpalenie na produkcji
co nie przeszkadza w tym, że branch może być wdrażany w każdym momencie. Nowy kod może finalnie nigdy nie zostać odpalony przez użytkownika końcowego
2. _separating feature release from code deployment_
3. tego typu _feature toggle_ są chwilowe z natury - albo w końcu odpalamy nasz niegotowy wcześniej kod, albo z niego rezygnujemy. 
4. Zazwyczaj czas ich życia to 1-2, maks kilka tygodni. Raczej warunki czy włączyć czy nie nie zmieniają się często. 

### _Experiment toggles_

1. Służą zazwyczaj do przeprowadzania testów na użytkownikach. _Toggle router_ decyduje, którą wersję kodu odpalić w danym momencie,
dane na temat zachowań użytkowników, sprzedaży itd są zbierane, analizowane, porównywane i w końcu ktoś podejmuje jakąś decyzję biznesową co z tym zrobić.
Często używane do optymalizacji procesów typu zakupy na stronie (który algorytm cenowy jest korzystniejszy pod jakimiś względami, czy jaki napis na przycisku do kupienia jest częściej klikalny)
2. Żyją na tyle długo, by móc zebrać znaczące dane na podstawie których można podjąć decyzje - w zależności od sytuacji mogą to być i godziny i tygodnie.
3. Warunki _toggle routera_ lubią się zmieniać dosyć często

### _Ops toggles_

1. 
# Feature toggles (feature flags)

Source: https://martinfowler.com/articles/feature-toggles.html

1. W kodzie wrzucamy _toggle point_, w którym rozchodzą się ścieżki tego "jak coś robimy"
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
2. Flagi mogą być dynamiczne, np. przechowywane w bazie/env/pliku/itd.
3. Możemy używać _toggle routerów_ do weryfikowania, której wersji używać i dzięki temu z łatwością odpalać testy na wszystkich rozgałęzieniach
4. _Canary releasing_ - puszczaniepuszczanie wersji tylko dla części użytkowników 
    * trzeba nauczyć _toggle router_ konceptu kohort użytkowników np. procentowo wyznaczając część użytkowników, którym pokażemy nową wersję (np. randomowo wybierając ich po % z id) i porównujemy staty wizyty z całą resztą
5. A/B testy
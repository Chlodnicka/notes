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
   zmiany _toggle configuration_, tak by wrócić do poprzedniej wersji (np. przez env, dane w bazie danych, flagę
   ustawialną przez administratora w UI, algorytm na podstwie np. ip/lokalizacji requestu, przekazanego ciostka itp.)
5. _Canary releasing_ - wypuszczanie wersji tylko dla części użytkowników, na podstawie jakichś warunków (_toggle
   router_)
    * można nauczyć _toggle router_ konceptu kohort użytkowników np. procentowo wyznaczając część użytkowników, którym
      pokażemy nową wersję (np. randomowo wybierając ich po % z id) i porównujemy staty wizyty z całą resztą
6. Dzięki temu można łatwo przeprowadzać testy A/B

## Kategorie

1. Główna zaleta - możliwość dostarczania alternatywnych ścieżek w kodzie w obrębie jednego deploy'u i możliwość wyboru
   między nimi w _runtime_
2. Różne rodzaje można podzielić ze względu na dwa główne czynniki: jak długo _feature toggle_ będzie żył i jak bardzo
   dynamiczne będzie to, jak się będzie zmieniać. Poza tym pod uwagę też trzeba wziąć to, kto się będzie zajmował tym _
   feature togge_ itp.

### _Release toggles_

1. pozwalają na wrzucenie do wspólnego brancha (np. developa) kodu funkcjonalności jeszcze nie gotowej na odpalenie na
   produkcji co nie przeszkadza w tym, że branch może być wdrażany w każdym momencie. Nowy kod może finalnie nigdy nie
   zostać odpalony przez użytkownika końcowego
2. _separating feature release from code deployment_
3. tego typu _feature toggle_ są chwilowe z natury - albo w końcu odpalamy nasz niegotowy wcześniej kod, albo z niego
   rezygnujemy.
4. Zazwyczaj czas ich życia to 1-2, maks kilka tygodni. Raczej warunki czy włączyć czy nie nie zmieniają się często.

### _Experiment toggles_

1. Służą zazwyczaj do przeprowadzania testów na użytkownikach. _Toggle router_ decyduje, którą wersję kodu odpalić w
   danym momencie, dane na temat zachowań użytkowników, sprzedaży itd są zbierane, analizowane, porównywane i w końcu
   ktoś podejmuje jakąś decyzję biznesową co z tym zrobić. Często używane do optymalizacji procesów typu zakupy na
   stronie (który algorytm cenowy jest korzystniejszy pod jakimiś względami, czy jaki napis na przycisku do kupienia
   jest częściej klikalny)
2. Żyją na tyle długo, by móc zebrać znaczące dane na podstawie których można podjąć decyzje - w zależności od sytuacji
   mogą to być i godziny i tygodnie.
3. Warunki _toggle routera_ lubią się zmieniać dosyć często

### _Ops toggles_

1. Służą do kontrolowania tego jak zachowuje się system np. przy wdrożeniu nowej funkcjonalności, której nie jesteśmy
   pewni ->
   _ops toggle_ może służyć do szybkiego wyłączenia / włączenia jeśli coś pójdzie nie tak.
2. Zazwyczaj żyją krótko - dopóki nie zyskamy pewności, że wszystko działa tak jak chcemy
3. Zdarzają się przypadki tzw. "kill switches", które mogą służyć do wyłączenia nie niezbędnych funkcjonalności systemu
   w przypadku dużego obciążenia. Trochę jak manulanie sterowany _[circut breaker](4_Circut_breaker.md)_
4. Ze względu na to w jakich celach są używane, muszą być konfigurowalne bardzo szybko (raczej flaga w bazie, env czy
   UI) niż nowy release

### _Permissioning toggles_

1. Zmieniają sposób działania naszego systemu dla konkretnych użytkowników (_free_ vs _premium_, _alpha_, _beta_, _
   champegne brunch*_)
    * _champagne brunch_ - podobne do _canary release_, z tą różnicą że przy _cr_ funkcjonalność odsłaniamy randomowo (1
      procent jakichkolwiek użytkoników), _cb_ - dla konkretnych, wybranych
2. Mogą żyć w nieskończoność (np. _premium_ a _free_), albo krótko (_alpha_, itd.), zazwyczaj dynamicznie się
   zmieniają (per request)

### Statyczne a dynamiczne

1. _Toggle_, wewnątrz których decyzje podejmujemy w runtime na podstawie danych per request mają zazwyczaj o wiele
   bardziej skomplikowane warunki
2. Dla _release toggle_ to zwykle prosty _on/off switch_ zmieniany w _toggle point_ wraz z wdrożeniem
3. Z kolei dla _experiment toggle_ podejmowanie decyzji, z jakiego kodu skorzystać może zawierać skomplikowany algorytm
   z wieloma regułami

### Tymczasowe a długotrwałe

1. Tymczasowe: _release_, _experiment_
2. Długotrwałe: _ops_, _permission_
3. Trzeba pamiętać, że to nie jest sztywny podział (jak rzadko co), to bardziej rozkład normalny, niż kod binarny

Te wszystkie aspekty trzeba wziąć pod uwagę implementując _feature flag_ ->
w zależności od tego jak długo będziemy z niego korzystać i jak bardzo dynamiczny będzie, lepiej będzie zastosować takie
a nie inne rozwiąznaie techniczne. Dobierzemy je nieadekwatnie i będzie płacz.

Np. dla algorytmu po refaktorze, który ma działać tak samo jak aktualny, tylko szybciej i być lepiej napisany
zwykły `if/else` jest całkowicie akceptowalny

- jak tylko refaktor się powiedzie, pozbywamy się starego kodu i _toggling point_. W przypadku _permission
  toggle_ `if/else` to może nie najlepszy pomysł -
- potrzebujemy raczej czegoś łatwiej konfigurowalnego i utrzymywalnego

## Implementacja

_Feature flags_ mają to do siebie, że lubi się wokół nich robić bałagan w kodzie - trzeba tego pilnować

### Odplątywanie _decision points_ od _decision logic_

1. Częsty błąd to mieszanie logiki _toggle pointu_ z _toggle routerem_

```js
 const features = fetchFeatureTogglesFromSomewhere();

function generateInvoiceEmail() {
    const baseEmail = buildEmailForInvoice(this.invoice);
    if (features.isEnabled("next-gen-ecomm")) {
        return addOrderCancellationContentToEmail(baseEmail);
    } else {
        return baseEmail;
    }
}
```

Niby wszystko jest ok, ale co jeżeli założenia dotyczące tego, czy zmieniać template maila się zmienią, skomplikują, będzie ich wiele zależnych od różnych warunków - a lubią w tego
typu miejscach. Można to rozdzielić wprowadzając [warstwę pośrednią](https://en.wikipedia.org/wiki/Fundamental_theorem_of_software_engineering).

```js
function createFeatureDecisions(features) {
    return {
        includeOrderCancellationInEmail() {
            return features.isEnabled("next-gen-ecomm");
        }
        // ... additional decision functions also live here ...
    };
}

const features = fetchFeatureTogglesFromSomewhere();
const featureDecisions = createFeatureDecisions(features);

function generateInvoiceEmail() {
    const baseEmail = buildEmailForInvoice(this.invoice);
    if (featureDecisions.includeOrderCancellationInEmail()) {
        return addOrderCancellationContentToEmail(baseEmail);
    } else {
        return baseEmail;
    }
}
```

Dodatkowy obiekt `FeatureDecisions` działa jako zbiór wszystkich reguł - jeśli one się zmienią, modyfikujemy tylko to jedno miejsce. 
A nasz mechanizm wysyłający maile nawet nie wie, jak ta decyzja została podjęta.

### _Inversion og decision_

...

### _Avoiding conditionals_


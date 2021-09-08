# Podstawy

## Bezpieczeństwo typów

* Pozwala nam zapewnić, że aplikacja się nie położy
* Inwestycja - dla innych typy mogą być podpowiedzią, o co chodzi
* Wyższy próg wejścia
* Nie wyłapie wszystkiego
* Type-checkery w JS: Typescript, Hegel, Purescript, Flow
    * Typescript jest najpowszechniej używany i jest duże wsparcie społeczności

* Ważniejsze niż sama technologia jest to jak się jej używa

## Zalety

* Type checker sprawdza nasz kod - kompilator sprawdza nasze błędy
* Odnajdujemy błędy wcześniej - w trakcie developmentu, nie w runtime
* Redukcja odpowiedzialności za błędy w kodzie
* Dzięki temu możemy odpuścić pisanie części testów
* Typy mogą wyrażać intencje programisty i podpowiadać innym
* Łatwiejsze refaktory

## Ograniczenia

* Typescript nie umie sprawdzić co jest w odpowiedzi z REST API - bo to jest robione dopiero w runtime
* Warunki wyścigu
* Niektóre operacja JS jak koercja `{} + ''`, `100/0 -> infinity`
* Typescript nie respektuje semver
* Typescript trzeba w miarę regularnie podnosić - zmiany między wersjami potrafią być inwazyjne

## Dodatkowo

* Playground: https://www.typescriptlang.org/play

    

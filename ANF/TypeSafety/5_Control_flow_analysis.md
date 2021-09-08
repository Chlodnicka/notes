# Control flow analysis - kontrola przepływu w aplikacji

* jakie ścieżki przejścia mamy w aplikacji
* _type narrowing_ - Typescript rozmontowuje typy do "najmniejszych" możliwych - doprecyzowanie typów
* _short circut opeartor_ - szukanie najkrótszych ścieżek np. sprawdzienie tylko jednej części przy || lub && jeśli się
  da
* _type widening_ -
  ```
  const EUR = "EUR" //typ "EUR"
  let euro_zmienne = EUR //typ string - typescript to sobie rozszerzy```
* _type guards_ - `typeof`, _custom type guard_:
  ```
  interface SomeInterface {
    type: "some_interface"
  }
  
   function jestemTymInterfejsem(obiekt: any): obiekt is SomeInterface {
    return typeof obiekt.type === "some_interface"
  }```

* _assert functions_ -
* jeśli do unknowna przypiszemy określoną typem / interfejsem zmienną, to od tego czasu ta zmienna jest określona
* opóźnianie błędów do runtime'u

``` 
var sth: Interface | undefined

if(!sth) {
    //jeśli jest undefined to rzucamy error i nie musimy go głębiej obsługiwać
    throw new Error();
}

//tutaj już musi być interfejsem
```

* czasem pozwolenie Typescriptowi na propagowanie (wywnioskowanie typu) jest niezłym pomysłem
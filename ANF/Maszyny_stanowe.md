# Maszyny stanowe

## Primitive obsession

Mamy dane oderwane od siebie zawarte w typach prostych (w szczególności `boolean`)

<pre>
data: [obj1, obj2, obj3]
hasError: boolean
isLoading: boolean
</pre>

* I bez sensu jest jak np. mamy jednoczeście `isLoading = true; hasError = true`
* A 3 zmienne boolowske to 2^3 = 8. A jak coś ma jeszcze enuma z większą ilością wartości to to tylko rośnie.
* Brak abstrakcji dla przejść i możliwość przejść do stanów niepoprawnych.


## Szukanie abstrakcji

* Co jest wspólne a co jest szczególne - ale po funkcjonalności, nie po danych
* Widok to nie zawsze jest stan - widok to tylko to co widzi użytkownik,
  stan to punkt w którym znajduje się jakiś proces 
* Karteczka i rysujemy ;) Jak zakodujemy zły pomysł na rozwiązanie problemu to ciężko go jest wyrzucić
* Unia dyskryminacyjna* może zapewnić nam, że w poszczególnych stanach będziemy mieć zawsze konkretne
zmienne, które zostaną zniszczone jeśli przejdziemy do innego stanu
* Logika nie staje się prostrza - logika staje się bardziej uporządkowana - podnosi koszt
* Maszyny stanowe (jak wszystko) nie nadaje się do wszystkiego - nail and hammer - 
np. lista z filtrami - przestrzelenie 


* [Typescript] Template literal types
* [Typescript] Unia dyskryminacyjna
<pre>
export type AuthorizeDeviceState = 
| {
    "type": LOADING
}
| {
    "type": LOGGED_OUT
}
| {
    "type": ALLOW_TEMPORARY_TOKEN,
    "tokenId": string,
    "instruction": string
}
</pre>
* [Typescript] assertion function
* [xstate] ? programowanie w json :) - https://xstate.js.org/docs/recipes/react.html


## Model base testing
* Maszyna stanowa sprawia, że automatycznie możemy wygenerować scenariusze testowe - black-box testing - nie dotykamy kodu
* Definiujemy zdarzenia powodujące zmianę stanu i asercje, które zweryfikują czy jesteśmy w oczekiwanym stanie
* Jedna sekwencja przejść --> jeden test


* [Cypres] ? testy end-to-end


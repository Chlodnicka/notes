#  Typy jako zbiory

# Typy rozłączne i nie
- string to nie number itd.
- null lub undefined (flaga: strictNullChecks, 
  jeśli włączymy to musimy deklarować że coś jest string lub null, 
  jeśli nie to null i undefined mogą być składową każdego z typów)

## Unie i przecięcia
- `TaxiDriver` & `Developer` - developer taksówkarz - przecięcia
- `TaxiDriver` | `Developer` - developer lub taksówkarz lub developer taksówkarz - unia

## Unie dyskryminacyjne 
- type A | B | C - zmienna może być któregokolwiek typu, ale jeśli nie mają wspólnej struktury
to Typescript nam zablokuje użycie
- Zgodnie z konwencją jest to pole `type` typu stringowego
- Jak się dostaniemy do tego pola to sprawdzamy, co tam mamy i po tym wiemy co to za typ
  // SUMY ZBIORÓW
```
{
type A = { type: "A" }
type B = { type: "B" }
type C = { type: "C" }
type Union = A | B | C
type PropType = Union['type'] // "A" | "B" | "C"
}

{
// niech choćby jedno będzie nadtypem (nadzbiorem) pozostałych - to "połknie" pozostałe
// pamiętamy: string | "ABC" = string
type A = { type: string }
type B = { type: "B" }
type C = { type: "C" }
type Union = A | B | C
type PropType = Union['type'] // string
}
```

```
type Invoice = {
  type: "INVOICE",
  number: string,
  date: Date
  positions: {
    name: string
    price: number
    quantity: number
  }[]
  rebate: number
}

type Bill = {
  type: "BILL",
  date: Date
  totalPrice: number
}

type DeptPayment = {
  type: "DEPT",
  date: Date
}

type CompanyPurchase = Invoice | Bill ;
// type CompanyPurchase = Invoice | Bill | DeptPayment;

const getPrice = (purchase: CompanyPurchase): number => {
  // implementation here...
  switch (purchase.type) {
    case "BILL":
      return purchase.totalPrice;
    case "INVOICE":
      return purchase.positions.reduce((acc: number, item) => acc + item.price * item.quantity, 0)
    //exhaustiveness check - kod nadmiarowy, w runtime go nie potrzebujemy, to jest check dla typescripta czy
    // ogarnęliśmy wszystkie unie
      //jak odkomentuje tu DeptPayment to rzuci błąd
    default:
      let x: never = purchase;
      return purchase;
  }
}

// 🔥 a potem rozszerzamy Unię o trzeci typ, np.
// type DebtPayment = { amount: number; due: Date }
```

## Nadtypy i podtypy
- dotyczy klas customowych jak i typów w typescripcie
- np. PropertyKey > string > 
  
## Typy top i bottom
- Typ top: zawierający wszystkie możliwe typy np. `any`, `unknown`
- Typ bottom: nie zawierający nic np. `never` - to znaczy że nie istnieje wyrażenie, które zaspoikoi typ gruszki i pietruszki,
  opisuje fragmenty kodu które kończą się błędem, pętlą nieskończoną, exhoustiveness check
- `any` można użyć wszędzie, bardzo unsafe type, gubi błędy w kompilacji, wybuchnie w runtime
- `unknown` - wszystko możemy przypisać, nie wiemy co to jest więc nie za bardzo mamy jak tego użyć - musimy to sprawdzić
- *customowe type guardy
- niepolecane: `Function`, `Object` - podobne do `any`
- `Function` - pozwala nam coś wywołać jako funkcję ale możemy do tego przypisać cokolwiek
- `Object` - można przypisać prymitywa, opiszmy `object` - tam nie przypiszemy prymitywa
- *autoboxing w jsach
- _excessive attribute check_ 
- _weak_types_ - co ze zmienną obiektową, która wszystkie pola ma opcjonalne - możemy tam przypisać cokolwiek

## Typy a interfejsy

- obiekty możemy reprezentować tak i tak, można je rozszerzać i implementować
- unii nie jesteśmy w stanie zaimplementować interfejsu ani _conditional types_
- _declaration merging_ - tylko interfejsy - przydatne do rozszerzania zewnętrznych bibliotek - typescript uwzględni
  deklaracje wszystkich deklaracji interfejsu o tej samej nazwie
- interfejsy muszą z góry znać wszystkie pola (odpadają unie, typy warunkowe)
- kod z interfejsami może być kompilowane szybciej - cacheuje sobie zawartość, bo wszystkie pola są znane
w małej skali to nie ma znaczenia
- interfejs przechowywany w pamięci typescripta 
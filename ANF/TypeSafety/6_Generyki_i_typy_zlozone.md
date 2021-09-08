# Generyki i typy złożone

## Generyki

* typy parametryzujący inne typy

``` 
type Storage<T> = {
    data: T[],
    add(t: T): void
}
```

* _generic constraints_
  ``` 
    class AnotherStorage<T extends {id: string}> {
    }
  
    const anotherStorage = new AnotherStorage({id: "TEST"})
  ```
* można jawnie zadeklarować, czym będzie typ generyczne
* generyczne funkcje vs funkcja ze sparametryzowanym typem
* `T` - może być czymkolwiek

## Typy mapowane

* budujemy nowe typy na podstawie innych

``` 
export interface Transfer {
  id: string;
  amount: number;
  title: string;
  payerAccount: string;
  beneficiaryAccount: string;
  beneficiaryAddress?: string;
  scheduledAt: string;
}

type T1 = Partial<Transfer> //nowy typ ma wsie pola stają się opcjonalne
type T2 = Required<Transfer> //wsie pola stają się wymagane
// type T2 = Required<Partial<Transfer>>
type T3 = Pick<Transfer, "id" | "amount"> //nowy typ ma tylko te pola, które wyszczególniliśmy
type T4 = Omit<Transfer, "id" | "amount"> //wsie poza tym

type T5 = Reveal<T> //sprawdza zawartość typu

const new: T2 = {...}
```

## Typy warunkowe

``` 
type X = T1 extends T2 ? A : B;
```

* _naked/distributive types_
* `infer`

## Typy warunkowe mapowane

* ???
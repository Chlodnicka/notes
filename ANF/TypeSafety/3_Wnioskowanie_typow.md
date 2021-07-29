# Wnioskowanie typow

1. Wyrażenia a instrukcje
    - instrukcje (jak `if`) - nie można przypisać ich do zmiennej
    - wyrażenia - mają typ i można przypisać je do zmiennej

1. Typescript umie wywnioskować typ - jak najwęziej potrafi, ale nie czyta nam w myślach
   ``` 
   const object = {
        name: 1,
        payment: "EUR"
   } --> typescript to wywnioskuje jako {name: number, payment: string}
   --> nie wie, że może chcemy tam literał wstawić 
   ```

1. `type Result = {[key: string]: number}` - tak można otypować hash array
1. Typescript nie umie wywnioskować parametrów funkcji, czasem umie typ wynikowy
   - np. jak konkatenujemy coś w wewntrz funkcji to z natury jsa
   to zawsze będzie string (string jako joker xD)
     
1. Problem z otypowaniem tego co jest zwracane asynchronicznie np. z API
   - Typescript nie wie co się dzieje w runtime aplikacji bo go już tam dawno nie ma
   - Więc nam nie rzuci błędem jeśli coś jest nie tak 
   - axios może pomóc to sparametryzować, natywny fetch tego nie umie
   
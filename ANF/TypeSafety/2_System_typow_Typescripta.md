# System typów Typescripta

## Typowanie statyczne, silne, słabe, dynamiczne
* Statyczne - zmienna dostaje od początku do końca życia jeden konkretny typ, 
  statycznie pisze się wolniej, ale czyta się szybciej
  * Explicite - w adnotacji
  * Implicite - wnioskowany 
* Dynamiczne - tworząc zmienną nadajemy mu jakiś typ, ale może się zmienić
* Silne - bardziej strict i na mniej pozwala, częściej rzuca błędami (TypeError albo Syntax error)
* Słabe - koercja - porównanie niekompatybilnych typów np. string i number
* [Języki] - Java: statycznie typowany, raczej silnie 
* Gradually typed - w typescript część flag można ustawić na `scrit`,
ale część kodu może być otypowana, część nie np. `any`

## Apparent vs actual type
* apparent type vs actual type - typ, który kompilator widzi a jaki ma rzeczywiście (polimorfizm)

## Typowanie strukturalne a nominalne
* nominalne: dwie klasy o tej samej strukturze nie są tożsame
* strukturalne: dwie klasy o tej samej strukturze są tożsame (Typescript)


# Dodatkowo
* Let - zmienna, która może zostać zadeklarowana tylko raz 
* Iterable 
* Wnioskowanie typu, adnotacja typu, asercja typu - trochę niebezpieczne, kompilator myśli, że to number,
ale ja wiem lepiej że to typ `T` - `var expr = value as T` - zastosowanie jako ostateczność, bo możemy się pomylić,
  rzutowanie typu na siłę zazwyczaj nie jest dobrym pomysłem
* Przestrzenie nazw: przestrzeń zmiennych i przestrzeń typów - można stworzyć typ i zmienną o tej samej nazwie
`type Result = ReturnType<typeof add>`
  

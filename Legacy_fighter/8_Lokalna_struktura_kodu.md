# Lokalna struktura kodu

## Zasady i pryncypia 

Zasada skauta - wielki blob kodu, pojedyncze refaktoryzacje -> extract method, inline variable, magiczne stałe.
Poprawa lokalnej cechy kodu. Drobne problemy lokalne po prostu naprawiaj. 

Teoria rozbitych okien / boiling frog - utrata jakości kodu następuje w dłuższej perspektywie, małe zmiany się kumulują.
Ochrona osiągniętych efektów. 
Parallel models / feature flags.
Trzeba reagować na akty wandalizmu xD

Brzydkie zapachy kodu

Kod degraduje się powoli. Symptomy -> brzydkie zapachy _code smell_ -> Kent Beck.
Kiedy powinniśmy reagować? 

Bloaters: długie klasy, metody, listy parametrów, obsesja typów prymitywnych - zaciemnia kod, utrudnia jego czytanie
Object-Orientation Abusers - odrzucenie spadku otrzymanego z nadklasy, instrukcje switch/if w zależnosci od typu obiektu
Change preventers: utrudniające wprowadzanie zmian w kodzie, shotgun surgery - wiele pozornie niepowiązanych miejsc,
rozbieżne zmiany wprowadzane dla całkowicie odmiennych funkcjonalności w tym samym miescu (funkcji/klasie)
Dispensables: nieużywany, martwy kod, zakomentowany kod, leniwy kod  (nieosiągalny przez niemożliwość np. przejścia ifa)
Couplers: związanie z powiązaniami w kodzie - niezachowanie poziomu intymności między klasami, zazdrość o dane -
jedna klasa korzysta z danych innej klasy częściej niż ze swoich, łańcuchy wywołań - silne sprzężenie obiektu, niewłaściwe
użycie paradygmatu obiektowego

Wewnętrzne (w klasie) / zewnętrzne (pomiędzy klasami)

Extract method / Introduce Class / przywrócenie polimorfizmu

Feature envy*

Solid vs stupid
(single responsibility, open-close, Liskov substitution, interface segregation, dependency inversion)
(singleton - tight coupling - untestability - premature optimization - indescriptive naming - duplication)

* uogólnienie na podstawie błędnych założeń 
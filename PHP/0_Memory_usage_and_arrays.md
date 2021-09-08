# Memory usage in PHP when working with arrays

1. Normalnie arrayki są przekazywane przez referencję do funkcji i wsio git (nowsze wersje PHP robią to cichaczem)
2. Problem jest wtedy, gdy zaczynamy modyfikować arraykę
    * wtedy kopiujemy to do nowej zmiennej i zajmujemy kolejne tyle RAMu co poprzednia (_copy on write_)
    * i tak w nieskończoność
3. Jeśli chcemy modyfikować arraykę to lepiej ją przekazać z `&` stricte przez referencję i wymuszamy pracę na tym
   konkretnym zasobie w pamięci

# Memory usage

1. `memory_get_usage` i `memory_get_peak_usage` zwracają informację o tym, ile rzeczywiście potrzebowaliśmy pamięci do
   wykonania procesu
2. php allokuje pamięć dynamicznie, bierze kawałek, jak go wykorzysta to dobiera kolejny kawałek itd.
3. argument `$realUsage` na true przy tych dwóch funkcjach pokaże nam ile w rzeczywistości pamięci zaalokowało, nie ile
   zużyło
4. dowiemy się dzięki temu ile pamięci systemu zostało zarezerwowane na dany proces

# Strategiczne DDD - słabe strony

1. Idź zawsze do eksperta domenowego, użytkownik systemu jest przydatny, ale z ostrożnością
1. Użytkownik powie co by chciał i jak używa systemu, nie ma głębszego spojrzenia
1. Jeśli mamy tylko użytkowników to trzeba samemu stać się ekspertem domenowym i wycisnąć clue problemu z tego co mówią
1. Trzeba pamiętać, że DDD nie zawsze jest odpowiedzią na nasze problemy - nie wrzucaj wszędzie gdzie się da
1. Pamiętaj nad czym pracujesz - np. przy wysyłce maili jebać czy to jest śliczne jak to działa, nikt tego nie czyta, dodaje funkcjonalności raz na pół roku
1. Zasadnicza różnica między zmianą stanu a kolejnym krokiem/etapem (zwalidowałem, sprawdziłem constrainty) - wyliczanie ceny/podatku vat jest mocno złożone,
   ale to jest algorytm wyliczeniowy, on się nie będzie zmieniał codziennie
1. Czy problem który chcemy rozwiązać aby na pewno potrzebuje event stormingu
1. I na odwrót - to że nie widzimy procesu, nie oznacza, że procesu nie ma - może proces jest, tylko modelujemy jego część i nie widzimy 
   i wcale nie potrzebujemy go widzieć
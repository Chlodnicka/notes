# Antywzorce

## Anemiczny model domenowy (anemic domain model)

https://martinfowler.com/bliki/AnemicDomainModel.html

Przypomina właściwy model domenowy (obiekty odpowiadające bytom rzeczywistym, które są w relacjach z innymi obiektami), 
ale w rzeczywistości obiekty te ograniczają się do funkcjonalności "worka na dane", których używają serwisy, wewnątrz których 
zamknięta jest logika domenowa. Serwisy ustawiają serie setterów na obiektach domenowych, logika domenowa wycieka poza obiekt,
którego dotyczy.

Nie ma wiele wspólnego z OOP, chociaż używa obiektów. To ukryty w klasach styl proceduralnego programowania.


# Principles / constraints / random notes

## Tell don't ask

https://martinfowler.com/bliki/TellDontAsk.html

* No return values
* No side effects changing "global variables"
* Don’t use exceptions as return values
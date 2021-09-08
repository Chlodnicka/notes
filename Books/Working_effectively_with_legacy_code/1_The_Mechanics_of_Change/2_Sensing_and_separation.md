# Sensing and separation

1. Są dwa główne powody do odplątywania zależności:
    * _sensing_ - _we brak dependencies to sense when we cant access values our code computes_ - chcemy sprawdzić jak
      nasz kod działa naprawdę
    * _separation_ - _we brak dependencies to separate when we cant event get a piece of code into a test harness to
      run_ - chcemy w ogóle sprawić, by dało się sprawdzić, jak nasz kod działa
2. _Sensing_:
    * główna technika rozbijania zależności: _faking collaborators_ - zastępujemy je _fake objects_ - testowe
      implementacje schowane za interfejsem klasy kolaborującej
    * _mock_ - oczekujemy od nich konkretnego zachowania np. sprawdzenia, czy metoda się wywołała
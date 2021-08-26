# It takes forever to make a change 

1. Zrozumienie kodu - w splątanym legacy to ciężke do zrobienia i nie mamy pewności, czy na pewno niczego nie pominęliśmy
1. _Lag time_ - czas między zrobieniem zmiany a feedbackiem na jej temat
1. "Programowanie bardziej jak jazda samochodem niż czekanie na przystanku autobusowym ;)"
1. Zależności - ukrywanie pod interfejsami, _dependency inversion principle_
  - jeśli kod zależy od interfejsu, kod kliencki nie musi się zmieniać w ogóle, nawet jeśli 
  implementacja interfejsu się zmieniła, a interfejs nie. A interfejs sam w sobie zmienia się zdecydowanie
  rzadziej, niż jego implementacja
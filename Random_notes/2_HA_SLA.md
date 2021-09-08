# HA - High availability software

1. oprogramowanie które działa i jest dostępne niemal cały czas
1. _high availability_ to wysoki procent czasu, w którym system funkcjonuje poprawnie (1 - (downtime/total time)) * 100%
1. standardowo chce się osiągnąć 99.999%
1. skalowalność
1. _checkpointing_ - aktywny subsytem musi się komunikowawać z systemami oczekującymi _stand by_ aby być pewnym, że ten
   jest w każdej chwili w stanie przejść do stanu aktywnego
1. _in service upgrades_ - wdrażanie aktualizacji na subsystemach _stand by_, szybka możliwość powrotu do poprzedniej
   wersji
1. minimalizacja czasu oczekiwania podsystemów oczekujących w _stand by_ aż przejdą w stan aktywny

# SLA - service-level agreement

1. kontrakt między dostawcą a odbiorcą serwisu, określa nie sposób ale raczej poziom - konkretne metryki (szybkość
   odpowiedzi, niezawodność)
1. dostępność serwisu, ilość błędów, bezpieczeństwo, jakość

# Circuit breaker - Ganesha

1. https://martinfowler.com/bliki/CircuitBreaker.html


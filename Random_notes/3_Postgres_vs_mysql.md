# Postgres vs Mysql

1. postgres lepszy w zapis bez locków - concurrent write
2. mysql (innodb) - robi lock, ale przy aktualizacji per wiersz nie lockuje się całej tabeli
3. postgres pozostawia większe pole manewru jeśli chodzi o relacje w bazie (np. relacje typu dziecko - rodzic)
4. concurrency - w postgresie robi snapshot na początku i na tym pracyje dany wątek, za każdym razem robi nową "wersję" (vaccum - wywala martwe tuple)
5. tryby: _read commited_ (przy locku ponawia), _serializable_ (przy locku wywala błąd, kontrola nad tym co z tym lockiem zrobić)
6. _SELECT FOR UPDATE_
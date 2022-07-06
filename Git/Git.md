# GIT

https://learngitbranching.js.org/?locale=en

1. Projekt w Gicie to lista commitów (każdy ze wskazaniem na swojego poprzednika).
Można o nim myśleć jako o acyklicznym grafie skierowanym. 
2. Każdy commit (poza pierwszym) ma wskaźnik do swojego rodzica
3. Commit to wierzchołek grafu
4. Branch to identyfikator kierujący do określonego commita. Jest modyfikowalny, 
można przypisać go do innego commita
```
git branch someBranch (tworzy nowy branch w aktualnym położeniu)
git checkout someBranch (przenosi nas do innego brancha)
git checkout -b someOtherBranch (tworzy i przenosi nas do nowego brancha)
```
5. Merge to szczególny rodzaj commita - wierzchołek ze wskaźnikiem do dwóch rodziców.
Przy mergu łączymy pracę z dwóch różnych commitów. Mogą zdarzyć się konflikty.
```
git merge someBranch 
(domergowuje zmiany z brancha someBranch do aktualnego położenia, 
tworzy commit mergujący i przsuwa wskaźnik aktualnego położenia na nowopowstały commit)
```
6. Rebase pobiera 1 lub więcej commitów, kopiuje je i ustawia w odpowiednim miejscu. 
Tworzy się w ten sposób sekwencja commitów, nie ma żadnego merga dwóch i konfliktów. 
Bierze commit z miejsca w którym jesteśmy (lub oznaczonego w poleceniu) i przesuwa je 
do docelowego.
```
git rebase main (dokłada aktualne położenie do gałęzi main)
git rebase someBranch (gdy jesteśmy w main, a main jest przodkie someBranch to przesuwa wskaźnik main na someBranch)
```
7. HEAD - symboliczna nazwa dla aktualnie wybranego commita, wierzchołka, na którym aktualnie się znajdujemy
HEAD się przemieszcza w drzewie projektu w zależności od wykonywanych poleceń np. 
```
git checkout main (wywołana na branchu someBranch przemieszcza HEAD z someBranch na main)
git commit ... (przesuwa HEAD z C1 na kolejny, który właśnie stworzyliśmy C2)
```
8. Po drzewie można poruszać się (HEADem) używając nazw branchy, hashy commitów lub ustawiając pozycję względną.
```
git checkout HEAD^ //skaczemy do commita poprzedzającego aktualny
git checkout main^ //skaczemy do commita poprzedzającego commita na który aktualnie wskazuje branch main
git checkout HEAD~4 //skaczemy o 4 przodków wstecz
git checkout HEAD~^~2 //skaczemy: commit do góry, do drugiego rodzica (przy mergu), o dwa commity do góry
git checkout HEAD~^~4 //skaczemy: commit co góry, do pierwszego rodzica (przy mergu), o 4 commity do góry
```
9. Może się to przydać, gdy chcemy sforsować gałąź - przypisać ją na siłę do jakiegoś commita
```
git branch -f main HEAD~3 //przypisz branch main 3 commity wstecz za HEAD
```
10. Reset - przesuwa referencję brancha do starszego commita, 
dobrze działa na lokalnym środowisku (dopóki nie zrobimy pusha)
```
git reset HEAD~1 //przesuwa referencję brancha o jeden commit wstecz od aktualnej pozycji
git reset HEAD^ //
```
11. Revert - tworzy nowy commit który anuluje zmiany poprzednika
```
git revert HEAD
```
12. Cherry-pick- przenoszenie pracy z commitów 
```
git cherry-pick C1 C2 C3 //przenosi zmiany z 3 commitów (w tej kolejności) do obecnej lokalizacji (HEAD)
```
13. Interaktywny rebase - potężne narzędzie, umożliwia przenoszenie pracy między branchami (patrz pkt 6),
ale zapewnia też możliwość zmiany ich kolejności, omijanie niektórych itd. Potrzebna jest bazowa znajomość vima.
```
git rebase -i HEAD~4 //wybiera do pracy 4 ostatnie commity od HEAD i 
//umożliwia pracę na nich, można przesuwać kolejność, wykluczać itd
//realizuje zmiany od commita za wybranymi (4)
```
14. Tagi - brancha są nietrwałe i przenoszalne, tagi trwale oznaczają konkretne commity
```
git tag V1 C1 //ustawia tag o nazwie V1 na commicie C1
git tag V2 //ustawia tag o nazwie V2 na aktualnej pozycji
```
15. Describe
```
git describe <ref> //ref to cokolwiek po czym można zientyfikować commit np. nazwa brancha
//jak nie podamy to bierze HEAD

output: <tag>_<numberOfCommits>_g<hash>
gdzie:
tag - znacznik najbliższego taga
numberOfCommits - liczba commitów do najbliższego taga
hash - hasz aktualnego commita
```
## Git zdalny

1. `git clone` - tworzenie lokalnej kopii zdalnego repo
2. Gałęzie zdalne - odzwierciedlają stan zdalnych repo (od czasu ostatniej komunikacji)
3. Jak przepinamy się na gałąź zdalną, wchodzimy w tryp "odłączonego HEADa" - nie da się pracować bezpośrednio na 
zdalnych gałęziach, można je tylko zsynchronizować ze zdalnym, ze zdalnego z lokalnym
4. Zdalne gałęzie mają nazwy 2-członowe
```
<remote_name>/<branch_name> np. defaultowo origin/main
```
5. Fetch - pobieranie danych ze zdalnego repo
```
git fetch
```
Pobiera commity, które są w zdalnym ale nie w lokalnym. Aktualizuje miejsce, które wskazuje na zdalne -> origin/main
Nic nie robi ze stanem lokalnym. Lokalna kopia `origin/main` zostanie zaktualizowany ale lokalny `main` już nie.
```
git fetch origin foo - pobierz commity ze zdalnego foo i zrzuć je na lokalną origin/foo. Z lokalną foo treba ręcznie scalić
git fetch origin <źródło (zdalne)>:<cel (lokalny)>
git fech origin foo~1:bar
* jak cel (bar) nie istnieje to go tworzy
* źródło - git pozwala na ustawienie tego parametru na "nic"
git fetch origin :bugfix - tworzy gałąź bugfix lokalnie
```
`Fetch` bez argumentów ściąga wszystko.
Zmiany pobrane ze zdalnego repo można dołączyć do loklanych branchy cherry-pickiem, rebasem czy mergem
```
git cherry-pick origin/main
git rebase origin/main
git merge origin/main
```
6. Pobieranie (`fetch`) i łączenie (`merge`) są tak powszechne, że jest osobne polecenie: `git pull`
```
git pull - merguje
git pull --rebase - rebasuje
git pull origin foo == git ferch origin foo;git merge origin/foo
git pull origin bar~1:bugfix == git fetch origin:bar~1:bugfix, git merge bugfix (do aktualnej pozycji)
```
Za rebase stoi to, że drzewo wygląda bardzo czysto (1 linia). Przeciw - rebase zmienia (pozornie) historię drzewa
commitów. Np C1 można przebazować za C3, co wygląda tak, jakby C3 zostało wykonane wcześniej niż C1. 
Merge zachowuje kolejność ale dokłada złożoności.
7. Gałęzie śledzące (`origin`): podczas pull comity są pobierane do `origin/main` a następnie za pomocą `merge` scalane z lokalnym main
8. Podczas `push` praca z main wypychana jest do zdalnej `main` (do której wskaźnik reprezentuje `origin/main`) - remote tracking
9. Przy clone te zależności tworzą się automatycznie. Git tworzy zdalną gałąź dla każdej gałęzi ze zdalnego repo, potem zazwyczaj tylko jedną gałąź lokalną (main)
Można zmienić to domyślne zachowanie i ustawić śledzenie gałęzi dowolnie
```
git checkout -b notMainBranch origin/main
lub
git branch -u origin/main foo 
lub gdy jesteśmy na danej gałęzi
git branch -u irign/main 
```
10. `git push` - przesyła zmiany do zdalnego repo. Push bez argumentów pushuje tam gdzie ustawiony jest push default.
Odpowiednik gałęzi w zdalnym repo to `remote`
```
git push <remote - gdzie do remote> <place - skąd>
np.
git push origin main 
git push (domyślnie automatyczna konfiguracja - do remota z brancha na którym jesteśmy)
git push origin foo^:main <źródło (lokalne)>:<cel (zdalny)> (chemy wypchnąć lokalny foo do zdalnego bar
* źródło - git pozwala na ustawienie tego parametru na "nic"
git push origin :side - usuwa gałąź :side ze zdalnego repo
```
11. Lokalizacja w gicie: można posługiwać sięnazwą brancha, hash commita, HEAD~1

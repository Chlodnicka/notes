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
# Inventory

1. Do zarządzania ilościa itemów/usług do sprzedaży.
    * W kontekście sprzedaży, celem jest odpowiedź na pytanie, czy możemy pokryć popyt i że sprzedaż nie ucierpi, bo nam
      rzeczy wyszły ze stocku
1. W przypadku usług to utrzymanie informacji, ile jesteśmy w stanie wykonać w danym czasie
1. _Inventory management, whether of goods or services, is about minimizing the costs of inventory while maximizing its
   benefit to the business_
1. _Inventory_ i _Product_ są mocno skorelowane
1. _Inventory_ reprezentuje zbiór _InventoryEntries_, które z kolei odzwierciedlają ilość dostępnych instancji produktu
   lub usługi
    * funkcjonalności związane z _Inventory_ mają kilka głównych zadań przydzielonych do dwóch aktorów:
      _InventoryManager_ (dodawanie nowych, odejmowanie) i _ReservationAgent_ (rezerwowanie ilości)
1. Dwa typy _Inventory entry_: _Product Inventory Entry_ i _Service inventory entry_
1. _Product inventory entry_
    * _Product inventory entry_ reprezentuje _Inventory entry_, które trzyma zbiór _Product instances_ tego samego _
      Product type_
    * Dostarcza mechanizmy do rozpoznawania, kiedy stocki zaczynają niebezpiecznie maleć
    * Śledzenie _Purchase orders_
    * _Purchase orders_ - mają jedną lub więcej _Order lines_ na itemy o tym samym _Product Type_ co _Product Inventory
      entry_ i przynajmniej jedna z _Order lines_ nie jest do końca dostarczona
    * Sprawdzenie _outstandingPurchaseOrders_ w stosunku do jednego _Product inventory entry_ można obliczyć ilość na
      zamówieniu i ilość oczekiwaną
    * _Restock policy_ - zbiór reguł określających, kiedy powinny być zamówione kolejne produkty do stocku, każdy _
      Product inventory entry_ może takie mieć (i może mieć różne). Mogą definiować takie rzeczy jak: jaki poziom
      dostępności jest optymalny? (aktualna dostępność _restockContext_), jaki poziom dostępności wywołuje domówienie
      sztuk? Jak zamówienia niezrealizowane (_outstandingPurchaseOrders_) wpływają na _restocking process_?
1. _Service inventory entry_ -> _capacity manager_
   * _capacity_ jest generaowana kiedy jakiś zasób zostaje przypisany do wykonania _Service instance_ 
   * _capacity planning_ vs _capacity management_
1. _Availability_ - jedną z kluczowych funkcji _Inventory_ jest decyzja czy _Product instnces_ są możliwe do sprzedania
   * _availabilityPolicy_ może zostać zaaplikowana dla konkretnego _InventoryEntry_ - czy klient może to kupić (np. czy jest w odpowienim wieku)
   * reguły _availabilityPolicy_ muszą zostać spełniona by wydarzył się _ReservationRequest_
1. _Reservations_ - tak naprawdę główny cel inventory - tworzenie _Reservations_ przez _Parties_
   * Proces początkuje stworzenie _Reservation request_ identyfikowalne przez _Reservation identifier_, ma zawsze _requester_ i _receiver_
   * _Reservation requests_ staje się _Reservation_
   * Każdy _Product instacje_ ma jakiś _Reservation status_: czy jest gotowe do bycia zarezerwowanym czy już zostal zarezerwowany
   * _Reservation request_ jest przekazywany jako parametr do _makeReservation_ aby stworzyć _Reservation_: 
      * _makeReservation_
      * _findInventoryEntry_
      * _canAcceptReservationRequest_ (_availabilityPolicy_)
      * _getAnyProductInstance_
   * _waitingList_ - jeszcze nie można stworzyć rezerwacji, ale będzie to możliwe w najbliższym czasie (np. przedsprzedaż itp)
   * porównująć _Reservation request -> dateReceived_ i _Reservation -> dateReservationRequestActioned_ można zbadać, jak dobrze i szybko _ReservationRequest_ przechodzi w _Reservation_
1. .   
1. .   
1. .   
1. .   
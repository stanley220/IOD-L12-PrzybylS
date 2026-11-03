# System aukcyjny

## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny. 

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna 

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego.

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([BR1](#br1)) ([UC2](#uc2), [UC3](#uc3))
3. [Kupujący](#ac2) wygrywa aukcję ([BR2](#br2)) ([UC4](#uc4))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu. ([UC5](#uc5))
5. [Sprzedający](#ac1) przekazuje produkt Kupującemu. ([UC6](#uc6))

**Scenariusze alternatywne:** 

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję. ([BR2](#br2)) ([UC4](#uc4))
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.

<a id="ac3"></a>
### AC3: Czas

Aktor reprezentujący upływ czasu. Inicjuje przypadki użycia, które są wyzwalane po upłynięciu określonego czasu (np. zakończenie aukcji).


## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję
* [UC6](#uc6): Potwierdzenie przekazania produktu
* [UC7](#uc7): Edycja danych produktu
* [UC8](#uc8): Anulowanie aukcji
* [UC9](#uc9): Przeglądanie wystawionych aukcji

[Kupujący](#ac2):
* [UC2](#uc2): Wyszukanie aukcji
* [UC3](#uc3): Złożenie oferty
* [UC5](#uc5): Przekazanie należności za wygraną aukcję
* [UC10](#uc10): Przeglądanie złożonych ofert
* [UC11](#uc11): Przeglądanie historii płatności

[Czas](#ac3):
* [UC4](#uc4): Zakończenie aukcji

---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:** 

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc2"></a>
### UC2: Wyszukanie aukcji

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) zgłasza do systemu chęć wyszukania aukcji.
2. System prosi o podanie kryteriów wyszukiwania (np. nazwy produktu).
3. [Kupujący](#ac2) podaje kryteria wyszukiwania.
4. System prezentuje listę trwających aukcji spełniających podane kryteria.
5. [Kupujący](#ac2) wybiera aukcję z listy.
6. System prezentuje szczegóły aukcji: dane produktu, aktualnie najwyższą ofertę oraz czas pozostały do zakończenia aukcji.

**Scenariusze alternatywne:** 

4.A. Nie znaleziono żadnej aukcji spełniającej podane kryteria.
* 4.A.1. System informuje o braku wyników wyszukiwania.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc3"></a>
### UC3: Złożenie oferty

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) zgłasza do systemu chęć złożenia oferty w wybranej aukcji ([UC2](#uc2)).
2. System prezentuje aktualnie najwyższą ofertę i prosi o podanie kwoty.
3. [Kupujący](#ac2) podaje kwotę oferty.
4. System weryfikuje, czy oferta spełnia warunki złożenia oferty ([BR1](#br1), [BR3](#br3)).
5. System rejestruje ofertę i informuje [Kupującego](#ac2), że jego oferta jest aktualnie najwyższa.
6. System informuje [Kupującego](#ac2), którego oferta została przebita, o złożeniu wyższej oferty.

**Scenariusze alternatywne:** 

1.A. Aukcja została już zakończona.
* 1.A.1. System informuje o zakończeniu aukcji.
* 1.A.2. Koniec przypadku użycia.

4.A. Podana kwota nie spełnia reguły [BR1](#br1).
* 4.A.1. System informuje o zbyt niskiej kwocie oraz o minimalnej kwocie, jaką można zaoferować.
* 4.A.2. Przejdź do kroku 2.

4.B. Ofertę próbuje złożyć Sprzedający produktu ([BR3](#br3)).
* 4.B.1. System informuje, że Sprzedający nie może składać ofert we własnej aukcji.
* 4.B.2. Koniec przypadku użycia.

6.A. Złożona oferta jest pierwszą ofertą w aukcji.
* 6.A.1. Koniec przypadku użycia.

---

<a id="uc4"></a>
### UC4: Zakończenie aukcji

**Aktorzy:** [Czas](#ac3), [Kupujący](#ac2), [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Czas](#ac3) sygnalizuje upłynięcie czasu trwania aukcji.
2. System kończy aukcję i ustala zwycięzcę zgodnie z regułą [BR2](#br2).
3. System informuje [Kupującego](#ac2), który wygrał aukcję, o wygranej oraz o kwocie do zapłaty.
4. System informuje [Sprzedającego](#ac1) o zakończeniu aukcji i o tym, kto ją wygrał.
5. System informuje pozostałych [Kupujących](#ac2), którzy złożyli oferty, o przegraniu aukcji.

**Scenariusze alternatywne:** 

2.A. W aukcji nie złożono żadnej oferty.
* 2.A.1. System informuje [Sprzedającego](#ac1), że produkt nie został sprzedany.
* 2.A.2. Koniec przypadku użycia.

---

<a id="uc5"></a>
### UC5: Przekazanie należności za wygraną aukcję

**Aktorzy:** [Kupujący](#ac2), [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Kupujący](#ac2) zgłasza do systemu chęć zapłaty za wygraną aukcję.
2. System prezentuje kwotę do zapłaty oraz dostępne sposoby płatności.
3. [Kupujący](#ac2) wybiera sposób płatności i potwierdza płatność.
4. System weryfikuje poprawność płatności.
5. System rejestruje płatność i informuje [Kupującego](#ac2) o jej przyjęciu.
6. System informuje [Sprzedającego](#ac1) o opłaceniu produktu.

**Scenariusze alternatywne:** 

1.A. Aukcja została już opłacona.
* 1.A.1. System informuje, że należność została już uregulowana.
* 1.A.2. Koniec przypadku użycia.

4.A. Płatność nie powiodła się.
* 4.A.1. System informuje o nieudanej płatności.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc6"></a>
### UC6: Potwierdzenie przekazania produktu

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu przekazanie produktu Kupującemu.
2. System prosi o podanie informacji o sposobie przekazania produktu (np. numeru przesyłki).
3. [Sprzedający](#ac1) podaje informacje o przekazaniu produktu.
4. System zapisuje informacje i oznacza aukcję jako zrealizowaną.
5. System informuje [Kupującego](#ac2) o przekazaniu produktu.

**Scenariusze alternatywne:** 

1.A. Produkt nie został jeszcze opłacony ([UC5](#uc5)).
* 1.A.1. System informuje, że nie można potwierdzić przekazania nieopłaconego produktu.
* 1.A.2. Koniec przypadku użycia.

---

<a id="uc7"></a>
### UC7: Edycja danych produktu

**Aktorzy:** [Sprzedający](#ac1)

*Przypadek użycia zidentyfikowany na podstawie macierzy CRUDL (brak U dla obiektu Produkt). Scenariusze do opracowania.*

---

<a id="uc8"></a>
### UC8: Anulowanie aukcji

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

*Przypadek użycia zidentyfikowany na podstawie macierzy CRUDL (brak D dla obiektów Aukcja i Produkt). Scenariusze do opracowania.*

---

<a id="uc9"></a>
### UC9: Przeglądanie wystawionych aukcji

**Aktorzy:** [Sprzedający](#ac1)

*Przypadek użycia zidentyfikowany na podstawie macierzy CRUDL (brak L dla obiektu Produkt z perspektywy Sprzedającego). Scenariusze do opracowania.*

---

<a id="uc10"></a>
### UC10: Przeglądanie złożonych ofert

**Aktorzy:** [Kupujący](#ac2)

*Przypadek użycia zidentyfikowany na podstawie macierzy CRUDL (L dla obiektu Oferta tylko w przypadku użycia inicjowanym przez system). Scenariusze do opracowania.*

---

<a id="uc11"></a>
### UC11: Przeglądanie historii płatności

**Aktorzy:** [Kupujący](#ac2)

*Przypadek użycia zidentyfikowany na podstawie macierzy CRUDL (brak L dla obiektu Płatność). Scenariusze do opracowania.*

---

## Obiekty biznesowe (inaczej obiekty dziedzinowe lub informatyczne)

### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupu, produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę. 

### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

### BO3: Oferta

Propozycja zakupu produktu złożona przez Kupującego w ramach aukcji. Zawiera kwotę, za którą Kupujący chce nabyć produkt, oraz czas złożenia oferty.

### BO4: Płatność

Należność przekazana przez Kupującego, który wygrał aukcję, za zakupiony produkt. Zawiera kwotę, sposób płatności oraz informację, czy płatność została przyjęta.

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.


<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujących](#ac2), który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

<a id="br3"></a>
### BR3: Oferty Sprzedającego

[Sprzedający](#ac1) nie może składać ofert w aukcji, w której wystawił produkt.

<a id="br4"></a>
### BR4: Wiążący charakter oferty

Złożonej oferty nie można zmienić ani wycofać.

## Macierz CRUDL


| Przypadek użycia                                  | Aukcja | Produkt | Oferta | Płatność |
| ------------------------------------------------- | ------ | ------- | ------ | -------- |
| UC1: Wystawienie produktu na aukcję               |   C    |    C    |        |          |
| UC2: Wyszukanie aukcji                            |   LR   |    R    |   R    |          |
| UC3: Złożenie oferty                              |   R    |         |   CR   |          |
| UC4: Zakończenie aukcji                           |   RU   |    R    |   L    |          |
| UC5: Przekazanie należności za wygraną aukcję     |   R    |    R    |   R    |    C     |
| UC6: Potwierdzenie przekazania produktu           |   RU   |    R    |        |    R     |
| UC7: Edycja danych produktu                       |   R    |    U    |        |          |
| UC8: Anulowanie aukcji                            |   D    |    D    |        |          |
| UC9: Przeglądanie wystawionych aukcji             |   L    |    L    |        |          |
| UC10: Przeglądanie złożonych ofert                |   R    |         |   L    |          |
| UC11: Przeglądanie historii płatności             |        |         |        |    L     |

### Analiza kompletności

Macierz dla przypadków użycia UC1–UC6 (wynikających z procesu [BC1](#bc1)) wykazała następujące braki:

* **Aukcja** – brak operacji D: Sprzedający nie ma możliwości wycofania aukcji. Dodano [UC8](#uc8).
* **Produkt** – brak operacji U, D i L: nie można poprawić danych produktu, usunąć go ani przejrzeć listy własnych produktów. Dodano [UC7](#uc7), [UC8](#uc8) oraz [UC9](#uc9).
* **Oferta** – operacja L występuje tylko w [UC4](#uc4), który jest inicjowany przez [Czas](#ac3), więc Kupujący nie może przejrzeć swoich ofert. Dodano [UC10](#uc10). Brak operacji U i D jest zamierzony – wynika z reguły [BR4](#br4).
* **Płatność** – brak operacji L: Kupujący nie może przejrzeć historii płatności. Dodano [UC11](#uc11). Brak U i D jest zamierzony – zarejestrowanej płatności się nie modyfikuje.

Po dodaniu UC7–UC11 każdy obiekt biznesowy ma zapewnione wszystkie operacje, które są potrzebne w procesie biznesowym.

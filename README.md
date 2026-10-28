**Polski** · [English](README.en.md)

---

# Matura z informatyki, poziom rozszerzony - kurs Pythona, część 6. "Funkcje"

> ### 🎬 Wideo z lekcją
> Pełne omówienie tej lekcji krok po kroku znajdziesz na moim kanale YouTube:
> **[Link do filmu na YouTube](https://youtu.be/uw6NC9ycLPE)**
>
> Na filmie piszę funkcje, które liczą pole i obwód prostokąta. Pokazuję parametry i argumenty, wartości domyślne, type hints, instrukcję `return`, zwracanie kilku wartości w krotce oraz szablon programu z funkcją `main`.

---

## Opis

Kod do szóstej części kursu Pythona, który przygotowuje do matury z informatyki na poziomie rozszerzonym. Ta część dotyczy pisania własnych funkcji.

Funkcja to nazwany fragment kodu. Piszesz go raz i wywołujesz tyle razy, ile potrzebujesz, zamiast kopiować ten sam kod. W lekcji pokazuję, jak przekazać dane do funkcji, jak oddać wynik, który funkcja wyliczy, i jak zbudować szablon programu z funkcją `main`. Z tego szablonu korzystamy w dalszej części kursu.

Dzięki funkcjom kod pisany na maturze jest krótszy i czytelniejszy. W stresie egzaminacyjnym łatwiej się w nim odnaleźć niż w jednym długim skrypcie bez podziału na funkcje.

W repozytorium są też pliki z poprzednich części kursu, od `app-1` do `app-5`.

## Wymagania

- Python 3.10 lub nowszy. Sam plik `app-6-funkcje.py` działa od wersji 3.9, ale `app-4-instrukcje-warunkowe.py` korzysta z instrukcji `match`, która jest dostępna od Pythona 3.10
- Brak zewnętrznych zależności. Pliki z poprzednich części kursu korzystają tylko z modułów `random` i `math` z biblioteki standardowej

## Uruchomienie

```bash
git clone https://github.com/kmprograms/matura-kurs-python-6-funkcje
cd matura-kurs-python-6-funkcje
python app-6-funkcje.py
```

Program nie czeka na dane z klawiatury, bo wywołania z `input` są zakomentowane. W nagraniu uruchamiam skrypt zieloną strzałką w PyCharm. Pod spodem wykonuje ona to samo polecenie `python` z nazwą pliku.

Pliki z poprzednich części kursu uruchamiasz tak samo, np. `python app-5-petle.py`.

## Struktura projektu

| Plik | Opis |
| --- | --- |
| `app-1-pierwszy-program-zmienne.py` | Pierwszy program, zmienne różnych typów, f-stringi z formatowaniem, operatory arytmetyczne, zamiana wartości zmiennych, parametry `end` i `sep` funkcji `print`, konwersja typów, operatory `+=`, `-=` i `*=` |
| `app-2-liczby-calkowite.py` | Działania na liczbach całkowitych, w tym `//` i `%`, parzystość i podzielność, operatory relacji, spójniki `and` i `or`, wyznaczanie cyfr liczby, zamiana sekund na godziny, minuty i sekundy |
| `app-3-pozyskiwanie-danych-systemy-liczbowe-float.py` | Pobieranie danych przez `input`, losowanie z modułem `random`, systemy liczbowe, operacje na bitach, moduł `math` |
| `app-4-instrukcje-warunkowe.py` | Operatory logiczne, leniwe obliczanie, instrukcje `if`, `elif` i `else`, wyrażenie warunkowe, instrukcja `match`, funkcje `min`, `max` i `abs` |
| `app-5-petle.py` | Pętla `while`, instrukcje `break` i `continue`, pętla `for` z `range`, przechodzenie po liście i napisie, pętla w pętli |
| `app-6-funkcje.py` | Kod z tej lekcji: własne funkcje, parametry i argumenty, wartości domyślne, type hints, `return`, zwracanie krotki, funkcja `main` i sekcja `if __name__ == '__main__':` |

## Zakres lekcji i omówienie kodu

Wszystkie fragmenty w tej sekcji pochodzą z pliku `app-6-funkcje.py`.

### Definicja i wywołanie funkcji

```python
def pole_prostokata_v1() -> None:
    a = int(input("Podaj pierwszy bok prostokąta: "))
    b = int(input("Podaj drugi bok prostokąta: "))
    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")

# pole_prostokata_v1()  # Tak wywołasz funkcję pole_prostokata_v1
# pole_prostokata_v1()
```

Funkcję definiujesz słowem kluczowym `def`. Po nim podajesz nazwę funkcji, okrągłe nawiasy i dwukropek. Ciało funkcji wcinasz czterema spacjami, tak samo jak przy `if` czy `while`.

Sama definicja niczego nie uruchamia. Kod z ciała funkcji wykona się dopiero wtedy, gdy wywołasz ją zapisem `pole_prostokata_v1()`. Każde wywołanie to kolejne wykonanie tego samego kodu, więc nie musisz go kopiować w różne miejsca programu. W pliku oba wywołania są zakomentowane, żeby program nie czekał na dane z klawiatury.

Nazwa funkcji powinna jasno mówić, co robi jej kod. Program zwykle składa się z kilku funkcji, więc czytelne nazwy pomagają szybko znaleźć tę, której potrzebujesz.

Wadą tej wersji jest brak elastyczności. Funkcja zawsze pobiera długości boków od użytkownika, więc nie da się ich wylosować ani podać na sztywno.

### Parametry, argumenty i type hints

```python
# a oraz b to parametry
# type hints
def pole_prostokata_v2(a: int = 1, b: int = 2) -> None:
    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")


# Kiedy wywołujesz funkcję i podstawiasz konkretne dane, wtedy mówimy,
# że podajesz argumenty
pole_prostokata_v2(10, 20)

# x = int(input("Podaj pierwszy bok prostokąta: "))
# y = int(input("Podaj drugi bok prostokąta: "))
# pole_prostokata_v2(x, y)
pole_prostokata_v2(b=11, a=22)
pole_prostokata_v2()
pole_prostokata_v2(11)
pole_prostokata_v2(b=11)
```

`a` i `b` w nagłówku funkcji to parametry. Konkretne wartości podane przy wywołaniu to argumenty. Wiele osób używa tych słów zamiennie, ale warto znać różnicę.

Nazwy parametrów mówią tylko, jak odwołać się do danych w ciele funkcji. Przy wywołaniu możesz przekazać zmienne o dowolnych nazwach, np. `x` i `y` pobrane przez `input`. Dane mogą też pochodzić z losowania albo z pliku tekstowego. Funkcja się nie zmienia, zmienia się tylko sposób dostarczenia danych.

Zapis `a: int` to type hint, czyli jawne określenie typu parametru. Python go nie wymaga i bez niego program też działa. Traktuj go jednak jako obowiązkowy. Na maturze to szybka podpowiedź, jakie dane przyjmuje twoja funkcja, szczególnie gdy w stresie zaczniesz się gubić. Zapis `-> None` po nawiasach oznacza, że funkcja nic nie zwraca.

### Wartości domyślne, argumenty pozycyjne i nazwane

Argumenty pozycyjne są przypisywane do parametrów od lewej. Argument nazwany, np. `b=11`, wskazuje parametr wprost, więc kolejność przestaje mieć znaczenie. Wartości domyślne `a: int = 1` i `b: int = 2` pozwalają pominąć argumenty przy wywołaniu.

| Wywołanie | `a` | `b` | Pole | Uwagi |
| --- | --- | --- | --- | --- |
| `pole_prostokata_v2(10, 20)` | 10 | 20 | 200 | Argumenty pozycyjne |
| `pole_prostokata_v2(b=11, a=22)` | 22 | 11 | 242 | Argumenty nazwane, kolejność nie ma znaczenia |
| `pole_prostokata_v2()` | 1 | 2 | 2 | Obie wartości domyślne |
| `pole_prostokata_v2(11)` | 11 | 2 | 22 | Jedyny argument trafia do `a`, `b` ma wartość domyślną |
| `pole_prostokata_v2(b=11)` | 1 | 11 | 11 | `a` ma wartość domyślną |

### Zwracanie wyniku przez return

```python
def pole_prostokata_v3(a: int = 1, b: int = 2) -> int:
    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")
    return pole

p = pole_prostokata_v3(10, 30)
if p > 100:
    print("Pole jest duże")
```

Wypisanie komunikatu przez `print` nie oznacza, że po zakończeniu funkcji możesz korzystać z wyliczonej w niej wartości. Do tego służy słowo kluczowe `return`, po którym podajesz to, co funkcja ma zwrócić. W miejscu wywołania pojawia się wartość z `return`, tutaj 300, i trafia do zmiennej `p`. Typ zwracanej wartości opisujesz w nagłówku po strzałce, tutaj `-> int`.

`print` w funkcji nie jest obowiązkowy i nie koliduje z `return`. Służy do podglądu wartości zmiennych albo do informowania użytkownika o wynikach. Parametry odpowiadają za dane wejściowe, a `return` za wynik. Funkcje mogą się w ten sposób komunikować: wynik jednej trafia jako argument do kolejnej, a program budujesz z funkcji jak z klocków.

Funkcja bez `return` domyślnie zwraca `None`. Gdyby przypisać do `p` wynik funkcji `pole_prostokata_v2` i porównać go ze 100, program zgłosi błąd, bo nie da się porównać `NoneType` z `int`. Dlatego w nagłówkach `pole_prostokata_v1` i `pole_prostokata_v2` jest zapis `-> None`.

### Nieprawidłowe dane wejściowe

```python
def pole_prostokata_v4(a: int = 1, b: int = 2) -> int:  # -> int | None:

    # W przypadku nieprawidłowych długości boków zwracamy specyficzną wartość
    # if a <= 0 or b <= 0:
    #     print(f"Podałeś złe długości boków {a=}, {b=}")
    #     # return None
    #     return -1

    # if a <= 0 or b <= 0:
    #     raise ValueError(f"Podałeś złe długości boków {a=}, {b=}")

    pole = a * b
    print(f"Pole prostokąta o bokach {a} oraz {b} wynosi {pole}")
    return pole


print(f"Pole prostokąta: {pole_prostokata_v4(10, -20)}")
print("Koniec")
```

Boki prostokąta muszą być dodatnie, a ktoś może podać np. `-20`. Funkcja pokazuje trzy sposoby reakcji na takie dane:

1. Zwrócenie wartości specjalnej `-1`. Pole prostokąta nie może być ujemne, więc `-1` jednoznacznie oznacza, że coś poszło nie tak. Wynik możesz przypisać do zmiennej i sprawdzić instrukcją `if`.
2. Zwrócenie `None`. To jeszcze mocniej podkreśla brak poprawnego wyniku i przydaje się wtedy, gdy każda liczba może być prawidłowym wynikiem funkcji. Typ zwracany trzeba wtedy zapisać jako `int | None`. Narzędzia sprawdzające typy mogą jednak wymuszać sprawdzenie wyniku przy każdym użyciu funkcji.
3. Rzucenie wyjątku przez `raise ValueError(...)`. Program wyświetla na czerwono typ błędu, komunikat i miejsce, w którym błąd wystąpił, a potem przerywa działanie. Instrukcja `print("Koniec")` już się nie wykona. W praktyce rzucanie i przechwytywanie wyjątków to podejście zalecane w takich sytuacjach. Obsługi wyjątków na tym etapie przygotowań do matury nie omawiam.

`return` nie tylko zwraca wartość, ale też natychmiast kończy działanie funkcji. W wariancie z `-1` po wykryciu złych boków kod poniżej `if` już się nie wykona. Dzięki temu na początku funkcji możesz sprawdzić warunki prowadzące do jej szybszego zakończenia, a dopiero potem przejść do głównych obliczeń. O tym mówiłem przy omawianiu `break` i `continue` w pętlach.

W repozytorium oba warianty sprawdzania są zakomentowane, więc wywołanie z `-20` zwraca `-200`. Żeby sprawdzić wybrany wariant, odkomentuj odpowiedni fragment.

Na maturze zwykle nie musisz tego robić. W treści zadania zawsze są założenia, np. że pracujesz na liczbach dodatnich, a algorytm jest do nich dopasowany. Kontrola poprawności argumentów to jednak ważny temat przy funkcjach, dlatego go pokazuję.

### Zwracanie wielu wartości w krotce

```python
def min_max_srednia(a: int, b: int, c: int) -> tuple[int, int, float]:
    najmniejsza = min(a, b, c)
    najwieksza = max(a, b, c)
    srednia = (a + b + c) / 3
    # return min(a, b, c), max(a, b, c), (a + b + c) / 3
    return najmniejsza, najwieksza, srednia

wynik = min_max_srednia(10, 20, 30)
print(wynik)
print(wynik[0])
print(wynik[1])
print(wynik[2])

najm, najw, sr = min_max_srednia(20, 30, 40)
print(najm, najw, sr)

_, najw_2, _ = min_max_srednia(20, 30, 40)
print(najw_2)
```

Funkcja wyznacza dla trzech liczb wartość najmniejszą, największą i średnią. Wartości po `return` oddzielone przecinkami tworzą krotkę, po angielsku tuple. W type hints używasz angielskiej nazwy i w nawiasie kwadratowym podajesz typy kolejnych elementów: `tuple[int, int, float]`.

Wynik możesz wykorzystać na trzy sposoby:

1. Przypisać całą krotkę do jednej zmiennej i odwoływać się do elementów po pozycjach, tak jak w listach. Pierwszy element ma pozycję 0.
2. Rozpakować krotkę do osobnych zmiennych. Ich nazwy, np. `najm`, `najw` i `sr`, nie muszą pokrywać się z nazwami w funkcji.
3. Zastąpić znakiem `_` elementy, które cię nie interesują. Po lewej stronie musi być tyle pozycji, ile elementów ma krotka.

Zakomentowana linia pokazuje, że po `return` możesz od razu umieścić wyrażenia, bez zmiennych pomocniczych.

### Szablon programu z funkcją main

```python
def obwod_prostokata(a: int, b: int) -> int:
    return 2 * (a + b)

def main() -> None:
    print("--")
    print(obwod_prostokata(10, 20))

if __name__ == '__main__':
    main()
```

Python pozwala przeplatać definicje funkcji z ich wywołaniami. Przy zadaniu maturalnym, w którym trzeba wczytać dane z pliku, napisać kilka funkcji realizujących algorytm i rozwiązać kolejne podpunkty, taka struktura szybko prowadzi do bałaganu. Dlatego stosujemy stały układ:

1. Na górze definicje wszystkich funkcji, jedna pod drugą.
2. Pod nimi funkcja `main`, w której są wszystkie wywołania i logika programu.
3. Na końcu sekcja uruchomieniowa `if __name__ == '__main__':`, która wywołuje `main`.

Niektóre języki, np. C++, wymagają funkcji głównej. Python jej nie wymaga, ale stosujemy ją dla porządku i zgodności z dobrymi praktykami.

Gdy uruchamiasz skrypt poleceniem `python`, specjalna zmienna `__name__` (czytana jako "dunder name", od double underscore) dostaje wartość `"__main__"`. Warunek sprawdza, czy ten skrypt został uruchomiony, i wtedy wywołuje funkcję `main`. Nazwa `main` nie jest wymagana, ale stosuje ją cały świat i do tego też zachęcam.

## Wyniki

Uruchomienie pliku `app-6-funkcje.py` wypisuje:

```
Pole prostokąta o bokach 10 oraz 20 wynosi 200
Pole prostokąta o bokach 22 oraz 11 wynosi 242
Pole prostokąta o bokach 1 oraz 2 wynosi 2
Pole prostokąta o bokach 11 oraz 2 wynosi 22
Pole prostokąta o bokach 1 oraz 11 wynosi 11
Pole prostokąta o bokach 10 oraz 30 wynosi 300
Pole jest duże
Pole prostokąta o bokach 10 oraz -20 wynosi -200
Pole prostokąta: -200
Koniec
(10, 30, 20.0)
10
30
20.0
20 40 30.0
40
--
60
```

Wiersz z polem `-200` wynika z tego, że sprawdzanie boków w `pole_prostokata_v4` jest zakomentowane. Krotka z funkcji `min_max_srednia` wypisuje się w nawiasach okrągłych, z elementami oddzielonymi przecinkami.

## Uwagi implementacyjne

Type hints nie są wymagane przez Pythona. W profesjonalnych projektach kod przed wdrożeniem przechodzi przez narzędzia sprawdzające jego jakość i poprawność, a tam type hints są praktycznie obowiązkowe. W tym kursie opisujemy nimi typy parametrów i typ zwracany każdej funkcji.

Zapis `tuple[int, int, float]` w nagłówku funkcji działa od Pythona 3.9. Zakomentowany zapis `int | None` wymaga Pythona 3.10.

PyCharm przy wywołaniu podpowiada, do którego parametru trafia dany argument pozycyjny. Ostrzega też, gdy przypisujesz wynik funkcji, która nic nie zwraca. Zapisy `-> None` i `-> int` ułatwiają pracę takim narzędziom.

Po `return` możesz umieścić całe wyrażenie, jak w `obwod_prostokata`. Wersja z osobnymi zmiennymi, jak w `min_max_srednia`, bywa jednak czytelniejsza.

W kolejnych lekcjach funkcje będą zwracać także całe listy, a może i słowniki. Kolejne nagranie dotyczy list.
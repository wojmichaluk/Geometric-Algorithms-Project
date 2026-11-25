# Lokalizacja punktu w przestrzeni 2D - metoda trapezowa

Projekt z przedmiotu *Algorytmy geometryczne*. Repozytorium zawiera implementację algorytmu budującego mapę trapezową dla zadanego zbioru odcinków, a także wizualizację zarówno budowy mapy (krok po kroku), jak i wyszukiwania trapezu zawierającego dany punkt.

**Autorzy:** Wojciech Michaluk, Michał Mróz

## Funkcjonalności programu

- budowa mapy trapezowej i struktury przeszukiwań dla podziału płaszczyzny zadanego zbiorem odcinków,
- odpowiedź na pytanie, w którym trapezie leży zadany punkt,
- wizualizacja kolejnych kroków budowy mapy oraz ścieżki wyszukiwania punktu,
- interaktywne okno do wprowadzania własnych odcinków myszką,
- pomiary czasu budowy, rozmiaru struktury przeszukiwań i czasu zapytań dla zbiorów od 100 do 100000 odcinków.

## Założenia dotyczące danych

Zbiór odcinków musi być w położeniu ogólnym, tzn.

- odcinki nie przecinają się (poza ewentualnymi wspólnymi wierzchołkami),
- żaden odcinek nie jest pionowy,
- żadne dwa wierzchołki nie mają tej samej współrzędnej `x` (poza końcami połączonych odcinków).

Odcinek to para punktów `((x1, y1), (x2, y2))`, a podział to lista takich par.

## Uruchomienie programu

Potrzebne jest środowisko z odpowiednią wersją Pythona i wymaganych bibliotek. Można je przygotować następująco:

```bash
conda create -n trapezoidal-map python=3.11 tk -y
conda activate trapezoidal-map
pip install -r requirements.txt
cd code
jupyter notebook
```

Notebook należy uruchamiać z katalogu `code/`, ponieważ importy (`util`, `plotter`, `vis_bit` itd.) są względne wobec niego. Z otwartego okna (należy wkleić link, który pojawi się w terminalu) trzeba wybrać notebook `Michaluk_Mróz_kod.ipynb`. Następnie wystarczy uruchamiać kolejne jego komórki.

> **Uwaga o wersjach:** notebook używa `%matplotlib notebook`, które nie działa w Notebooku 7, dlatego w `requirements.txt` jest `notebook<7`. Starsze `ipykernel` nie współpracuje z IPythonem 9, stąd `ipython<9`.

## Zawartość notebooka

1. opis problemu i algorytmu, razem z implementacją kluczowych funkcji (`createTrapezoidalMap`, `insertIntoOne`, `insertIntoMany`),
2. testy efektywności (czas budowy, rozmiar struktury przeszukiwań, czas zapytań),
3. gotowe przykłady wizualizacji budowy mapy,
4. okno do wprowadzania własnego zestawu odcinków,
5. wizualizacja wyszukiwania trapezu dla wskazanego punktu.

### Własne odcinki

Komórka pod nagłówkiem "Przetestuj własny zbiór odcinków!" otwiera osobne okno:

- **Add line segments** - dodawanie odcinków; kliknięcia lewym przyciskiem myszy ustawiają punkty, każda para kolejnych punktów tworzy odcinek,
- **Print line segments** - wypisuje wprowadzone odcinki pod oknem, żeby można je było zapisać i np. użyć ponownie,
- **Clear display** - czyści ekran i pozwala zacząć od nowa,
- **Create trapezoid map** - otwiera okno z wizualizacją budowy mapy krok po kroku.

## Struktura repozytorium

```
.
├── code/
│   ├── Michaluk_Mróz_kod.ipynb   # główny notebook
│   ├── DataStructures.py         # klasy Point, Segment, Trapezoid, DNode, DTree
│   ├── util.py                   # funkcje pomocnicze algorytmu i generatory danych
│   ├── Examples.py               # przygotowane przykłady testowe
│   ├── plotter.py                # okno do wprowadzania odcinków i prezenter wizualizacji
│   ├── plotter_functions.py      # budowa mapy i wyszukiwanie z zapisem scen do wizualizacji
│   └── vis_bit/                  # biblioteka do rysowania* (figury, wykresy, animacje)
├── docs/
│   ├── Michaluk_Mróz_dokumentacja.pdf
│   └── Michaluk_Mróz_prezentacja.pdf
├── requirements.txt
└── README.md
```

`*` [Wizualizator](https://github.com/aghbit/Algorytmy-Geometryczne) od AGH-BIT.  

## Złożoność obliczeniowa

Dla randomizowanego algorytmu przyrostowego, gdzie `n` to liczba odcinków:

| | oczekiwana złożoność |
|---|---|
| czas budowy mapy | `O(n log n)` |
| rozmiar struktury przeszukiwań | `O(n)` |
| czas zapytania o punkt | `O(log n)` |

## Dokumentacja

Szczegółowy opis algorytmu, struktur danych i funkcji znajduje się w katalogu `docs`:

- [Dokumentacja](docs/Michaluk_Mr%C3%B3z_dokumentacja.pdf)
- [Prezentacja](docs/Michaluk_Mr%C3%B3z_prezentacja.pdf)

## Wykorzystane biblioteki

- **NumPy**: operacje matematyczne i generowanie liczb losowych,
- **Matplotlib**: rysowanie i animacje,
- **Tkinter**: okno do wprowadzania odcinków,
- **Jupyter Notebook**: środowisko uruchomieniowe.

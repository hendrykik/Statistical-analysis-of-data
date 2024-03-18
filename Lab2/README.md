# Temat: Wprowadzenie w jupyter notebook, wczytywanie danych, eksploracja danych, techniki czyszczenia danych
## Wprowadzenie
Celem zajęć jest krótkie wprowadzenie do jupyter notebooków oraz do pracy z danymi. Więcej info jak rozpocząć pracę z jupyter notebookami np. [tu](https://www.datageeks.pl/geeks-blog/40-instalacja-i-korzystanie-z-jupyter-notebook) 

Wszelkie wymagane do działania biblioteki można instalować w notebooku np.
`pip install liac-arff` lub poprzez dodanie ich do pliku [`requirements.txt`](requirements.txt) i wywołanie komendy `pip install -r requirements.txt`.

Na potrzeby zajęć przygotowałem plik [`setup.sh`](setup.sh), który można uruchomić w terminalu w celu przygotowania środowiska i rozpoczęcia pracy z tym notebookiem. 

## Pandas
Osoby, które nie miały wcześniej styczności z biblioteką `pandas` zachęcam od rozpoczęcia przygody z `pandas` od przejrzenia wprowadzenia - [`user_guide/10min.html`](https://pandas.pydata.org/docs/user_guide/10min.html).

### Import biblioteki i wczytanie pliku
zwyczajowo importujemy `pandas` jako `pd`:
`import pandas as pd`
podobnie, `numpy` importujemy jako `np`:
`import numpy as np`

#### Wczytanie danych z pliku CSV
`df = pd.read_csv('ścieżka_do_pliku.csv')`

#### Wczytanie danych z pliku Excel
`df = pd.read_excel('ścieżka_do_pliku.xlsx')`

#### Wczytanie danych z pliku parquet
`df = pd.read_parquet('ścieżka_do_pliku.parquet')`


### Przegląd danych
#### Wyświetlenie pierwszych wierszy danych
`print(df.head())`

#### Podsumowanie informacji o danych
`print(df.info())`

#### Statystyki opisowe dla danych numerycznych
`print(df.describe())`

#### Sprawdzenie brakujących wartości
`print(df.isnull().sum())`

#### Wyświetlenie unikalnych wartości dla kolumny
`print(df['nazwa_kolumny'].unique())`

#### Filtrowanie danych
- [pandas.DataFrame.filter](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.filter.html)
- logiczne warunkowanie `df[df['column'].isin(allowed_values)]`

### Grupowanie danych
[pandas.DataFrame.groupby](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html)

#### Pivot
[pandas.DataFrame.pivot](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pivot.html)

#### Time series
[time series/date functionality](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html)

## Techniki czyszczenia danych
Techniki czyszczenia danych są kluczowe do przeprowadzenia miarodajnej analizy. Czyszczenie jest zazwyczaj poprzedzone wnikliwym przeglądaniem i zrozumieniem danych, by zidentyfikować ewentualne problemy dotyczące jakości danych, takich jak:

1. Identyfikacja i usunięcie duplikatów.

Duplikaty mogą wprowadzać błędy w analizie, patrz: [`pandas.DataFrame.drop_duplicates()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.drop_duplicates.html)

2. Obsługa brakujących wartości - więcej info w [`pandas - user_guide/missing_data.html`](https://pandas.pydata.org/docs/user_guide/missing_data.html)

Brakujące dane identyfikujemy przy użyciu [`pandas.DataFrame.isna`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.isna.html) - po zidentyfikowaniu brakujących danych można rozważyć obsłużenie ich na kilka sposobów, w zależności od kontekstu i ilości brakujących danych:

Usunięcie [`pandas.DataFrame.dropna`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dropna.html#pandas.DataFrame.dropna): Wiersze lub kolumny z brakującymi danymi można usunąć, jeśli nie wpłynie to znacząco na analizę.

Imputacja [`pandas.DataFrame.fillna`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.fillna.html#pandas.DataFrame.fillna): Brakujące wartości można zastąpić wartością statystyczną (np. średnią, medianą) lub za pomocą bardziej zaawansowanych technik, takich jak imputacja wielokrotna czy K najbliższych sąsiadów (KNN).

3. Normalizacja i skalowanie danych.

W przypadku pracy z algorytmami, które są wrażliwe na skalę danych (np. algorytmy uczenia maszynowego), normalizacja (przeskalowanie wartości do zakresu [0, 1]) lub standaryzacja (przeskalowanie do rozkładu o średniej 0 i odchyleniu standardowym 1) może być konieczna.

Biblioteka [`scikit-learn`](https://pypi.org/project/scikit-learn/) oferuje kilka narzędzi do preprocessingu danych, w tym [skalowanie](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html) (np. do standardowej skali z wartościami średnimi 0 i odchyleniem standardowym 1) lub [MinMaxScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MinMaxScaler.html) oraz [normalizację](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.normalize.html) (np. skalowanie każdej próbki do długości jednostkowej).

4. Korekta typów danych.

Zapewnienie, że każda kolumna ma odpowiedni typ danych (np. liczbowy, ciąg tekstowy, data/czas), jest kluczowe dla efektywnej analizy. W pandas, można to zrobić za pomocą metody [`pandas.DataFrame.astype`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.astype.html#pandas.DataFrame.astype).

5. Kodowanie zmiennych kategorycznych.

Algorytmy uczenia maszynowego wymagają numerycznej reprezentacji danych. Zmienne kategoryczne można kodować za pomocą technik takich jak kodowanie jednoznaczne ([one-hot encoding](https://pandas.pydata.org/docs/reference/api/pandas.get_dummies.html)) czy kodowanie etykiet ([label encoding](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html)).

6. Wykrywanie i obsługa wartości odstających.

Wartości odstające mogą mieć duży wpływ na analizę statystyczną i modele predykcyjne. Można je identyfikować za pomocą metod statystycznych (np. odległość międzykwartylowa) lub wizualizacji (np. boxploty), a następnie usunąć lub zastąpić.

[scipy umożliwia policzenie zscore](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.zscore.html)

7. Czyszczenie tekstów.

W przypadku danych tekstowych, usuwanie znaków interpunkcyjnych, zbędnych spacji, konwersja na małe litery `pandas.DataFrame.str.lower` czy usuwanie słów nieznaczących - tzw. [stop words](https://www.geeksforgeeks.org/removing-stop-words-nltk-python/) mogą być konieczne do analizy tekstu. Biblioteki jak NLTK czy spaCy oferują narzędzia do przetwarzania języka naturalnego. Można też użyć technik regex lub NLP do wygenerowania nowych kolumn danych na bazie tekstowych kolumn.

## Graficzna wizualizacja danych
[User guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html)

Wymagany jest backend do wizualizacji np. biblioteka [`matplotlib`](https://pypi.org/project/matplotlib/).
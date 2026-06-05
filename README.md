# Video-Game-Sales-Prediction-Project
Projekt zaliczeniowy z Programowania 2 - analiza danych Kaggle
Cel projektu
Głównym celem projektu jest analiza historycznych danych dotyczących rynku gier wideo oraz implementacja modeli uczenia maszynowego w celu przewidywania globalnej sprzedaży poszczególnych tytułów (w milionach kopii). Projekt realizuje zadanie z zakresu regresji, wykorzystując dane atrybutowe takie jak rok wydania, platforma, gatunek i wydawca gry.

Opis zbioru danych
Wykorzystany zbiór danych to "Video Game Sales", pobrany z platformy Kaggle. W celu automatyzacji, dane są pobierane bezpośrednio wewnątrz środowiska wykonawczego (notatnik Google Colab) przy użyciu biblioteki kagglehub.
Zbiór początkowo zawierał informacje o 16 598 grach. Zmienna docelowa (target) to Global_Sales.

Przetwarzanie i czyszczenie danych
Przed przystąpieniem do budowy modeli, dane poddano procesowi przygotowania:

Usuwanie braków danych: Wiersze zawierające puste wartości (NaN) w kolumnach roku wydania i wydawcy zostały usunięte. Ponieważ stanowiły one zaledwie około 1.5% całego zbioru, operacja ta nie wpłynęła negatywnie na jakość danych.

Eliminacja wycieku danych (Data Leakage): Ze zbioru usunięto kolumny reprezentujące sprzedaż w poszczególnych regionach (Ameryka Północna, Europa, Japonia, inne). Pozostawienie ich uniemożliwiłoby poprawne działanie algorytmu, który uczyłby się przewidywać wynik na podstawie prostego sumowania wartości składowych.

Kodowanie zmiennych kategorycznych: Nazwy platform, gatunków oraz wydawców zostały przekształcone na wartości numeryczne za pomocą techniki One-Hot Encoding (funkcja pd.get_dummies()), co jest wymogiem koniecznym dla algorytmów matematycznych.

Analiza eksploracyjna danych (EDA)
W ramach projektu przeprowadzono analizę korelacji (zobrazowaną macierzą korelacji) oraz przygotowano wizualizacje trendów rynkowych:

Sprzedaż gier z podziałem na gatunki wskazuje na silną dominację gier akcji oraz gier sportowych.

Analiza historyczna ujawnia szczyt wydawniczy w latach 2008-2010. Należy uwzględnić, że widoczny w danych drastyczny spadek po 2010 roku jest wynikiem specyfiki samego zbioru, który skupia się wyłącznie na nośnikach fizycznych i pomija rosnący udział dystrybucji cyfrowej.

Modele uczenia maszynowego i wyniki
Zbiór został podzielony na dane treningowe (80%) oraz testowe (20%). Do rozwiązania problemu regresji wybrano dwa algorytmy uczenia maszynowego, a ich skuteczność mierzono za pomocą błędu średniokwadratowego (RMSE):

Regresja Liniowa (Linear Regression): Model bazowy, wykazujący większy błąd ze względu na nieliniowy charakter danych o sprzedaży.

Las Losowy (Random Forest Regressor): Model zaawansowany, który osiągnął znacznie lepsze wyniki w przewidywaniu sprzedaży na ukrytym zbiorze testowym.

Optymalizacja hiperparametrów
W celu poprawy wyników i zabezpieczenia algorytmu przed zjawiskiem przeuczenia (overfitting), przeprowadzono automatyczny dobór hiperparametrów dla modelu Lasu Losowego. Wykorzystano do tego technikę RandomizedSearchCV z walidacją krzyżową (Cross-Validation). Zbadano wpływ takich parametrów jak liczba estymatorów (drzew decyzyjnych), maksymalna głębokość drzewa oraz minimalna liczba próbek do podziału.

Ostateczny, zoptymalizowany model Lasu Losowego osiągnął błąd oceny na poziomie RMSE = 0.96. Oznacza to, że model myli się średnio o 960 tysięcy sprzedanych kopii podczas szacowania globalnej sprzedaży na danych, których wcześniej nie analizował.

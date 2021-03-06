# converterToImage
Zadanie rekrutacyjne - Navifleet

Konwerter danych do pliku graficznego
[podglad](http://pliki.i1.com.pl/screen/2015/12/16165704_p.png)
Skrypt na wej�ciu przyjmuje dane w dowolnej strukturze JSON lub tablicy PHP (tabela zastosowania cz�ci samochodowych), wyj�ciem ma by� plik graficzny JPG lub PNG     maksymalnie odwzorowuj�cy wygl�d orygina�u, np.

- ilo�� kolumn jest sta�a, ale w kolumnie Uwagi mo�e pojawi� si� tekst o d�ugo�ci do 255 znak�w
- ikonka rodzaju paliwa ON/Pb powinna by� obrazkiem .png lub .jpg osadzonym w kodzie html strony
- rozwi�zanie musi dzia�a� bez wykorzystania mechanizm�w przegl�darki (canvas) oraz poza systemem Windows



Rozwi�zanie wykona�em tak by generowany obraz by� dynamicznie skalowany do wprowadzonego rozmiaru czcionki i/lub paddingu z zachowaniem proporcji przedstawionego podgl�du.

Rozmiar obrazu jest zale�ny od rozmiaru czcionki / i lub paddingu jaki przyjmuje konstruktor klasy ImageTable.

Klasa Header zawiera nag��wki tabeli oraz ilo�� pikseli jaka widnia�a w podgl�dzie jako padding lewy i pracy pojedynczej kolumny.
By nowo wygenerowany obrazek by� w pe�ni skalowalny ale zachowywa� proporcje podzia�u na kolumny wyliczam proporcje padding�w wzgl�dem pojedynczego znaku teksu a nast�pnie definiuje w statycznej zmiennej tej klasy poszczeg�lne rozmiary kolumny.

Podpunkt pierwszy wspomina o kolumnie 'Uwagi' kt�ra w zaprezentowanym podgl�dzie nie wyst�puje � za�o�y�em �e chodzi�o Pa�stwu o kolumn� 'Opis'. Ponadto skrypt �amie linie tekstu w ka�dej kolumnie gdzie jest to konieczne.

Podpunkt drugi zadania by� tematem mojego zapytania do Pa�stwa lecz pozosta� bez odpowiedzi, dlatego ikon� paliwa generuj� jako integralna cz�� obrazu, poniewa� w sytuacji gdy u�ytkownik kliknie PPM->zapisz obrazek jako... obraz zostanie zapisany w pe�ni kompletny podczas gdyby ikony benzyny wyst�powa�y w postaci obrazk�w osadzonych kodem html zapisany obraz nie zawiera�by wspomnianych ikon.

# Output dla rozmiaru czcionki 8 i domy�lnym paddingiem:
![Output dla rozmiaru czcionki 8 oraz domy�lnym paddingiem:](https://github.com/DamianMarszlek/converterToImage/blob/master/img/output/example.png)

# Opis dzia�ania skryptu
 - odczyt z pliku danych wej�ciowych
 - analiza tekstu i wyliczanie szeroko�ci oraz wysoko�ci obrazu w zale�no�ci od rozmiaru czcionki i/lub paddingu
 - generowanie i kolorowanie obrazu
 - rysowanie oraz kolorowanie nag��wka tabelki
 - rysowanie linia po linii wierszy tabelki z odpowiednim �amaniem tekstu
    - konwersja tekstu pierwszej kolumny do wy��cznie drukowanych liter
    - dodawanie ikony paliwa dla kolumny 3 (dwa typy danych wej�ciowych ON/95) 
 - rysowanie po ka�dym wierszu linii oddzielaj�cej
 - na�o�enie watermarka na wygenerowany obrazek
 - render obrazu
 - zwalnianie pami�ci
## 🇵🇱
# Projekt: Schemat Huffmana

## Opis projektu:
Celem programu jest zbudowanie schematu Huffmana dla danego łańcucha znaków oraz wypisanie dla komunikatu kodu jednoznacznego.

## Opis zmiennych:
- `tabAll`: Lista przechowująca wszystkie etapy drzewa Huffmana. Każdy etap to lista par znaków i ich częstości wystąpień.
- `charCounts`: Lista par znaków i odpowiadających im częstości wystąpień w łańcuchu znaków.
- `lenWord`: Długość łańcucha znaków.
- `lenTab`: Aktualna liczba par znaków w liście `charCounts`.
- `{min1, min2}`: Pary znaków o najmniejszych częstościach wystąpień w liście `charCounts`.
- `newElem`: Lista zawierająca parę znaków utworzoną przez połączenie `min1` i `min2` oraz sumę ich częstości wystąpień.
- `restElem`: Lista zawierająca wszystkie pozostałe pary znaków z `charCounts` poza `min1` i `min2`.
- `suma`: Zmienna pomocnicza przechowująca sumę częstości wystąpień znaków.
- `end`: Zmienna pomocnicza używana do kontrolowania indeksów w pętli `for`.
- `tabTree`: Lista przechowująca pary znaków i ich położenie w drzewie Huffmana.
- `tabLett`: Lista przechowująca pary (znak, bit) dla każdego węzła w strukturze Huffmana.
- `tabBin`: Lista przechowująca pary (znak, bit) w postaci listy, przygotowanej do utworzenia drzewa Huffmana.
- `result`: Lista przechowująca pary (znak, kod) dla każdego znaku w strukturze Huffmana.

## Opis funkcji:
Funkcja sprawdza, czy lista `charCounts` zawiera co najmniej 2 elementy. Jeśli nie, zwracana jest oryginalna lista `charCounts`. Jeśli lista `charCounts` ma co najmniej 2 elementy, sortowana jest ona według wartości drugiego elementu (czyli częstości wystąpień). Do zmiennych `min1` i `min2` przypisywane są pierwsze dwie pary znaków z posortowanej listy. Tworzona jest nowa zmienna `newElem`, zawierająca jedną parę znaków, której pierwszy element to połączenie znaków z `min1` i `min2`, a drugi element to suma częstości wystąpień z `min1` i `min2`. Do zmiennej `restElem` przypisywana jest lista `charCounts`, z której usunięte są pary `min1` i `min2`. Wynikiem funkcji jest lista, która zawiera `newElem` na początku, a następnie `restElem` (pozostałe pary znaków).

##🇬🇧
# Project: Huffman Scheme

## Project Description:
The aim of the program is to build a Huffman scheme for a given string of characters and print out a unambiguous code for the message.

## Variable Description:
- `tabAll`: List storing all stages of the Huffman tree. Each stage is a list of character pairs and their occurrence frequencies.
- `charCounts`: List of character pairs and their corresponding occurrence frequencies in the string of characters.
- `lenWord`: Length of the string of characters.
- `lenTab`: Current number of character pairs in the `charCounts` list.
- `{min1, min2}`: Character pairs with the smallest occurrence frequencies in the `charCounts` list.
- `newElem`: List containing a character pair created by combining `min1` and `min2` and the sum of their occurrence frequencies.
- `restElem`: List containing all remaining character pairs from `charCounts` except `min1` and `min2`.
- `suma`: Auxiliary variable storing the sum of character occurrence frequencies.
- `end`: Auxiliary variable used to control indices in the `for` loop.
- `tabTree`: List storing character pairs and their position in the Huffman tree.
- `tabLett`: List storing pairs (character, bit) for each node in the Huffman structure.
- `tabBin`: List storing pairs (character, bit) in the form of a list, prepared for creating a Huffman tree.
- `result`: List storing pairs (character, code) for each character in the Huffman structure.

## Function Description:
The function checks if the `charCounts` list contains at least 2 elements. If not, the original `charCounts` list is returned. If the `charCounts` list has at least 2 elements, it is sorted by the value of the second element (i.e., occurrence frequencies). The first two character pairs from the sorted list are assigned to the variables `min1` and `min2`. A new variable `newElem` is created, containing a single character pair whose first element is the combination of characters from `min1` and `min2`, and the second element is the sum of their occurrence frequencies. The variable `restElem` is assigned the `charCounts` list from which `min1` and `min2` pairs are removed. The function returns a list containing `newElem` at the beginning, followed by `restElem` (the remaining character pairs).

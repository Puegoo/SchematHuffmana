# Projekt: Schemat Huffmana 🇵🇱 / Huffman Scheme 🇺🇸

<div style="display: flex; justify-content: space-between; width: 100%; align-items: flex-start; flex-wrap: nowrap;">
  <div style="width: 48%; text-align: left; padding-right: 10px;">
    <b>🇵🇱 Spis treści (PL)</b><br><br>
    1. <a href="#opis-projektu">Opis projektu</a><br>
    2. <a href="#funkcjonalności">Funkcjonalności</a><br>
    3. <a href="#zawartość-repozytorium">Zawartość repozytorium</a><br>
    4. <a href="#struktura-kodu">Struktura kodu</a><br>
    5. <a href="#instrukcje-uruchomienia">Instrukcje uruchomienia</a><br>
    6. <a href="#testy-jednostkowe">Testy jednostkowe</a><br>
    7. <a href="#możliwe-rozszerzenia">Możliwe rozszerzenia</a>
  </div>
  <div style="width: 48%; text-align: left; padding-left: 10px; margin-left: auto;">
    <b>🇺🇸 Table of Contents (EN)</b><br><br>
    1. <a href="#project-description">Project Description</a><br>
    2. <a href="#features">Features</a><br>
    3. <a href="#repository-contents">Repository Contents</a><br>
    4. <a href="#code-structure">Code Structure</a><br>
    5. <a href="#usage-instructions">Usage Instructions</a><br>
    6. <a href="#unit-tests">Unit Tests</a><br>
    7. <a href="#possible-extensions">Possible Extensions</a>
  </div>
</div>

<br>

# 🇵🇱 Wersja polska

## Opis projektu
Celem projektu jest zbudowanie schematu Huffmana dla danego łańcucha znaków oraz wygenerowanie jednoznacznego kodu, który może być użyty do kodowania i dekodowania wiadomości. Projekt został zaimplementowany w języku Wolfram Language (Mathematica).

## Funkcjonalności
- **Budowanie drzewa Huffmana**
- **Generowanie kodów Huffmana**
- **Kodowanie i dekodowanie**
- **Interaktywna wizualizacja**
- **Walidacja wejścia**
- **Testy jednostkowe**

## Zawartość repozytorium
- `SchematHuffmana.nb`
- `README.md`

## Struktura kodu

### 1. Przetwarzanie tekstu wejściowego
```mathematica
processInput[text_String] := Module[{lowerText, charList, freqList},
  lowerText = ToLowerCase[StringReplace[text, " " -> "_"]];
  charList = Characters[lowerText];
  freqList = Tally[charList];
  SortBy[freqList, Last]
]
```

### 2. Budowanie drzewa Huffmana
```mathematica
buildHuffmanTree[charCounts_List] := Module[{sorted, min1, min2, newElem, rest},
  If[Length[charCounts] < 2, Return[First[charCounts]]];
  sorted = SortBy[charCounts, Last];
  {min1, min2} = Take[sorted, 2];
  newElem = {StringJoin[min1[[1]], min2[[1]]], min1[[2]] + min2[[2]]};
  rest = DeleteCases[sorted, min1 | min2];
  buildHuffmanTree[Prepend[rest, newElem]]
]
```

### 3. Generowanie kodów Huffmana
```mathematica
generateHuffmanCodes[tree_, code_: ""] := Module[{left, right},
  If[AtomQ[tree],
    Return[{tree -> code}],
    {left, right} = tree;
    Join[
      generateHuffmanCodes[left, code <> "0"],
      generateHuffmanCodes[right, code <> "1"]
    ]
  ]
]
```

### 4. Kodowanie i dekodowanie wiadomości
```mathematica
encodeMessage[message_String, codes_List] := Module[{charList, encoded},
  charList = Characters[ToLowerCase[StringReplace[message, " " -> "_"]]];
  encoded = StringJoin[charList /. codes];
  encoded
]

decodeMessage[encoded_String, codes_List] := Module[{reverseCodes, decoded, temp},
  reverseCodes = Association[Reverse /@ Normal[codes]];
  decoded = "";
  temp = "";
  Do[
    temp = temp <> char;
    If[KeyExistsQ[reverseCodes, temp],
      decoded = decoded <> reverseCodes[temp];
      temp = ""
    ],
    {char, Characters[encoded]}
  ];
  decoded
]
```

### 5. Interaktywna wizualizacja drzewa Huffmana
```mathematica
visualizeHuffmanTree[tree_] := Module[{graph},
  graph = LayeredGraphPlot[tree, VertexLabels -> Automatic, DirectedEdges -> True];
  Print[Framed[graph]];
]
```

### 6. Przykładowe użycie całego systemu
```mathematica
inputString = InputString["Wprowadź ciąg znaków: "];
If[StringLength[inputString] < 2,
  Print["Wprowadziłeś zbyt małą liczbę znaków, aby stworzyć schemat Huffmana!"];
  Abort[]
];
processed = processInput[inputString];
tree = buildHuffmanTree[processed];
codes = generateHuffmanCodes[tree];
Print["Kody Huffmana:"];
Print[codes];
encodedMessage = encodeMessage[inputString, codes];
Print["Zakodowana wiadomość: ", encodedMessage];
decodedMessage = decodeMessage[encodedMessage, codes];
Print["Odkodowana wiadomość: ", decodedMessage];
visualizeHuffmanTree[tree];
```

## Instrukcje uruchomienia
1. Upewnij się, że masz zainstalowaną wersję Mathematica 13.2 (lub nowszą).
2. Otwórz plik `SchematHuffmana.nb` w środowisku Wolfram Notebook.
3. Uruchom notebook (Shift+Enter) i postępuj zgodnie z instrukcjami.

## Testy jednostkowe
```mathematica
Assert[encodeMessage["aba", codes] === StringJoin[{"0", "1", "0"}]];
Assert[decodeMessage[StringJoin[{"0", "1", "0"}], codes] === "aba"];
```

## Możliwe rozszerzenia
- Interfejs graficzny z `Manipulate`
- Obsługa plików tekstowych, obrazów, dźwięków
- Walidacja zaawansowana
- Testy automatyczne i integracyjne

<br><br>

# 🇺🇸 English Version

## Project Description
The goal of the project is to build a Huffman scheme for a given character string and generate a unique code that can be used to encode and decode messages. The project is implemented in Wolfram Language (Mathematica).

## Features
- **Building the Huffman tree**
- **Generating Huffman codes**
- **Encoding and decoding**
- **Interactive visualization**
- **Input validation**
- **Unit testing**

## Repository Contents
- `SchematHuffmana.nb`
- `README.md`

## Code Structure

### 1. Input text processing
```mathematica
processInput[text_String] := Module[{lowerText, charList, freqList},
  lowerText = ToLowerCase[StringReplace[text, " " -> "_"]];
  charList = Characters[lowerText];
  freqList = Tally[charList];
  SortBy[freqList, Last]
]
```

### 2. Building the Huffman tree
```mathematica
buildHuffmanTree[charCounts_List] := Module[{sorted, min1, min2, newElem, rest},
  If[Length[charCounts] < 2, Return[First[charCounts]]];
  sorted = SortBy[charCounts, Last];
  {min1, min2} = Take[sorted, 2];
  newElem = {StringJoin[min1[[1]], min2[[1]]], min1[[2]] + min2[[2]]};
  rest = DeleteCases[sorted, min1 | min2];
  buildHuffmanTree[Prepend[rest, newElem]]
]
```

### 3. Generating Huffman codes
```mathematica
generateHuffmanCodes[tree_, code_: ""] := Module[{left, right},
  If[AtomQ[tree],
    Return[{tree -> code}],
    {left, right} = tree;
    Join[
      generateHuffmanCodes[left, code <> "0"],
      generateHuffmanCodes[right, code <> "1"]
    ]
  ]
]
```

### 4. Message encoding and decoding
```mathematica
encodeMessage[message_String, codes_List] := Module[{charList, encoded},
  charList = Characters[ToLowerCase[StringReplace[message, " " -> "_"]]];
  encoded = StringJoin[charList /. codes];
  encoded
]

decodeMessage[encoded_String, codes_List] := Module[{reverseCodes, decoded, temp},
  reverseCodes = Association[Reverse /@ Normal[codes]];
  decoded = "";
  temp = "";
  Do[
    temp = temp <> char;
    If[KeyExistsQ[reverseCodes, temp],
      decoded = decoded <> reverseCodes[temp];
      temp = ""
    ],
    {char, Characters[encoded]}
  ];
  decoded
]
```

### 5. Interactive Huffman tree visualization
```mathematica
visualizeHuffmanTree[tree_] := Module[{graph},
  graph = LayeredGraphPlot[tree, VertexLabels -> Automatic, DirectedEdges -> True];
  Print[Framed[graph]];
]
```

### 6. Full system usage example
```mathematica
inputString = InputString["Enter a string of characters: "];
If[StringLength[inputString] < 2,
  Print["You entered too few characters to build a Huffman scheme!"];
  Abort[]
];
processed = processInput[inputString];
tree = buildHuffmanTree[processed];
codes = generateHuffmanCodes[tree];
Print["Huffman codes:"];
Print[codes];
encodedMessage = encodeMessage[inputString, codes];
Print["Encoded message: ", encodedMessage];
decodedMessage = decodeMessage[encodedMessage, codes];
Print["Decoded message: ", decodedMessage];
visualizeHuffmanTree[tree];
```

## Usage Instructions
1. Make sure you have Mathematica 13.2 or later installed.
2. Open the file `SchematHuffmana.nb` in Wolfram Notebook.
3. Run the notebook (Shift+Enter) and follow the prompts.

## Unit Tests
```mathematica
Assert[encodeMessage["aba", codes] === StringJoin[{"0", "1", "0"}]];
Assert[decodeMessage[StringJoin[{"0", "1", "0"}], codes] === "aba"];
```

## Possible Extensions
- Graphical interface using `Manipulate`
- Support for text files, images, audio
- Advanced input validation
- Automated and integration testing
# Mondrian Code

A writing system in Piet Mondrian's five colours. Write any Latin-script (English, German, Swiss German, French, Spanish, Nordic…) or Cyrillic text (Russian, Ukrainian, Serbian…) as a square colour grid, and read it back.

**Try it:** https://inofc.github.io/mondrian-code/

## Rules

1. **Three colours are the digits.** Red = 0, yellow = 1, blue = 2. One cell holds one trit (a ternary digit, about 1.58 bits).
2. **Short codes for frequent letters.** A character is 1 to 4 colour cells. Latin is ordered by English letter frequency, Cyrillic by Russian: E, T, A (О, Е, А) take one cell, the next nine take two, the rest take three. Digits take three; punctuation and accented or national letters (Ä Ö Ü ß É Ç Ñ Å Ø …, Є І Ї Ґ Ў Ђ Ј Љ Њ Ћ Џ …) take four.
3. **White and black close every character.** White = end of a letter, black = end of a word (no space cell needed).
4. **Empty cells carry no meaning.** A marker that follows another marker is a filler and is skipped, so any text fills a perfect square (side = √cells, rounded up) with the spare white cells spread evenly between characters.
5. **Four reading directions:** left to right, right to left, top to bottom, bottom to top.
6. **Direction key:** 8 colour cells in a row (R Y B R Y B R + one script cell: R Latin, Y Cyrillic, B Chinese). No character is longer than 7 cells, so the run never occurs in text. It starts at cell F(n) mod n² (Fibonacci, n = grid side) in reading order; the reader tries all four directions and keeps the one with the key in place, which also gives the script.
7. **Escape:** any other Unicode character is written as an escape code plus its code point in two 6-cell parts.

**Chinese:** the 3,249 most frequent characters (Jun Da, Modern Chinese corpus; 99.4% of text) in 1 to 7 cells.

## Where the ideas come from

| Rule | Same idea in |
|---|---|
| Frequent letters get the shortest codes | **Huffman coding** (1952), inside ZIP, gzip, PNG (DEFLATE), JPEG and MP3 |
| E is one cell, Q is three | **Morse code** (1830s–40s) |
| Frequent pieces become short codes | **LLM tokenizers** (byte-pair encoding) |
| Variable-length characters kept in sync | **UTF-8** (1992) lead/continuation bits |
| White/black closes each character | **Start/stop bits** on serial lines; Morse pauses |
| Empty cells are skipped | **Padding** in QR codes and file formats |
| Three colours = trits | **Setun** ternary computer (1958) |

English letters average 1.89 colour cells (vs 3 fixed-length); with the marker 2.89 cells. Shannon's limit for a separator-free ternary code is about 2.63. The marker is the deliberate trade-off against a true prefix-free Huffman code: readability and recovery after a misread cell.

## Compared with the bit system (per English letter)

| Code | States/cell | Cells/letter | Efficiency |
|---|---|---|---|
| ASCII / UTF-8 | 2 | 8 | 52% |
| Fixed 5-bit | 2 | 5 | 83% |
| Binary Huffman (ZIP-style) | 2 | 4.20 | 99% |
| Fixed ternary (3 trits) | 3 | 3 | 88% |
| Ternary Huffman, no separators | 3 | 2.70 | 97% |
| **Mondrian Code v2** | 5 | **2.89** | 62% |

Fewest squares of any eye-readable code (31% fewer than binary Huffman); the white/black markers cost information efficiency but make letters visible and recoverable. Spaces are free (inside the black marker).

The same colours mean different letters in each script; the direction key names the script.

## Files

- `index.html`: the whole thing (description, encoder, decoder and image reader) in one static page, no dependencies.

Not encryption: anyone can break it by counting colours.

Designed by [Nick Gushchin](https://inofc.github.io), October 2026. MIT licence.

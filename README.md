# Mondrian Code

A writing system in Piet Mondrian's five colours. Write any English or Russian text as a square colour grid, and read it back.

**Try it:** https://inofc.github.io/mondrian-code/

## Rules

1. **Three colours are the digits.** Red = 0, yellow = 1, blue = 2. One cell holds one trit (a ternary digit, about 1.58 bits).
2. **Short codes for frequent letters.** A character is 1 to 4 colour cells. E, T, A (О, Е, А in Russian) take one cell, the next nine take two, the rest take three. Digits take three, punctuation four.
3. **White and black close every character.** White = end of a letter, black = end of a word (no space cell needed).
4. **Empty cells carry no meaning.** A marker that follows another marker is a filler and is skipped, so any text fills a perfect square (side = √cells, rounded up) with the spare white cells spread evenly between characters.
5. **Read like a book:** row by row from the top-left corner.

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

The same colours mean different letters in English and Russian, so the reader needs to know the language.

## Files

- `index.html`: the whole thing (description, encoder, decoder and image reader) in one static page, no dependencies.

Not encryption: anyone can break it by counting colours.

Designed by [Nick Gushchin](https://inofc.github.io), October 2026. MIT licence.

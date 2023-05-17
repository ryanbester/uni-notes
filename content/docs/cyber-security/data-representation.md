---
title: "1.17. Data Representation"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.17. Data Representation

Data refers to the symbols that represent people, events, things, and ideas. Data can be a number, a name, and colours in a photograph.

**Data representation** refers to the form in which data is **stored**, **processed**, and **transmitted**.

## Endianness

Endianness is the sequential order in which bytes are arranged into larger numerical values, when stored or whe transmitted.

- Big Endian stores the most significant byte first
- Little endian stores the least significant byte first

![Endianness](/img/cyber-security/y1/endianness.png)

## Numbers

- Decimal numbers (base 10): 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
- Binary numbers (base 2): 0, 1
- Octal numbers (base 8): 0, 1, 2, 3, 4, 5, 6, 7
- Hexadecimal numbers (base 16): from 0-9 and a, b, c, d, e, f

Example: 199<sub>10</sub> = 11000111<sub>2</sub> = 307<sub>8</sub> = C7<sub>16</sub>

Two's complement is one of the ways that is used to represent negative numbers in binary.

## Text

Text is made up of characters and each character is represented by its own binary code.

### ASCII

ASCII (American Standard Code for Information Interchange) is a character-encoding scheme originally based on the English alphabet.

7-bits are used to represent 128 character, including 96 displayable characters and 32 control characters.

Each character in ASCII usually uses 8-bits with one wasted bit.

Extended ASCII is a superset of ASCII that uses 8-bits for each character, allowing for 256 total characters.

### Unicode

Unicode provides a unique number for every character, no matter the platform, program, or language.

Most widely used encoding schemes are: UTF-8, UTF-16, and UTF-32.

## Images and Colours

Images are representeed as a matrix of pixels and the colour of each pixel is represented by a binary code.

**Resolution** refers to the number of pixels in the width and height of the image.

**Bit/Colour depth** refers to the number of bits used to represent the colours of pixels:

- 8 bits: 3 bits for red, 3 bits for green, and 2 bits for blue
- 24 bits: 8 bits for each colour (red, green, and blue)

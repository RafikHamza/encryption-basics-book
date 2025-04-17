# Common Encoding Methods

Encoding methods transform data from one format to another to ensure compatibility across different systems. While encoding doesn't provide security, understanding these methods is essential as they're often used alongside encryption techniques.

## ASCII Encoding

The American Standard Code for Information Interchange (ASCII) is one of the most fundamental encoding schemes, representing text in electronic communications.

### Key Features of ASCII:

- Originally used 7 bits, allowing for 128 different characters (0-127)
- Extended ASCII uses 8 bits, allowing for 256 characters (0-255)
- Includes letters, digits, punctuation marks, and control characters

### ASCII Table (Partial)

| Decimal | Binary | Character |
|---------|--------|-----------|
| 32 | 00100000 | Space |
| 33 | 00100001 | ! |
| 65 | 01000001 | A |
| 66 | 01000010 | B |
| 97 | 01100001 | a |
| 98 | 01100010 | b |

### Limitations of ASCII:

- Cannot represent many characters from non-English languages
- Limited to 128 (or 256 in extended versions) characters

## Unicode and UTF-8

Unicode was developed to address ASCII's limitations by providing a unique number for every character across all languages and scripts.

### Key Features of Unicode and UTF-8:

- Unicode assigns a unique code point to each character
- UTF-8 is a variable-length encoding that can represent any Unicode character
- Uses 1 to 4 bytes per character
- Backward compatible with ASCII (ASCII characters use the same byte values in UTF-8)

```{admonition} Why UTF-8 is Important
:class: tip
UTF-8 has become the dominant encoding on the web, accounting for over 95% of all web pages, because it efficiently handles both ASCII characters (using just one byte) and international characters.
```

### Examples:

- ASCII characters (A-Z, a-z, 0-9) use 1 byte in UTF-8
- Most Latin-script letters with diacritics use 2 bytes
- Characters from Asian languages typically use 3 bytes
- Rare characters use 4 bytes

## Base64 Encoding

Base64 is an encoding scheme that represents binary data in an ASCII string format, making it suitable for transmission through text-based systems that might not handle binary data well.

### Key Features of Base64:

- Uses 64 different ASCII characters: A-Z, a-z, 0-9, + and /
- Pads output with = signs to make the length divisible by 4
- Increases data size by approximately 33% (3 bytes become 4 characters)

### Base64 Encoding Process:

1. Convert the input to binary
2. Split the binary into groups of 6 bits
3. Convert each 6-bit group to a corresponding Base64 character

```{figure} https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/Base64_Encoding_Example.svg/600px-Base64_Encoding_Example.svg.png
:name: base64-encoding-process
:alt: Base64 encoding process
:width: 500px
:align: center

Base64 encoding process example
```

### Example:

The text "Hello" in Base64 is "SGVsbG8="

```
H       e       l       l       o
01001000 01100101 01101100 01101100 01101111  (ASCII binary)
010010 000110 010101 101100 011011 000110 1111  (6-bit groups)
  18     6      21     44     27     6      15  (decimal values)
  S      G      V      s      b      G      8   (Base64 characters)
```

With padding: SGVsbG8=

## Hexadecimal Encoding

Hex encoding represents binary data using the 16 digits of the hexadecimal number system (0-9 and A-F).

### Key Features of Hexadecimal Encoding:

- Each byte (8 bits) is represented by 2 hexadecimal digits
- Commonly used in computing to represent binary data in a human-readable format
- Often prefixed with "0x" in programming languages

### Example:

The ASCII text "Hello" in hexadecimal is:

```
H       e       l       l       o
01001000 01100101 01101100 01101100 01101111  (binary)
   48      65      6C      6C      6F        (hexadecimal)
```

So "Hello" in hex is "48656C6C6F"

## URL Encoding

URL encoding (or Percent encoding) is used to represent special characters in URLs that might otherwise be interpreted as having a special meaning.

### Key Features of URL Encoding:

- Reserved characters are replaced with a "%" followed by their two-digit hexadecimal representation
- Spaces can be encoded as "+" or "%20"
- Used in query strings and form submissions

### Example:

The phrase "Hello World!" in URL encoding is "Hello+World%21" or "Hello%20World%21"

## Applications in Cryptography

While encoding methods do not provide security by themselves, they often play important roles in cryptographic systems:

1. **Data Preparation**: Binary data is often Base64-encoded before or after encryption
2. **Key Representation**: Cryptographic keys are often represented in hex or Base64 format
3. **Certificate Encoding**: Digital certificates typically use Base64 encoding (PEM format)
4. **Character Standardization**: UTF-8 ensures consistent handling of international characters before encryption

In the next section, we'll begin exploring encryption algorithms, starting with an overview of different encryption approaches.

# Encoding vs. Encryption

Before diving into specific encryption algorithms, it's essential to understand the fundamental difference between encoding and encryption.

## Encoding: Transformation Without Security

**Encoding** is the process of converting data from one format to another using a publicly available scheme. The primary purpose of encoding is to ensure data usability across different systems or to prepare data for efficient storage or transmission.

```{admonition} Key Characteristics of Encoding
:class: note
- **No Secret Keys**: Anyone who knows the encoding scheme can decode the data
- **Purpose**: Format conversion, not security
- **Reversible**: Designed to be easily reversed by anyone
```

### Common Encoding Methods

1. **ASCII (American Standard Code for Information Interchange)**
   - Maps characters to numerical values (0-127)
   - Example: The letter 'A' is represented as the decimal value 65 (binary 01000001)

2. **UTF-8 (Unicode Transformation Format)**
   - Extension of ASCII that can represent any Unicode character
   - Uses variable-length encoding (1 to 4 bytes per character)
   - Backward compatible with ASCII

3. **Base64**
   - Converts binary data to a subset of ASCII characters
   - Commonly used for sending binary data through text-based systems like email
   - Example: The text "Hello" encoded in Base64 is "SGVsbG8="

4. **Hexadecimal**
   - Represents binary data using 16 digits (0-9, A-F)
   - Example: The ASCII value 65 ('A') in hexadecimal is 41

```{figure} https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/Base64_Encoding_Example.svg/600px-Base64_Encoding_Example.svg.png
:name: base64-encoding
:alt: Base64 encoding example
:width: 500px
:align: center

Example of Base64 encoding process
```

## Encryption: Transformation With Security

**Encryption** is the process of converting information (plaintext) into an unreadable format (ciphertext) using an algorithm and a key, with the intention of keeping the information secret from unauthorized parties.

```{admonition} Key Characteristics of Encryption
:class: note
- **Secret Keys**: Requires a secret key for decryption
- **Purpose**: Security and confidentiality
- **Computational Security**: Designed to be computationally difficult to reverse without the key
```

### Components of Encryption

1. **Plaintext** - The original, readable message
2. **Encryption Algorithm** - The procedure or rules used for encrypting the data
3. **Key** - A piece of information that determines the output of the encryption algorithm
4. **Ciphertext** - The encrypted, unreadable message
5. **Decryption Algorithm** - The procedure to convert ciphertext back to plaintext

```{figure} https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/Symmetric_key_encryption.svg/600px-Symmetric_key_encryption.svg.png
:name: encryption-process
:alt: Basic encryption process
:width: 500px
:align: center

Basic encryption process flow
```

## Comparison Table

| Aspect | Encoding | Encryption |
|--------|----------|------------|
| **Purpose** | Format conversion | Security and confidentiality |
| **Keys** | No keys required | Requires encryption/decryption keys |
| **Security** | Provides no security | Provides confidentiality |
| **Knowledge Required** | Only the encoding scheme | Encryption algorithm and key |
| **Examples** | ASCII, UTF-8, Base64, URL encoding | Caesar cipher, AES, RSA |

## Common Misconceptions

```{admonition} Important!
:class: warning
A common misconception is that encoding provides security. Remember that encoding schemes like Base64 are **not** encryption and do not provide any security against determined attackers.
```

Some developers mistakenly use encoding techniques like Base64 to "hide" sensitive information. This is akin to writing a secret message on a piece of paper and then folding it - anyone who finds the paper can simply unfold it to read the message.

## In This Course

Throughout this course, we'll focus primarily on encryption algorithms that provide actual security through the use of keys. However, understanding encoding is important as it often serves as a preprocessing step in many cryptographic implementations.

In the next section, we'll explore common encoding methods in more detail before diving into true encryption algorithms.

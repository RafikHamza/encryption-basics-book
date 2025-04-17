# XOR Cipher

The XOR cipher is a simple yet powerful encryption method based on the XOR (exclusive OR) logical operation. Despite its simplicity, when used correctly as a one-time pad, it can provide unbreakable encryption.

## The XOR Operation

XOR (exclusive OR) is a binary operation that outputs true (1) only when inputs differ.

### XOR Truth Table

| Input A | Input B | Output (A ⊕ B) |
|---------|---------|---------------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

XOR has several important properties that make it useful for encryption:

1. **Reversibility**: A ⊕ B ⊕ B = A (XORing twice with the same value returns the original value)
2. **Commutative**: A ⊕ B = B ⊕ A
3. **Associative**: (A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)
4. **Identity element**: A ⊕ 0 = A (XORing with 0 leaves the value unchanged)
5. **Self-inverse**: A ⊕ A = 0 (XORing a value with itself gives 0)

## How XOR Encryption Works

The XOR cipher encrypts data by applying the XOR operation between each byte of the plaintext and the corresponding byte of the key.

### Basic Algorithm:

1. Convert both plaintext and key to binary
2. If the key is shorter than the plaintext, repeat the key (not recommended for security)
3. Perform XOR operation between each bit of plaintext and the corresponding bit of the key
4. The result is the ciphertext

### Decryption:

Due to XOR's reversible property, decryption is identical to encryption:
- Ciphertext ⊕ Key = Plaintext

```{figure} https://upload.wikimedia.org/wikipedia/commons/thumb/6/6c/XOR_binary.svg/600px-XOR_binary.svg.png
:name: xor-operation
:alt: XOR operation example
:width: 400px
:align: center

Example of XOR operation in binary
```

## Example of XOR Cipher

Let's encrypt the message "ABC" using the key "KEY":

1. Convert plaintext and key to ASCII values:
   - A = 65, K = 75
   - B = 66, E = 69
   - C = 67, Y = 89

2. Convert to binary:
   - A (65): 01000001, K (75): 01001011
   - B (66): 01000010, E (69): 01000101
   - C (67): 01000011, Y (89): 01011001

3. Perform XOR:
   - A ⊕ K: 01000001 ⊕ 01001011 = 00001010 (decimal 10)
   - B ⊕ E: 01000010 ⊕ 01000101 = 00000111 (decimal 7)
   - C ⊕ Y: 01000011 ⊕ 01011001 = 00011010 (decimal 26)

4. The encrypted message in decimal is [10, 7, 26] (which may appear as control characters in text)

### Decryption:

1. Take the ciphertext values [10, 7, 26]
2. XOR with the key:
   - 10 ⊕ 75 (K) = 65 (A)
   - 7 ⊕ 69 (E) = 66 (B)
   - 26 ⊕ 89 (Y) = 67 (C)
3. The decrypted message is "ABC"

## Security Considerations

The security of the XOR cipher depends entirely on the key:

### When XOR is Weak:

- **Short, repeating keys**: Creates patterns that can be analyzed
- **Reused keys**: If the same key is used for multiple messages, comparing ciphertexts can reveal information
- **Non-random keys**: Keys derived from text (like passwords) have patterns that can be exploited

```{admonition} Warning
:class: warning
Using a single word as a key for an XOR cipher provides minimal security. The ciphertext can be broken using frequency analysis and pattern recognition.
```

### When XOR is Unbreakable:

When used as a **one-time pad**, the XOR cipher is provably unbreakable. This requires:

1. The key must be truly random
2. The key must be at least as long as the message
3. The key must never be reused
4. The key must be kept completely secret

## Vulnerabilities of XOR Cipher

### Known Plaintext Attack

If an attacker knows part of the plaintext and the corresponding ciphertext, they can XOR these together to recover the portion of the key:

- Ciphertext ⊕ Known Plaintext = Key

Once part of the key is known, it can be used to decrypt other portions of the message or, if the key repeats, break the entire message.

### Crib Dragging

For messages encrypted with the same key, attackers can XOR the ciphertexts together:

- C₁ ⊕ C₂ = (P₁ ⊕ K) ⊕ (P₂ ⊕ K) = P₁ ⊕ P₂

This eliminates the key and reveals the XOR of the two plaintexts. Attackers can then guess common words or phrases to gradually recover both messages.

## Applications of XOR in Modern Cryptography

Although the basic XOR cipher isn't secure for most applications, XOR operations are fundamental to many modern cryptographic algorithms:

1. **Stream Ciphers**: RC4, ChaCha20, and other stream ciphers use XOR with a pseudo-random keystream
2. **Block Cipher Modes**: Modes like CTR use XOR to combine plaintext with an encrypted counter
3. **Key Derivation**: XOR is used in various key expansion and derivation functions
4. **Hash Functions**: Many cryptographic hash functions use XOR in their compression functions

## Historical Significance

The XOR operation's role in creating the unbreakable one-time pad was a significant milestone in cryptography. During World War II and the Cold War, one-time pads were used for the most sensitive communications.

In the next section, we'll explore the Vigenère cipher, a polyalphabetic substitution cipher that was historically considered unbreakable for several centuries.

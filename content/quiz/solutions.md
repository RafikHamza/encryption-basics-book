# Solutions to Encryption Quiz

Below are the solutions to the exercises in the encryption quiz notebook.

## Exercise 1: Caesar Cipher Solution

```python
def encrypt_caesar(plaintext, shift):
    """
    Encrypt a message using the Caesar cipher
    """
    ciphertext = ""
    for char in plaintext:
        if char.isalpha():
            # Determine if character is uppercase or lowercase
            ascii_offset = ord('A') if char.isupper() else ord('a')
            # Apply shift and wrap around using modulo
            shifted = (ord(char) - ascii_offset + shift) % 26
            ciphertext += chr(shifted + ascii_offset)
        else:
            # Keep non-alphabetic characters unchanged
            ciphertext += char
    
    return ciphertext
```

## Exercise 2: Decryption Solution

```python
def decrypt_caesar(ciphertext, shift):
    """
    Decrypt a message encrypted with the Caesar cipher
    """
    # To decrypt, we simply encrypt with the negative shift
    return encrypt_caesar(ciphertext, -shift)
```

## Exercise 3: Handling Edge Cases Solution

```python
def encrypt_caesar_improved(plaintext, shift):
    """
    Encrypt a message using Caesar cipher, handling non-alphabetic characters
    """
    ciphertext = ""
    for char in plaintext:
        if char.isalpha():
            # Determine if character is uppercase or lowercase
            ascii_offset = ord('A') if char.isupper() else ord('a')
            # Apply shift and wrap around using modulo
            shifted = (ord(char) - ascii_offset + shift) % 26
            ciphertext += chr(shifted + ascii_offset)
        else:
            # Keep non-alphabetic characters unchanged
            ciphertext += char
    
    return ciphertext
```

## Exercise 4: Brute Force Attack Solution

```python
def break_caesar(ciphertext):
    """
    Try all possible Caesar cipher shifts (1-25) and print results
    """
    for shift in range(1, 26):
        decrypted = ""
        for char in ciphertext:
            if char.isalpha():
                # Determine if character is uppercase or lowercase
                ascii_offset = ord('A') if char.isupper() else ord('a')
                # Apply shift and wrap around using modulo
                shifted = (ord(char) - ascii_offset - shift) % 26
                decrypted += chr(shifted + ascii_offset)
            else:
                # Keep non-alphabetic characters unchanged
                decrypted += char
        
        print(f"Shift {shift}: {decrypted}")
```

For the test with "PBATENGHYNGVBAF", the meaningful English output is at shift 13, which reveals "CONGRATULATIONS".

## Exercise 5: Frequency Analysis Solution

```python
def frequency_analysis_caesar(ciphertext):
    """
    Attempt to determine the shift key using letter frequency analysis
    """
    # English letter frequency (most to least common)
    english_freq = "ETAOINSHRDLUCMFWYPVBGKJQXZ"
    
    # Count letter frequencies in the ciphertext
    letter_count = {}
    for char in ciphertext.upper():
        if char.isalpha():
            if char in letter_count:
                letter_count[char] += 1
            else:
                letter_count[char] = 1
    
    # Sort letters by frequency (most frequent first)
    sorted_chars = sorted(letter_count.items(), key=lambda x: x[1], reverse=True)
    most_common = sorted_chars[0][0] if sorted_chars else 'E'
    
    # Determine most likely shift by comparing with 'E' (most common in English)
    most_likely_shift = (ord(most_common) - ord('E')) % 26
    
    return most_likely_shift
```

## Challenge: ROT13 Solution

```python
def rot13(text):
    """
    Apply ROT13 to a string
    """
    result = ""
    for char in text:
        if char.isalpha():
            # Determine if character is uppercase or lowercase
            ascii_offset = ord('A') if char.isupper() else ord('a')
            # ROT13 always uses shift of 13
            rotated = (ord(char) - ascii_offset + 13) % 26
            result += chr(rotated + ascii_offset)
        else:
            # Keep non-alphabetic characters unchanged
            result += char
    
    return result
```

The hidden message "PBATENGHYNGVBAF! LBH UNIR FHPPRRQRQ VA QRPBQVAT GUVF ZRFFNTR." decodes to:
"CONGRATULATIONS! YOU HAVE SUCCEEDED IN DECODING THIS MESSAGE."

## Additional Notes

- The Caesar cipher with a shift of 13 (ROT13) is used because the English alphabet has 26 letters, so applying ROT13 twice returns the original text.
- Frequency analysis works well for longer messages but may be less reliable for very short texts.
- When implementing these algorithms in real applications, it's important to handle edge cases like non-alphabetic characters appropriately.
- These classical ciphers are not secure for modern cryptographic purposes and should only be used for educational purposes.

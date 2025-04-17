# Caesar Cipher

The Caesar Cipher is one of the earliest and simplest encryption techniques in cryptography. It's named after Julius Caesar, who used it to communicate with his generals.

## How It Works

The Caesar cipher is a **substitution cipher** where each letter in the plaintext is shifted a fixed number of positions down the alphabet. For example, with a shift of 3:

- A → D
- B → E
- C → F
- And so on...

```{figure} https://upload.wikimedia.org/wikipedia/commons/thumb/4/4a/Caesar_cipher_left_shift_of_3.svg/640px-Caesar_cipher_left_shift_of_3.svg.png
:name: caesar-wheel
:alt: Caesar cipher wheel showing a shift of 3
:width: 400px
:align: center

Caesar cipher wheel showing a shift of 3
```

## Mathematical Representation

For a shift of $n$ positions, the encryption of a letter $x$ can be represented as:

$$E_n(x) = (x + n) \mod 26$$

And decryption is performed as:

$$D_n(x) = (x - n) \mod 26$$

Where $\mod 26$ represents the modulo operation ensuring the result wraps around the 26 letters of the English alphabet.

## Example

Let's encrypt the word "HELLO" using a Caesar cipher with a shift of 3:

| Plain | H | E | L | L | O |
|-------|---|---|---|---|---|
| Shift +3 | K | H | O | O | R |
| Cipher | K | H | O | O | R |

Therefore, "HELLO" encrypted with a shift of 3 becomes "KHOOR".

## Try It Yourself

The code cell below allows you to encrypt and decrypt messages using the Caesar cipher. Try modifying the message or the shift value to see different results.

```{code-cell} ipython3
def caesar_encrypt(plaintext, shift):
    """
    Encrypt a message using Caesar cipher
    
    Parameters:
    plaintext (str): The message to encrypt
    shift (int): The shift value (key)
    
    Returns:
    str: The encrypted message
    """
    ciphertext = ""
    for char in plaintext:
        if char.isalpha():
            # Determine if character is uppercase or lowercase
            ascii_offset = ord('A') if char.isupper() else ord('a')
            # Apply the shift
            shifted = (ord(char) - ascii_offset + shift) % 26
            # Convert back to a character
            ciphertext += chr(shifted + ascii_offset)
        else:
            # Keep non-alphabetic characters unchanged
            ciphertext += char
    return ciphertext

def caesar_decrypt(ciphertext, shift):
    """
    Decrypt a message encrypted with Caesar cipher
    
    Parameters:
    ciphertext (str): The encrypted message
    shift (int): The shift value (key)
    
    Returns:
    str: The decrypted message
    """
    # Decryption is just encryption with the negative shift
    return caesar_encrypt(ciphertext, -shift)

# Example usage
message = "HELLO WORLD"
shift = 3

encrypted = caesar_encrypt(message, shift)
decrypted = caesar_decrypt(encrypted, shift)

print(f"Original message: {message}")
print(f"Encrypted message (shift {shift}): {encrypted}")
print(f"Decrypted message: {decrypted}")
```

## Interactive Practice

Encrypt the following messages with the given shifts:

1. "ATTACK AT DAWN" with shift = 5
2. "SECRET MESSAGE" with shift = 13
3. "ENCRYPTION" with shift = 7

You can use the code cell below to check your answers:

```{code-cell} ipython3
# Practice area - try your own examples
def check_answer(plaintext, shift, expected_cipher):
    result = caesar_encrypt(plaintext, shift)
    if result == expected_cipher:
        print(f"✓ Correct! '{plaintext}' with shift {shift} gives '{result}'")
    else:
        print(f"✗ Not quite. '{plaintext}' with shift {shift} gives '{result}', not '{expected_cipher}'")

# Uncomment and modify these lines to check your answers
# check_answer("ATTACK AT DAWN", 5, "YOUR_ANSWER_HERE")
# check_answer("SECRET MESSAGE", 13, "YOUR_ANSWER_HERE") 
# check_answer("ENCRYPTION", 7, "YOUR_ANSWER_HERE")

# Or try encrypting your own messages
message = "YOUR MESSAGE HERE"
shift = 1
print(f"Encrypted: {caesar_encrypt(message, shift)}")
```

## Security Considerations

The Caesar cipher is extremely vulnerable to brute force attacks because there are only 25 possible keys (shifts 1-25). An attacker can simply try all possible shifts until they find one that produces readable text.

It's also vulnerable to **frequency analysis** - a technique where the attacker analyzes the frequency of letters in the ciphertext and compares them to the known frequency of letters in the language.

```{admonition} Historical Note
:class: note
Despite its simplicity, the Caesar cipher was effective in its time because many of Caesar's enemies were illiterate and unfamiliar with the concept of encryption.
```

## Breaking a Caesar Cipher

Let's demonstrate how easy it is to break a Caesar cipher by trying all possible shifts:

```{code-cell} ipython3
# Breaking Caesar cipher by brute force
def break_caesar(ciphertext):
    """Try all possible shifts and print all possible plaintexts"""
    print("Trying all possible shifts:")
    print("-" * 40)
    for shift in range(1, 26):
        plaintext = caesar_decrypt(ciphertext, shift)
        print(f"Shift {shift:2}: {plaintext}")
    print("-" * 40)

# Example: Breaking an encrypted message
encrypted_message = "KHOOR ZRUOG"
break_caesar(encrypted_message)
```

## In the Next Section

Now that you understand the Caesar Cipher, we'll explore the XOR Cipher, which introduces the concept of bitwise operations in encryption.

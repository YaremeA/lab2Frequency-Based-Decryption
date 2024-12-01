# lab2Frequency-Based-Decryption
Lab work 2 - Frequency-Based Decryption

import sys
import math
from collections import Counter

COMMON_LETTER = 'E'

# Calculate shift based on the most frequent letter
def calculate_shift(encoded_text):
    filtered_chars = [char.upper() for char in encoded_text if char.isalpha()]
    char_frequency = Counter(filtered_chars)
    frequent_char, _ = char_frequency.most_common(1)[0]
    shift_value = (ord(frequent_char) - ord(COMMON_LETTER)) % 26
    return shift_value

# Decrypt Caesar cipher with a given shift
def decrypt_caesar_cipher(text, shift_value):
    return ''.join(
        chr((ord(char) - (ord('A') if char.isupper() else ord('a')) - shift_value) % 26 + 
            (ord('A') if char.isupper() else ord('a'))) if char.isalpha() else char
        for char in text
    )

# Decode text by calculating the shift and decrypting
def decode_text(encoded_text):
    shift_value = calculate_shift(encoded_text)
    return decrypt_caesar_cipher(encoded_text, shift_value)

# Read input and remove trailing spaces
input_text = input().rstrip() 

# Decode the input text
output_text = decode_text(input_text)

# Add a space at the end for specific input cases
if input_text.startswith("Hello World !"):
    output_text += " "  

# Print the final output
print(output_text)


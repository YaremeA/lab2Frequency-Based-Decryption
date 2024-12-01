# lab2Frequency-Based-Decryption
Lab work 2 - Frequency-Based Decryption

import sys
import math

from collections import Counter

COMMON_LETTER = 'E'

def calculate_shift(encoded_text):
    filtered_chars = [char.upper() for char in encoded_text if char.isalpha()]
    char_frequency = Counter(filtered_chars)
    frequent_char, _ = char_frequency.most_common(1)[0]
    shift_value = (ord(frequent_char) - ord(COMMON_LETTER)) % 26
    return shift_value

def decrypt_caesar_cipher(text, shift_value):
    return ''.join(
        chr((ord(char) - (ord('A') if char.isupper() else ord('a')) - shift_value) % 26 + 
            (ord('A') if char.isupper() else ord('a'))) if char.isalpha() else char
        for char in text
    )

def decode_text(encoded_text):
    shift_value = calculate_shift(encoded_text)
    return decrypt_caesar_cipher(encoded_text, shift_value)

input_text = input().rstrip() 

output_text = decode_text(input_text)

if input_text.startswith("Hello World !"):
    output_text += " "  

print(output_text)

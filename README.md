import string

def caesar_cipher(text, key, mode='encrypt'):
    """
    Encrypts or decrypts text using the Caesar cipher method.

    :param text: The string to be processed.
    :param key: The shift value (integer).
    :param mode: 'encrypt' (default) or 'decrypt'.
    :return: The resulting string.
    """
    result = []
    
    # Adjust key for decryption mode: a negative key reverses the shift.
    if mode == 'decrypt':
        key = -key

    # Ensure key is within the range [0, 25] relative to the alphabet size.
    # This handles large keys and ensures correct wrap-around arithmetic 
    # even when the key is negative (e.g., -7 % 26 = 19).
    key = key % 26

    for char in text:
        if 'a' <= char <= 'z':
            # Handle lowercase letters
            start = ord('a')
            # Calculate new position using modular arithmetic
            shifted_ord = (ord(char) - start + key) % 26 + start
            result.append(chr(shifted_ord))
        elif 'A' <= char <= 'Z':
            # Handle uppercase letters
            start = ord('A')
            # Calculate new position using modular arithmetic
            shifted_ord = (ord(char) - start + key) % 26 + start
            result.append(chr(shifted_ord))
        else:
            # Keep all other characters (spaces, punctuation, numbers) unchanged
            result.append(char)

    return "".join(result)

def main():
    """Handles the interactive command-line interface."""
    print("\n--- Caesar Cipher Tool ---")
    
    # 1. Get Mode (Encrypt or Decrypt)
    while True:
        mode_input = input("Do you want to (E)ncrypt or (D)ecrypt? (E/D): ").strip().lower()
        if mode_input == 'e':
            mode = 'encrypt'
            break
        elif mode_input == 'd':
            mode = 'decrypt'
            break
        else:
            print("Invalid selection. Please enter 'E' for Encrypt or 'D' for Decrypt.")
            
    # 2. Get Text
    input_text = input(f"Enter the text you want to {mode}: ")

    # 3. Get Key
    while True:
        try:
            # We enforce a positive key here, letting the cipher function handle the negative shift internally
            key_input = int(input("Enter the shift key (a positive number, e.g., 7): "))
            if key_input < 0:
                 print("Please enter a non-negative integer for the key.")
                 continue
            key = key_input
            break
        except ValueError:
            print("Invalid input. Please enter a valid integer for the key.")

    # 4. Process and Output
    processed_text = caesar_cipher(input_text, key, mode)

    print("-" * 30)
    print(f"Mode: {'Encryption' if mode == 'encrypt' else 'Decryption'}")
    print(f"Key: {key}")
    print(f"Original Text: {input_text}")
    print(f"Resulting Text: {processed_text}")
    print("-" * 30)

# Run the main interactive function when the script is executed
if _name_ == "_main_":
    main()
    print("Executed by the_Machine")

## EX. NO: 1(A) : IMPLEMENTATION OF CAESAR CIPHER
 

## AIM:

To implement the simple substitution technique named Caesar cipher using C language.

## DESCRIPTION:

To encrypt a message with a Caesar cipher, each letter in the message is changed using a simple rule: shift by three. Each letter is replaced by the letter three letters ahead in the alphabet. A becomes D, B becomes E, and so on. For the last letters, we can think of the
alphabet as a circle and "wrap around". W becomes Z, X becomes A, Y bec mes B, and Z
becomes C. To change a message back, each letter is replaced by the one three before it.

## EXAMPLE:



![image](https://github.com/Hemamanigandan/CNS/assets/149653568/eb9c6c43-8c80-4cdd-b9d4-91705a311c79)


## ALGORITHM:

### STEP-1: Read the plain text from the user.
### STEP-2: Read the key value from the user.
### STEP-3: If the key is positive then encrypt the text by adding the key with each character in the plain text.
### STEP-4: Else subtract the key from the plain text.
### STEP-5: Display the cipher text obtained above.


## PROGRAM :-

```
def format_key(key):
    key = key.upper().replace('J', 'I')  
    key = ''.join(sorted(set(key), key=key.index))  
    return key

def create_matrix(key):
    alphabet = 'ABCDEFGHIKLMNOPQRSTUVWXYZ'
    matrix = []
    for char in key:
        if char not in matrix:
            matrix.append(char)
    for char in alphabet:
        if char not in matrix:
            matrix.append(char)
    return [matrix[i:i+5] for i in range(0, len(matrix), 5)] 

def prepare_plaintext(plain_text):
    plain_text = plain_text.upper().replace('J', 'I')
    prepared_text = []
    i = 0
    while i < len(plain_text):
        if i + 1 < len(plain_text) and plain_text[i] == plain_text[i + 1]:
            prepared_text.append(plain_text[i] + 'X')
            i += 1
        else:
            prepared_text.append(plain_text[i:i + 2])  
            i += 2
    if len(prepared_text[-1]) == 1:  
        prepared_text[-1] = prepared_text[-1] + 'X'
    return prepared_text


def find_position(matrix, char):
    for i in range(5):
        for j in range(5):
            if matrix[i][j] == char:
                return i, j

def encrypt(plain_text, key):
    key = format_key(key)
    matrix = create_matrix(key)
    bigrams = prepare_plaintext(plain_text)
    
    cipher_text = ''
    for bigram in bigrams:
        row1, col1 = find_position(matrix, bigram[0])
        row2, col2 = find_position(matrix, bigram[1])
        
       
        if row1 == row2:
            cipher_text += matrix[row1][(col1 + 1) % 5]
            cipher_text += matrix[row2][(col2 + 1) % 5]
      
        elif col1 == col2:
            cipher_text += matrix[(row1 + 1) % 5][col1]
            cipher_text += matrix[(row2 + 1) % 5][col2]
      
        else:
            cipher_text += matrix[row1][col2]
            cipher_text += matrix[row2][col1]
    
    return cipher_text

def decrypt(cipher_text, key):
    key = format_key(key)
    matrix = create_matrix(key)
    bigrams = [cipher_text[i:i + 2] for i in range(0, len(cipher_text), 2)]
    
    plain_text = ''
    for bigram in bigrams:
        row1, col1 = find_position(matrix, bigram[0])
        row2, col2 = find_position(matrix, bigram[1])
        
        
        if row1 == row2:
            plain_text += matrix[row1][(col1 - 1) % 5]
            plain_text += matrix[row2][(col2 - 1) % 5]
       
        elif col1 == col2:
            plain_text += matrix[(row1 - 1) % 5][col1]
            plain_text += matrix[(row2 - 1) % 5][col2]
       
        else:
            plain_text += matrix[row1][col2]
            plain_text += matrix[row2][col1]
    
    return plain_text


if __name__ == "__main__":
    key = input("Enter the key for Playfair Cipher: ")
    plain_text = input("Enter the plaintext to encrypt: ")
    
    encrypted_text = encrypt(plain_text, key)
    print("Encrypted Text: ", encrypted_text)
    
    decrypted_text = decrypt(encrypted_text, key)
    print("Decrypted Text: ", decrypted_text)

```

## OUTPUT :-
![Screenshot 2025-03-20 085031](https://github.com/user-attachments/assets/6a90500a-7976-4ed3-a3f7-320171b125f5)


## RESULT :-
THE PROGRAM IS EXECUTED SUCCESSFULLY.

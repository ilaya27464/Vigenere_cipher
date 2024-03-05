# Ex.No: 1 D) IMPLEMENTATION OF VIGENERE CIPHER
### DATE: 27-02-2024                                                                          
### REGISTER NUMBER : 212221040057
### AIM: 
To implement the simple substitution technique named Vigenere cipher using C language.
### Steps:
1. : Arrange the alphabets in row and column of a 26*26 matrix.
2. Circulate the alphabets in each row to position left such that the first letter is attached to last.
3. Repeat this process for all 26 rows and construct the final key matrix.
4. The keyword and the plain text is read from the user.
5. The characters in the keyword are repeated sequentially so as to match with that of the plain text.
6. Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
7. The junction character where these two meet forms the cipher character.
8. Repeat the above steps to generate the entire cipher text.



### Program:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void vigenereEncrypt(char *plaintext, char *key, char *ciphertext) {
    int i, j, keyLen, textLen;
    char encryptedChar;

    keyLen = strlen(key);
    textLen = strlen(plaintext);

    for (i = 0, j = 0; i < textLen; ++i, ++j) {
        if (j == keyLen)
            j = 0;

        if (isalpha(plaintext[i])) {
            encryptedChar = ((toupper(plaintext[i]) + toupper(key[j])) % 26) + 'A';
            ciphertext[i] = encryptedChar;
        } else {
            ciphertext[i] = plaintext[i];
            --j;
        }
    }
    ciphertext[i] = '\0';
}

void vigenereDecrypt(char *ciphertext, char *key, char *plaintext) {
    int i, j, keyLen, textLen;
    char decryptedChar;

    keyLen = strlen(key);
    textLen = strlen(ciphertext);

    for (i = 0, j = 0; i < textLen; ++i, ++j) {
        if (j == keyLen)
            j = 0;

        if (isalpha(ciphertext[i])) {
            decryptedChar = ((toupper(ciphertext[i]) - toupper(key[j]) + 26) % 26) + 'A';
            plaintext[i] = decryptedChar;
        } else {
            plaintext[i] = ciphertext[i];
            --j;
        }
    }
    plaintext[i] = '\0';
}

int main() {
    char plaintext[100], key[100], ciphertext[100], decrypted[100];
    int choice;

    printf("Choose an option:\n");
    printf("1. Encryption\n");
    printf("2. Decryption\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    printf("Enter the text: ");
    getchar(); 
    fgets(plaintext, sizeof(plaintext), stdin);
    printf("Enter the key: ");
    fgets(key, sizeof(key), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0';
    key[strcspn(key, "\n")] = '\0';

    switch(choice) {
        case 1:
            vigenereEncrypt(plaintext, key, ciphertext);
            printf("Encrypted Text: %s\n", ciphertext);
            break;
        case 2:
            vigenereDecrypt(plaintext, key, decrypted);
            printf("Decrypted Text: %s\n", decrypted);
            break;
        default:
            printf("Invalid choice.\n");
    }

    return 0;
}

```


### Output:

## Encryption:

## Decryption:


### Result:
Thus the implementation of Vigenere cipher had been executed successfully.

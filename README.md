# Cryptography---19CS412-classical-techqniques

# Name : DILIP KUMAR R 
# REG NO : 212222040037

# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To develop a simple C program to implement Caeser Cipher.

## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <string.h>

// Function to perform Caesar cipher encryption
void encrypt(char *text, int shift) {
    int i;
    for (i = 0; i < strlen(text); i++) {
        // Encrypt uppercase letters
        if (text[i] >= 'A' && text[i] <= 'Z')
            text[i] = (text[i] - 'A' + shift) % 26 + 'A';
        // Encrypt lowercase letters
        else if (text[i] >= 'a' && text[i] <= 'z')
            text[i] = (text[i] - 'a' + shift) % 26 + 'a';
    }
}

// Function to perform Caesar cipher decryption
void decrypt(char *text, int shift) {
    int i;
    for (i = 0; i < strlen(text); i++) {
        // Decrypt uppercase letters
        if (text[i] >= 'A' && text[i] <= 'Z')
            text[i] = (text[i] - 'A' - shift + 26) % 26 + 'A';
        // Decrypt lowercase letters
        else if (text[i] >= 'a' && text[i] <= 'z')
            text[i] = (text[i] - 'a' - shift + 26) % 26 + 'a';
    }
}

int main() {
    char text[100];
    int shift;
    
    printf("Enter the text : ");
    fgets(text, sizeof(text), stdin);
    
    printf("Enter Key value: ");
    scanf("%d", &shift);

    // Encrypt the text
    encrypt(text, shift);
    printf("\nEncrypted text: %s\n", text);

    // Decrypt the text
    decrypt(text, shift);
    printf("Decrypted text: %s\n", text);

    return 0;
}
```
## OUTPUT:
![Screenshot 2024-03-07 122923](https://github.com/dilipkumar1265/Cryptography---19CS412-classical-techqniques/assets/119065291/6a63c0b5-746d-4f37-a6d2-e3cd41ef16bc)


## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```


#include<stdio.h>
#include<string.h>
#include<ctype.h>
#define MX 5

void playfair(char ch1, char ch2, char key[MX][MX]) {
    int i, j, w, x, y, z;
    FILE *out;
    if ((out = fopen("cipher.txt", "a+")) == NULL) {
        printf("File Corrupted.");
    }
    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (ch1 == key[i][j]) {
                w = i;
                x = j;
            } else if (ch2 == key[i][j]) {
                y = i;
                z = j;
            }
        }
    }
    if (w == y) {
        x = (x + 1) % 5;
        z = (z + 1) % 5;
        printf("%c%c", key[w][x], key[y][z]);
        fprintf(out, "%c%c", key[w][x], key[y][z]);
    } else if (x == z) {
        w = (w + 1) % 5;
        y = (y + 1) % 5;
        printf("%c%c", key[w][x], key[y][z]);
        fprintf(out, "%c%c", key[w][x], key[y][z]);
    } else {
        printf("%c%c", key[w][z], key[y][x]);
        fprintf(out, "%c%c", key[w][z], key[y][x]);
    }
    fclose(out);
}

int main() {
    int i, j, k = 0, l, m = 0, n;
    char key[MX][MX], keyminus[25], keystr[10], str[25] = {0};
    char alpa[26] = {'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    printf("\nEnter key:");
    gets(keystr);
    printf("\nEnter the plain text:");
    gets(str);
    n = strlen(keystr);
    for (i = 0; i < n; i++) {
        if (keystr[i] == 'j') keystr[i] = 'i';
        else if (keystr[i] == 'J') keystr[i] = 'I';
        keystr[i] = toupper(keystr[i]);
    }
    for (i = 0; i < strlen(str); i++) {
        if (str[i] == 'j') str[i] = 'i';
        else if (str[i] == 'J') str[i] = 'I';
        str[i] = toupper(str[i]);
    }
    j = 0;
    for (i = 0; i < 26; i++) {
        for (k = 0; k < n; k++) {
            if (keystr[k] == alpa[i]) break;
            else if (alpa[i] == 'J') break;
        }
        if (k == n) {
            keyminus[j] = alpa[i];
            j++;
        }
    }
    k = 0;
    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (k < n) {
                key[i][j] = keystr[k];
                k++;
            } else {
                key[i][j] = keyminus[m];
                m++;
            }
            printf("%c ", key[i][j]);
        }
        printf("\n");
    }
    printf("\n\nEntered text :%s\nCipher Text :",str);
    for (i = 0; i < strlen(str); i++) {
        if (str[i] == 'J') str[i] = 'I';
        if (str[i + 1] == '\0') playfair(str[i], 'X', key);
        else {
            if (str[i + 1] == 'J') str[i + 1] = 'I';
            if (str[i] == str[i + 1]) playfair(str[i], 'X', key);
            else {
                playfair(str[i], str[i + 1], key);
                i++;
            }
        }
  
    }
     printf("\nDecrypted text:%s",str);
    return 0;
}
```

## OUTPUT:
![Screenshot 2024-03-07 123108](https://github.com/dilipkumar1265/Cryptography---19CS412-classical-techqniques/assets/119065291/8a7986d8-a46f-49be-882e-f857b73e4e57)


## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>

int main() 
{
    unsigned int key[3][3] = {{6, 24, 1}, {13, 16, 10}, {20, 17, 15}};
    unsigned int inverseKey[3][3] = {{8, 5, 10}, {21, 8, 21}, {21, 12, 8}};

    char msg[4];
    unsigned int enc[3] = {0}, dec[3] = {0};

    printf("Enter plain text: ");
    scanf("%3s", msg);

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            enc[i] += key[i][j] * (msg[j] - 'A') % 26;

    printf("Encrypted  Text: %c%c%c\n", enc[0] % 26 + 'A', enc[1] % 26 + 'A', enc[2] % 26 + 'A');

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            dec[i] += inverseKey[i][j] * enc[j] % 26;

    printf("Decrypted  Text: %c%c%c\n", dec[0] % 26 + 'A', dec[1] % 26 + 'A', dec[2] % 26 + 'A');

    return 0;
}
```

## OUTPUT:
![Screenshot 2024-03-07 123923](https://github.com/dilipkumar1265/Cryptography---19CS412-classical-techqniques/assets/119065291/e7673930-930e-491b-9164-c54e51861033)


## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_LENGTH 100

// Function to encrypt or decrypt text using the Vigenère cipher
void vigenereCipher(char *input, char *key, char *output, int encrypt) {
    int inputLength = strlen(input);
    int keyLength = strlen(key);

    for (int i = 0, j = 0; i < inputLength; ++i) {
        char currentChar = input[i];
        
        if (isalpha(currentChar)) {
            // Determine the shift value based on the key
            int keyIndex = j % keyLength;
            int shift = toupper(key[keyIndex]) - 'A';

            if (!encrypt) {
                shift = -shift;
            }

            // Encrypt or decrypt the current character
            if (isupper(currentChar)) {
                output[i] = ((currentChar - 'A' + shift + 26) % 26) + 'A';
            } else {
                output[i] = ((currentChar - 'a' + shift + 26) % 26) + 'a';
            }

            ++j;
        } else {
            // Non-alphabetic characters remain unchanged
            output[i] = currentChar;
        }
    }

    output[inputLength] = '\0';
}

int main() {
    char input[MAX_LENGTH];
    char key[MAX_LENGTH];
    char encrypted[MAX_LENGTH];
    char decrypted[MAX_LENGTH];

    printf("Enter the text : ");
    fgets(input, MAX_LENGTH, stdin);
    input[strcspn(input, "\n")] = '\0'; // Remove trailing newline if present
    printf("Enter the key: ");
    fgets(key, MAX_LENGTH, stdin);
    key[strcspn(key, "\n")] = '\0'; // Remove trailing newline if present

    // Encrypt the input text
    vigenereCipher(input, key, encrypted, 1);
    printf("Encrypted text: %s\n", encrypted);

    // Decrypt the encrypted text
    vigenereCipher(encrypted, key, decrypted, 0);
    printf("Decrypted text: %s\n", decrypted);

    return 0;
}

```

## OUTPUT:
![Screenshot 2024-03-07 122551](https://github.com/dilipkumar1265/Cryptography---19CS412-classical-techqniques/assets/119065291/f2034063-26bb-4d54-882b-cf1c27a50dba)


## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include<stdio.h>
#include<string.h>

int main(){
    int i, j, k, l;
    char a[20], c[20], d[20];
    printf("\n\nEnter the text: ");
    gets(a);
    l = strlen(a);

    // Ciphering
    for(i = 0, j = 0; i < l; i++){
        if(i % 2 == 0)
            c[j++] = a[i];
    }
    for(i = 0; i < l; i++){
        if(i % 2 == 1)
            c[j++] = a[i];
    }
    c[j] = '\0';

    printf("\nEncrypted Text:");
    printf("%s", c);

    // Deciphering
    if(l % 2 == 0)
        k = l / 2;
    else
        k = (l / 2) + 1;

    for(i = 0, j = 0; i < k; i++){
        d[j] = c[i];
        j = j + 2;
    }
    for(i = k, j = 1; i < l; i++){
        d[j] = c[i];
        j = j + 2;
    }
    d[l] = '\0';

    printf("\nDecrypted Text:");
    printf("%s", d);

    return 0;
}
```

## OUTPUT:
![Screenshot 2024-03-07 122219](https://github.com/dilipkumar1265/Cryptography---19CS412-classical-techqniques/assets/119065291/6f44ed2c-765b-4b13-bf65-f504472806ba)


## RESULT:
The program is executed successfully

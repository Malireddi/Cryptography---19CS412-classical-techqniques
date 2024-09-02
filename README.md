# Cryptography---19CS412-classical-techqniques
# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
PROGRAM:
CaearCipher.
PROGRAM:
```
Caesar Cipher Encryption Code:
#include <stdio.h>

void encrypt(char text[], int shift) {
    char ch;
    for (int i = 0; text[i] != '\0'; ++i) {
        ch = text[i];
        
        if (ch >= 'a' && ch <= 'z') {
            ch = ch + shift;

            if (ch > 'z') {
                ch = ch - 'z' + 'a' - 1;
            }

            text[i] = ch;
        } else if (ch >= 'A' && ch <= 'Z') {
            ch = ch + shift;

            if (ch > 'Z') {
                ch = ch - 'Z' + 'A' - 1;
            }

            text[i] = ch;
        }
    }
}

int main() {
    char text[100];
    int shift;

    printf("Enter a message to encrypt: ");
    gets(text);

    printf("Enter shift amount: ");
    scanf("%d", &shift);

    encrypt(text, shift);

    printf("Encrypted message: %s\n", text);

    return 0;
}
Caesar Cipher Decryption Code
#include <stdio.h>

void decrypt(char text[], int shift) {
    char ch;
    for (int i = 0; text[i] != '\0'; ++i) {
        ch = text[i];
        
        if (ch >= 'a' && ch <= 'z') {
            ch = ch - shift;

            if (ch < 'a') {
                ch = ch + 'z' - 'a' + 1;
            }

            text[i] = ch;
        } else if (ch >= 'A' && ch <= 'Z') {
            ch = ch - shift;

            if (ch < 'A') {
                ch = ch + 'Z' - 'A' + 1;
            }

            text[i] = ch;
        }
    }
}

int main() {
    char text[100];
    int shift;

    printf("Enter a message to decrypt: ");
    gets(text);

    printf("Enter shift amount: ");
    scanf("%d", &shift);

    decrypt(text, shift);

    printf("Decrypted message: %s\n", text);

    return 0;
}
```

## OUTPUT:
OUTPUT:
Simulating Caesar Cipher

![Screenshot 2024-09-02 134434](https://github.com/user-attachments/assets/2fe2e29c-bde9-4945-b0bb-886a8af882bf)

![image](https://github.com/user-attachments/assets/0d043a8b-5a0e-4c43-ab0f-7d244d8aa1ff)



## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define SIZE 5

void generateKeyTable(char key[], char keyTable[SIZE][SIZE]) {
    int dicty[26] = {0};
    int i, j, k = 0, len = strlen(key);


    for (i = 0; i < len; i++) {
        if (key[i] != 'j' && dicty[key[i] - 'a'] == 0) {
            keyTable[k / SIZE][k % SIZE] = key[i];
            dicty[key[i] - 'a'] = 1;
            k++;
        }
    }


    for (i = 0; i < 26; i++) {
        if (i != 9 && dicty[i] == 0) { // skip 'j'
            keyTable[k / SIZE][k % SIZE] = (char)(i + 'a');
            k++;
        }
    }
}

void prepareText(char text[], char preparedText[]) {
    int i, j = 0, len = strlen(text);

    for (i = 0; i < len; i++) {
        text[i] = tolower(text[i]);
        if (text[i] == 'j') {
            text[i] = 'i';
        }
    }

    for (i = 0; i < len; i++) {
        if (isalpha(text[i])) {
            preparedText[j++] = text[i];
        }
    }

    preparedText[j] = '\0';


    for (i = 0; i < j; i += 2) {
        if (preparedText[i] == preparedText[i + 1]) {
            memmove(preparedText + i + 2, preparedText + i + 1, j - i + 1);
            preparedText[i + 1] = 'x';
            j++;
        }
    }

    if (strlen(preparedText) % 2 != 0) {
        preparedText[j++] = 'x';
        preparedText[j] = '\0';
    }
}

void searchPosition(char keyTable[SIZE][SIZE], char a, char b, int pos[]) {
    int i, j;

    if (a == 'j') a = 'i';
    if (b == 'j') b = 'i';

    for (i = 0; i < SIZE; i++) {
        for (j = 0; j < SIZE; j++) {
            if (keyTable[i][j] == a) {
                pos[0] = i;
                pos[1] = j;
            }
            if (keyTable[i][j] == b) {
                pos[2] = i;
                pos[3] = j;
            }
        }
    }
}

void encryptOrDecrypt(char text[], char keyTable[SIZE][SIZE], int mode) {
    int i, pos[4], len = strlen(text);

    for (i = 0; i < len; i += 2) {
        searchPosition(keyTable, text[i], text[i + 1], pos);

        if (pos[0] == pos[2]) {
            text[i] = keyTable[pos[0]][(pos[1] + mode + SIZE) % SIZE];
            text[i + 1] = keyTable[pos[2]][(pos[3] + mode + SIZE) % SIZE];
        } else if (pos[1] == pos[3]) {
            text[i] = keyTable[(pos[0] + mode + SIZE) % SIZE][pos[1]];
            text[i + 1] = keyTable[(pos[2] + mode + SIZE) % SIZE][pos[3]];
        } else {
            text[i] = keyTable[pos[0]][pos[3]];
            text[i + 1] = keyTable[pos[2]][pos[1]];
        }
    }
}

int main() {
    char key[30], text[100], preparedText[100], keyTable[SIZE][SIZE];
    int choice;

    printf("Enter the key: ");
    gets(key);

    generateKeyTable(key, keyTable);

    printf("Enter the text: ");
    gets(text);

    prepareText(text, preparedText);

    printf("Enter 1 to encrypt or 2 to decrypt: ");
    scanf("%d", &choice);

    if (choice == 1) {
        encryptOrDecrypt(preparedText, keyTable, 1);  
        printf("Encrypted text: %s\n", preparedText);
    } else if (choice == 2) {
        encryptOrDecrypt(preparedText, keyTable, -1); 
        printf("Decrypted text: %s\n", preparedText);
    } else {
        printf("Invalid choice!\n");
    }

    return 0;
}
```
## OUTPUT:
Output:

![Screenshot 2024-09-02 140052](https://github.com/user-attachments/assets/34adeb93-779c-4bbc-b31e-f2251222e45a)

![image](https://github.com/user-attachments/assets/7dd612a0-04eb-4019-b02c-5268845023a1)



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
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
PROGRAM:
```
#include <stdio.h>
#include <string.h>

#define MATRIX_SIZE 3

void getKeyMatrix(char key[], int keyMatrix[MATRIX_SIZE][MATRIX_SIZE]) {
    int k = 0;
    for (int i = 0; i < MATRIX_SIZE; i++) {
        for (int j = 0; j < MATRIX_SIZE; j++) {
            keyMatrix[i][j] = (key[k]) % 65; // 'A' -> 0, 'B' -> 1, ...
            k++;
        }
    }
}

void getCofactor(int mat[MATRIX_SIZE][MATRIX_SIZE], int temp[MATRIX_SIZE][MATRIX_SIZE], int p, int q, int n) {
    int i = 0, j = 0;
    for (int row = 0; row < n; row++) {
        for (int col = 0; col < n; col++) {
            if (row != p && col != q) {
                temp[i][j++] = mat[row][col];
                if (j == n - 1) {
                    j = 0;
                    i++;
                }
            }
        }
    }
}

int determinant(int mat[MATRIX_SIZE][MATRIX_SIZE], int n) {
    int D = 0;
    if (n == 1)
        return mat[0][0];

    int temp[MATRIX_SIZE][MATRIX_SIZE];
    int sign = 1;

    for (int f = 0; f < n; f++) {
        getCofactor(mat, temp, 0, f, n);
        D += sign * mat[0][f] * determinant(temp, n - 1);
        sign = -sign;
    }

    return D;
}

void adjoint(int mat[MATRIX_SIZE][MATRIX_SIZE], int adj[MATRIX_SIZE][MATRIX_SIZE]) {
    if (MATRIX_SIZE == 1) {
        adj[0][0] = 1;
        return;
    }

    int sign = 1, temp[MATRIX_SIZE][MATRIX_SIZE];

    for (int i = 0; i < MATRIX_SIZE; i++) {
        for (int j = 0; j < MATRIX_SIZE; j++) {
            getCofactor(mat, temp, i, j, MATRIX_SIZE);
            sign = ((i + j) % 2 == 0) ? 1 : -1;
            adj[j][i] = (sign * determinant(temp, MATRIX_SIZE - 1));
        }
    }
}

int modInverse(int a, int m) {
    a = a % m;
    for (int x = 1; x < m; x++)
        if ((a * x) % m == 1)
            return x;
    return -1;
}

void inverse(int mat[MATRIX_SIZE][MATRIX_SIZE], int inverse[MATRIX_SIZE][MATRIX_SIZE]) {
    int det = determinant(mat, MATRIX_SIZE);
    int invDet = modInverse(det, 26);

    if (invDet == -1) {
        printf("Inverse doesn't exist, key matrix is not invertible!\n");
        return;
    }

    int adj[MATRIX_SIZE][MATRIX_SIZE];
    adjoint(mat, adj);

    for (int i = 0; i < MATRIX_SIZE; i++)
        for (int j = 0; j < MATRIX_SIZE; j++)
            inverse[i][j] = (adj[i][j] * invDet) % 26;

    for (int i = 0; i < MATRIX_SIZE; i++)
        for (int j = 0; j < MATRIX_SIZE; j++)
            if (inverse[i][j] < 0)
                inverse[i][j] += 26;
}

void multiplyMatrix(int mat1[MATRIX_SIZE][MATRIX_SIZE], int mat2[], int res[]) {
    for (int i = 0; i < MATRIX_SIZE; i++) {
        res[i] = 0;
        for (int j = 0; j < MATRIX_SIZE; j++) {
            res[i] += mat1[i][j] * mat2[j];
        }
        res[i] = res[i] % 26;
    }
}

void encrypt(char message[], int keyMatrix[MATRIX_SIZE][MATRIX_SIZE]) {
    int messageVector[MATRIX_SIZE];
    int cipherVector[MATRIX_SIZE];

    for (int i = 0; i < MATRIX_SIZE; i++) {
        messageVector[i] = (message[i]) % 65;
    }

    multiplyMatrix(keyMatrix, messageVector, cipherVector);

    printf("Encrypted text: ");
    for (int i = 0; i < MATRIX_SIZE; i++) {
        printf("%c", cipherVector[i] + 65);
    }
    printf("\n");
}

void decrypt(char message[], int inverseKeyMatrix[MATRIX_SIZE][MATRIX_SIZE]) {
    int messageVector[MATRIX_SIZE];
    int plainVector[MATRIX_SIZE];

    for (int i = 0; i < MATRIX_SIZE; i++) {
        messageVector[i] = (message[i]) % 65;
    }

    multiplyMatrix(inverseKeyMatrix, messageVector, plainVector);

    printf("Decrypted text: ");
    for (int i = 0; i < MATRIX_SIZE; i++) {
        printf("%c", plainVector[i] + 65);
    }
    printf("\n");
}

int main() {
    char message[MATRIX_SIZE + 1];
    char key[MATRIX_SIZE * MATRIX_SIZE + 1];
    int keyMatrix[MATRIX_SIZE][MATRIX_SIZE];
    int inverseKeyMatrix[MATRIX_SIZE][MATRIX_SIZE];
    int choice;

    printf("Enter the %d-letter key: ", MATRIX_SIZE * MATRIX_SIZE);
    gets(key);

    getKeyMatrix(key, keyMatrix);

    printf("Enter the %d-letter message: ", MATRIX_SIZE);
    gets(message);

    printf("Enter 1 to encrypt or 2 to decrypt: ");
    scanf("%d", &choice);

    if (choice == 1) {
        encrypt(message, keyMatrix);
    } else if (choice == 2) {
        inverse(keyMatrix, inverseKeyMatrix);
        decrypt(message, inverseKeyMatrix);
    } else {
        printf("Invalid choice!\n");
    }

    return 0;
}
```


## OUTPUT:
OUTPUT:
Simulating Hill Cipher

![image](https://github.com/user-attachments/assets/1fcc984c-e329-45a2-a476-b854c5881f6b)

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
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void generateKey(char str[], char key[]) {
    int strLen = strlen(str);
    int keyLen = strlen(key);
    int i, j;

    for (i = 0, j = 0; i < strLen; i++, j++) {
        if (j == keyLen)
            j = 0;
        key[i] = key[j];
    }
    key[i] = '\0';
}

void encryptDecrypt(char str[], char key[], int mode) {
    int strLen = strlen(str);
    char result[strLen];

    for (int i = 0; i < strLen; i++) {
        if (isalpha(str[i])) {
            char base = isupper(str[i]) ? 'A' : 'a';
            if (mode == 1) { 
                result[i] = (str[i] + key[i] - 2 * base) % 26 + base;
            } else if (mode == 2) { 
                result[i] = (str[i] - key[i] + 26) % 26 + base;
            }
        } else {
            result[i] = str[i]; 
        }
    }

    result[strLen] = '\0';
    printf("Result: %s\n", result);
}

int main() {
    char str[100], key[100];
    int choice;

    printf("Enter the text: ");
    gets(str);

    printf("Enter the key: ");
    gets(key);

    char originalKey[100];
    strcpy(originalKey, key);

    generateKey(str, key);

    printf("Enter 1 to encrypt or 2 to decrypt: ");
    scanf("%d", &choice);

    if (choice == 1) {
        encryptDecrypt(str, key, 1);  
    } else if (choice == 2) {
        encryptDecrypt(str, key, 2);  
    } else {
        printf("Invalid choice!\n");
    }

    return 0;
}
```

## OUTPUT:
OUTPUT :

Simulating Vigenere Cipher

![image](https://github.com/user-attachments/assets/811d722f-ef42-4869-83e0-2cdc5078441b)

![image](https://github.com/user-attachments/assets/1b0f267d-c9e7-4d4a-a71e-6c8f1567a283)


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
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:

PROGRAM:

```
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
main()
{
int i,j,len,rails,count,code[100][1000];
 char str[1000];
 printf("Enter a Secret Message\n");
 gets(str);
 len=strlen(str);
printf("Enter number of rails\n");
scanf("%d",&rails);
for(i=0;i<rails;i++)
{
 for(j=0;j<len;j++)
 {
 code[i][j]=0;
 }
}
count=0;
j=0;
while(j<len)
{
if(count%2==0)
{
for(i=0;i<rails;i++)
{
 //strcpy(code[i][j],str[j]);
 code[i][j]=(int)str[j]; 
 j++;
}
}
else
{
for(i=rails-2;i>0;i--)
{
 code[i][j]=(int)str[j];
j++;
} 
} 
count++;
}
for(i=0;i<rails;i++)
{
for(j=0;j<len;j++)
{
 if(code[i][j]!=0)
 printf("%c",code[i][j]);
}
}
printf("\n");
}
```
## OUTPUT:
OUTPUT:

![Screenshot 2024-09-02 142437](https://github.com/user-attachments/assets/07d9c517-dd7d-461f-99d2-aa5f63b684ce)

## RESULT:
The program is executed successfully

# Cryptography---19CS412-classical-techqniques
## EX.NO:1-Caeser Cipher
## DATE:19-02-2025

Caeser Cipher using with different key values

### AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


### DESIGN STEPS:

#### Step 1:

Design of Caeser Cipher algorithnm 

#### Step 2:

Implementation using C or pyhton code

#### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


### PROGRAM:
CaearCipher.
```
'''
Developed By:Moenish Baalan G
Ref No.: 212223220057
'''
#include <stdio.h>
#include <stdlib.h>
 
void caesarEncrypt(char *text, int key) {
   for (int i = 0; text[i] != '\0'; i++) 
   { 
       char c = text[i];
    if (c >= 'A' && c <= 'Z') 
    {
    text[i] = ((c - 'A' + key) % 26 + 26) % 26 + 'A';
    }
    else if (c >= 'a' && c <= 'z') 
    {
        text[i] = ((c - 'a' + key) % 26 + 26) % 26 + 'a';
    }
    }
}

void caesarDecrypt(char *text, int key) {
caesarEncrypt(text, -key);
}

int main() {
char message[100]; 
int key;
printf("Enter the message to encrypt: ");
fgets(message, sizeof(message), stdin); 
printf("Enter the Caesar Cipher key (an integer): ");
scanf("%d", &key); 
caesarEncrypt(message, key); 
printf("Encrypted Message: %s", message);
caesarDecrypt(message, key); 
printf("Decrypted Message: %s", message);
return 0;
}
```
### OUTPUT:
![image](https://github.com/user-attachments/assets/428cdc73-1e97-4d5b-97a9-719f9c007b1f)


### RESULT:
The program is executed successfully

---------------------------------


## EX.NO:2-PlayFair Cipher
## DATE:24-02-2025
Playfair Cipher using with different key values

### AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
### DESIGN STEPS:

#### Step 1:

Design of PlayFair Cipher algorithnm 

#### Step 2:

Implementation using C or pyhton code

#### Step 3:

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
py
'''
Developed By:Moenish Baalan G
Ref No.: 212223220057
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define SIZE 30

void toLowerCase(char plain[], int ps)
{
int i;
for (i = 0; i < ps; i++) {
if (plain[i] > 64 && plain[i] < 91)
plain[i] += 32;}}
int removeSpaces(char* plain, int ps)
{
int i, count = 0;
for (i = 0; i < ps; i++)
if (plain[i] != ' ')
plain[count++] = plain[i];
plain[count] = '\0'; return count;
}

void generateKeyTable(char key[], int ks, char keyT[5][5])
{
int i, j, k, flag = 0, *dicty;
dicty = (int*)calloc(26, sizeof(int));
for (i = 0; i < ks; i++) {
if (key[i] != 'j')
dicty[key[i] - 97] = 2;
}
dicty['j' - 97] = 1;
i = 0;
j = 0;
for (k = 0; k < ks; k++) {
if (dicty[key[k] - 97] == 2) {
dicty[key[k] - 97] -= 1;
keyT[i][j] = key[k]; j++;
if (j == 5) {
i++; j = 0;}}}
for (k = 0; k < 26; k++) {
if (dicty[k] == 0) {
keyT[i][j] = (char)(k + 97);
 
j++;
if (j == 5) {
i++; j = 0;}}}}
void search(char keyT[5][5], char a, char b, int arr[])
{
int i, j;

if (a == 'j')
a = 'i'; else if (b == 'j')
b = 'i';
for (i = 0; i < 5; i++) {
for (j = 0; j < 5; j++) {
if (keyT[i][j] == a) {
arr[0] = i;
arr[1] = j;
}
else if (keyT[i][j] == b) {
arr[2] = i;
arr[3] = j;}}}}

int mod5(int a)
{
return (a % 5);
}

int prepare(char str[], int ptrs)
{
if (ptrs % 2 != 0) {
str[ptrs++] = 'z';
str[ptrs] = '\0';}
return ptrs;}
void encrypt(char str[], char keyT[5][5], int ps)
{
int i, a[4];

for (i = 0; i < ps; i += 2) {
search(keyT, str[i], str[i + 1], a); if (a[0] == a[2]) {
str[i] = keyT[a[0]][mod5(a[1] + 1)];
str[i + 1] = keyT[a[0]][mod5(a[3] + 1)];
}
else if (a[1] == a[3]) {
str[i] = keyT[mod5(a[0] + 1)][a[1]];
str[i + 1] = keyT[mod5(a[2] + 1)][a[1]];
}
else {
str[i] = keyT[a[0]][a[3]];
str[i + 1] = keyT[a[2]][a[1]];}}}
void encryptByPlayfairCipher(char str[], char key[])
{
char ps, ks, keyT[5][5];
ks = strlen(key);
ks = removeSpaces(key, ks); toLowerCase(key, ks);
ps = strlen(str); toLowerCase(str, ps);
ps = removeSpaces(str, ps); ps = prepare(str, ps);
generateKeyTable(key, ks, keyT); encrypt(str, keyT, ps);
 
}
int main()
{
char str[SIZE], key[SIZE];
strcpy(key, "Monarchy"); 
printf("Key text: %s\n", key);
strcpy(str, "instruments"); 
printf("Plain text: %s\n", str);
encryptByPlayfairCipher(str, key);
printf("Cipher text: %s\n", str);
return 0;
}
```
### OUTPUT:
![Screenshot 2025-03-19 085013](https://github.com/user-attachments/assets/9fa20c3d-e6a7-40e7-8c11-5918b4225284)

### RESULT:
The program is executed successfully


---------------------------

## Hill Cipher
Hill Cipher using with different key values

### EX.NO:3-Hill Cipher
### DATE:26-02-2025

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
c
'''
Developed By:Moenish Baalan G
Ref No.: 212223220057
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>

int keymat[3][3] = {{1, 2, 1}, {2, 3, 2}, {2, 2, 1}};
int invkeymat[3][3] = {{-1, 0, 1}, {2, -1, 0}, {-2, 2, -1}};
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

char* process(char a, char b, char c, int mat[3][3]) {
    char* ret = (char*)malloc(4);
    int x = (a - 65) * mat[0][0] + (b - 65) * mat[1][0] + (c - 65) * mat[2][0];
    int y = (a - 65) * mat[0][1] + (b - 65) * mat[1][1] + (c - 65) * mat[2][1];
    int z = (a - 65) * mat[0][2] + (b - 65) * mat[1][2] + (c - 65) * mat[2][2];
    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
    return ret;
}

void hill_cipher(char* msg, int mat[3][3], char* result) {
    for (int i = 0; i < strlen(msg); i += 3) {
        strcat(result, process(msg[i], msg[i + 1], msg[i + 2], mat));
    }
}

int main() {
    char msg[100] = "SECURITYLABORATORY", enc[100] = "", dec[100] = "";
    printf("Simulation of Hill Cipher\nInput message: %s\n", msg);

    for (int i = strlen(msg) % 3; i < 3 && i > 0; i++) strcat(msg, "X");
    printf("Padded message: %s\n", msg);

    hill_cipher(msg, keymat, enc);
    printf("Encoded message: %s\n", enc);

    hill_cipher(enc, invkeymat, dec);
    printf("Decoded message: %s\n", dec);

    return 0;
}
```

## OUTPUT:
![Screenshot 2025-03-19 085141](https://github.com/user-attachments/assets/c6593f37-a7ac-4c34-8ada-5c0a08125f18)

## RESULT:
The program is executed successfully

-------------------------------------------------

## EX.NO:4-Vigenere Cipher
## DATE:03-03-2025
Vigenere Cipher using with different key values

### AIM:

To develop a simple C program to implement Vigenere Cipher.

### DESIGN STEPS:

#### Step 1:

Design of Vigenere Cipher algorithnm 

#### Step 2:

Implementation using C or pyhton code

#### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



### PROGRAM:
c
'''
Developed By:Moenish Baalan G
Ref No.: 212223220057
```
#include <stdio.h>
#include <string.h>
void vigenereEncrypt(char *text, const char *key) {
    int textLen = strlen(text);
    int keyLen = strlen(key);
    for (int i = 0; i < textLen; i++) {
        char c = text[i];
        if (c >= 'A' && c <= 'Z') {
            text[i] = ((c - 'A' + key[i % keyLen] - 'A') % 26) + 'A';
        } else if (c >= 'a' && c <= 'z') {
            // Encrypt lowercase letters
            text[i] = ((c - 'a' + key[i % keyLen] - 'A') % 26) + 'a';
        }
    }
}
void vigenereDecrypt(char *text, const char *key) {
    int textLen = strlen(text);
    int keyLen = strlen(key);
    for (int i = 0; i < textLen; i++) {
        char c = text[i];
        if (c >= 'A' && c <= 'Z') {
            text[i] = ((c - 'A' - (key[i % keyLen] - 'A') + 26) % 26) + 'A';
        } else if (c >= 'a' && c <= 'z') {
            text[i] = ((c - 'a' - (key[i % keyLen] - 'A') + 26) % 26) + 'a';
        }
    }
}

int main() {
    const char *key = "KEY"; 
    char message[100] ;
    printf("Enter the message:");
    scanf("%[^\n]",message);
    vigenereEncrypt(message, key);
    printf("Encrypted Message: %s\n", message);
    vigenereDecrypt(message, key);
    printf("Decrypted Message: %s\n", message);
   return 0;
}
```
### OUTPUT:
![Screenshot 2025-03-19 085350](https://github.com/user-attachments/assets/cc7b49d6-780a-4efb-8844-4cb6074c3864)

### RESULT:
The program is executed successfully

-----------------------------------------------------------------------

## EX.NO:5-Rail Fence Cipher
## DATE:05-03-2025
Rail Fence Cipher using with different key values

### AIM:

To develop a simple C program to implement Rail Fence Cipher.

### DESIGN STEPS:

#### Step 1:

Design of Rail Fence Cipher algorithnm 

#### Step 2:

Implementation using C or pyhton code

#### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

### PROGRAM:
c
'''
Developed By:Moenish Baalan G
Ref No.: 212223220057
```
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main() {
    int i, j, len, rails, count, direction;
    char code[100][1000]; 
    char str[1000];
    printf("Enter a Secret Message: ");
    fgets(str, sizeof(str), stdin);  
    str[strcspn(str, "\n")] = 0;     
    len = strlen(str);
    printf("Enter number of rails: ");
    scanf("%d", &rails);
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            code[i][j] = '\0';
        }
    }
    count = 0;
    direction = 1; // 1 for moving down, -1 for moving up
    for (j = 0, i = 0; j < len; j++) {
        code[i][j] = str[j];
        if (i == 0) {
            direction = 1; // Move down when at the top
        } else if (i == rails - 1) {
            direction = -1; // Move up when at the bottom
        }
        i += direction; // Move up or down the rails
    }
    printf("Encrypted Message: ");
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (code[i][j] != '\0') {
                printf("%c", code[i][j]);
            }
        }
    }
    printf("\n");
    return 0;
}
```
### OUTPUT:
![Screenshot 2025-03-19 085608](https://github.com/user-attachments/assets/76102be1-26e6-448f-9542-c9d4a9d57f5f)


### RESULT:
The program is executed successfully

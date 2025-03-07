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
```
Developed by: Karan A
Register number: 212223230099
```
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

void encode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];

    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}

void decode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = a - 'A';
    int posb = b - 'A';
    int posc = c - 'A';

    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];

    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
}

int main() {
    char msg[1000] = "SecurityLaboratory";
    char enc[1000] = "";
    char dec[1000] = "";
    char temp[4];
    
    printf("Simulation of Hill Cipher\n");
    printf("Input message: %s\n", msg);

    // Convert to uppercase and remove spaces
    int len = 0;
    for (int i = 0; msg[i] != '\0'; i++) {
        if (msg[i] != ' ') {
            msg[len++] = toupper(msg[i]);
        }
    }
    msg[len] = '\0';

    // Padding with 'X' if length is not a multiple of 3
    while (len % 3 != 0) {
        msg[len++] = 'X';
    }
    msg[len] = '\0';

    printf("Padded message: %s\n", msg);

    // Encoding
    for (int i = 0; i < len; i += 3) {
        encode(msg[i], msg[i + 1], msg[i + 2], temp);
        strcat(enc, temp);
    }

    printf("Encoded message: %s\n", enc);

    // Decoding
    for (int i = 0; i < len; i += 3) {
        decode(enc[i], enc[i + 1], enc[i + 2], temp);
        strcat(dec, temp);
    }

    printf("Decoded message: %s\n", dec);

    return 0;
}
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/affd6da5-f1c9-46ec-a283-434e0dfd9fee)

## RESULT:
The program is executed successfully

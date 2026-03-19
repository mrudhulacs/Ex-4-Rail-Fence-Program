# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.


# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.

STEP-2: Arrange the plain text in row columnar matrix format.

STEP-3: Now read the keyword depending on the number of columns of the plain text.

STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.

STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.


# PROGRAM

```
#include <stdio.h> 
#include <string.h> 
 
void railFenceEncrypt(char *message, int rails, char *cipherText) { 
    int len = strlen(message); 
    int row = 0, dir = 1;   
    char rail[rails][len]; 
    memset(rail, '\n', sizeof(rail)); 
 
    for (int i = 0; i < len; i++) { 
        rail[row][i] = message[i]; 
        if (row == 0) dir = 1; 
        else if (row == rails - 1) dir = -1; 
        row += dir; 
    } 
 
    int k = 0; 
    for (int i = 0; i < rails; i++) { 
        for (int j = 0; j < len; j++) { 
            if (rail[i][j] != '\n') { 
                cipherText[k++] = rail[i][j]; 
            } 
        } 
    } 
    cipherText[k] = '\0'; 
} 
 
void railFenceDecrypt(char *cipherText, int rails, char *plainText) { 
    int len = strlen(cipherText); 
    char rail[rails][len]; 
    memset(rail, '\n', sizeof(rail)); 
 
    int row = 0, dir = 1; 
    for (int i = 0; i < len; i++) { 
        rail[row][i] = '*'; 
        if (row == 0) dir = 1; 
        else if (row == rails - 1) dir = -1; 
        row += dir; 
    } 
 
    int k = 0; 
    for (int i = 0; i < rails; i++) { 
        for (int j = 0; j < len; j++) { 
            if (rail[i][j] == '*' && k < len) { 
                rail[i][j] = cipherText[k++]; 
            } 
        } 
    } 
 
    row = 0, dir = 1; 
    for (int i = 0; i < len; i++) { 
        plainText[i] = rail[row][i]; 
        if (row == 0) dir = 1; 
        else if (row == rails - 1) dir = -1; 
        row += dir; 
    } 
    plainText[len] = '\0'; 
} 
 
int main() { 
    char message[100], cipherText[100], decryptedText[100]; 
    int rails; 
 
    printf ("Enter the plain text: "); 
    fgets(message, sizeof(message), stdin); 
    message[strcspn(message, "\n")] = '\0'; 
 
    printf ("Enter number of rails: "); 
    scanf("%d", &rails); 
 
    railFenceEncrypt(message, rails, cipherText); 
    printf("\nEncrypted Text: %s\n", cipherText); 
 
    railFenceDecrypt(cipherText, rails, decryptedText); 
    printf ("Decrypted Text: %s\n", decryptedText); 
 
    return 0; 
}




```



# OUTPUT

<img width="1375" height="890" alt="image" src="https://github.com/user-attachments/assets/6dc30ba9-4935-4d5e-8c15-c8d0d6160d88" />

# RESULT


The program has been executed successfully.


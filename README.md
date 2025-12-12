# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
#include <stdio.h>
#include <string.h>

long long modexp(long long b,long long e,long long m){
    long long r=1;
    while(e){ if(e&1) r=(r*b)%m; b=(b*b)%m; e>>=1; }
    return r;
}
long long egcd(long long a,long long b,long long *x,long long *y){
    if(!b){ *x=1; *y=0; return a; }
    long long x1,y1,g=egcd(b,a%b,&x1,&y1);
    *x=y1; *y=x1-(a/b)*y1; return g;
}

int main(void){
    int p=61,q=53;
    int n=p*q, phi=(p-1)*(q-1), e=17;
    long long x,y;
    if (egcd(e,phi,&x,&y)!=1){ puts("e and phi not coprime"); return 1; }
    int d = (int)((x%phi+phi)%phi);

    printf("Public Key: (e = %d, n = %d)\n", e, n);
    printf("Private Key: (d = %d, n = %d)\n", d, n);

    char msg[100];
    printf("Enter a message to encrypt (alphabetic characters only): ");
    if(!fgets(msg,sizeof msg,stdin)) return 0;
    size_t len = strlen(msg); if(len && msg[len-1]=='\n'){ msg[--len]=0; }

    printf("\nEncrypted Message:\n");
    long long enc[100];
    for(size_t i=0;i<len;i++){
        int m = (unsigned char)msg[i];
        enc[i] = modexp(m, e, n);
        printf("%lld ", enc[i]);
    }
    printf("\n\nDecrypted Message:\n");
    for(size_t i=0;i<len;i++){
        int dec = (int)modexp(enc[i], d, n);
        putchar((char)dec);
    }
    putchar('\n');
    return 0;
}

```

## Output:
<img width="818" height="482" alt="image" src="https://github.com/user-attachments/assets/cb76a7de-e703-43d0-b69c-5a65bfa38112" />

## Result:
 The program is executed successfully.

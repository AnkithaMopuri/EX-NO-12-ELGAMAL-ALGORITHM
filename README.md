# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h>
#include <math.h>


long long int power(long long int base, long long int exp, long long int mod) {
    long long int result = 1;
    for (int i = 0; i < exp; i++) {
        result = (result * base) % mod;
    }
    return result;
}

long long int modInverse(long long int a, long long int m) {
    a = a % m;
    for (long long int x = 1; x < m; x++) {
        if ((a * x) % m == 1)
            return x;
    }
    return 1;
}

int main() {
    long long int p, g, x, y, k, m, c1, c2, s, s_inv, decrypted;

    printf("Enter a large prime number (p): ");
    scanf("%lld", &p);
    printf("Enter primitive root of %lld (g): ", p);
    scanf("%lld", &g);

    printf("Enter private key (x): ");
    scanf("%lld", &x);

    y = power(g, x, p);
    printf("\nPublic key: (p = %lld, g = %lld, y = %lld)\n", p, g, y);
    printf("Private key: x = %lld\n", x);

    printf("\nEnter message (m): ");
    scanf("%lld", &m);
    printf("Enter random key (k): ");
    scanf("%lld", &k);

    c1 = power(g, k, p);
    c2 = (m * power(y, k, p)) % p;

    printf("\nCiphertext: (c1 = %lld, c2 = %lld)\n", c1, c2);

 
    s = power(c1, x, p);
    s_inv = modInverse(s, p);
    decrypted = (c2 * s_inv) % p;

    printf("\nDecrypted message: %lld\n", decrypted);

    return 0;
}

```


## Output:
<img width="580" height="379" alt="image" src="https://github.com/user-attachments/assets/b71e7ff7-dbe3-46dc-b588-c6de7525db0a" />



## Result:
The program is executed successfully.

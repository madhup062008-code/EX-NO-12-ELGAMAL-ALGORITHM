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

long long powerMod(long long base, long long exp, long long mod)
{
    long long result = 1;

    base = base % mod;

    while (exp > 0)
    {
        if (exp % 2 == 1)
            result = (result * base) % mod;

        base = (base * base) % mod;
        exp = exp / 2;
    }

    return result;
}

long long modInverse(long long a, long long p)
{
    long long i;

    for (i = 1; i < p; i++)
    {
        if ((a * i) % p == 1)
            return i;
    }

    return -1;
}

int main()
{
    long long p, g;
    long long x, y;
    long long m, k;
    long long c1, c2;
    long long s, sInverse;
    long long decrypted;
    printf("Enter prime number p: ");
    scanf("%lld", &p);

    printf("Enter primitive root g: ");
    scanf("%lld", &g);

    printf("Enter private key x: ");
    scanf("%lld", &x);
    y = powerMod(g, x, p);

    printf("\nPublic Key (p, g, y): (%lld, %lld, %lld)\n", p, g, y);
    printf("Private Key x: %lld\n", x);

    printf("\nEnter message m: ");
    scanf("%lld", &m);

    if (m <= 0 || m >= p)
    {
        printf("Message must satisfy 0 < m < p.\n");
        return 0;
    }

    printf("Enter random key k: ");
    scanf("%lld", &k);/
    c1 = powerMod(g, k, p);

    c2 = (m * powerMod(y, k, p)) % p;

    printf("\nEncrypted Ciphertext:\n");
    printf("c1 = %lld\n", c1);
    printf("c2 = %lld\n", c2);

    s = powerMod(c1, x, p);

    sInverse = modInverse(s, p);

    if (sInverse == -1)
    {
        printf("Modular inverse does not exist.\n");
        return 0;
    }

    decrypted = (c2 * sInverse) % p;

    printf("\nDecryption:\n");
    printf("Shared secret s = %lld\n", s);
    printf("Modular inverse of s = %lld\n", sInverse);
    printf("Decrypted message = %lld\n", decrypted);

    if (m == decrypted)
        printf("\nElGamal Encryption and Decryption Successful!\n");
    else
        printf("\nDecryption Failed!\n");

    return 0;
}
```

## Output:
<img width="706" height="636" alt="image" src="https://github.com/user-attachments/assets/7707a4e5-ebcc-4308-864e-4923d013437a" />


## Result:
The program is executed successfully.

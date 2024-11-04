# Exp-12-Elgamal-Algorithm

To encrypt and decrypt a message using the ElGamal encryption algorithm.

## Aim
To securely exchange a message between two users using the ElGamal encryption and decryption algorithm, implemented in C.

## Algorithm

### Step 1: Input Large Prime and Generator
- Bob inputs a large prime number `p` and a generator `g`.

### Step 2: Generate Public and Private Keys
- Alice selects a private key, `privateKeyA`.
- Alice computes her public key as:

### Step 3: Encrypt Message
- Bob inputs the message to be encrypted.
- Bob selects a random integer `k`.
- Bob computes the ciphertext:


### Step 4: Decrypt Message
- Alice receives `c1` and `c2` and decrypts the message using:


### Step 5: Verification
- The decrypted message is compared to the original message to confirm successful decryption.

## Code

Here is the implementation of the ElGamal encryption and decryption algorithm in C:

```c
#include <stdio.h>
#include <math.h>

// Function to compute modular exponentiation (base^exp % mod)
long long int modExp(long long int base, long long int exp, long long int mod) {
  long long int result = 1;
  while (exp > 0) {
      if (exp % 2 == 1) {
          result = (result * base) % mod;
      }
      base = (base * base) % mod;
      exp = exp / 2;
  }
  return result;
}

int main() {
  long long int p, g, privateKeyA, publicKeyA;
  long long int k, message, c1, c2, decryptedMessage;

  // Step 1: Input a large prime number (p) and a generator (g)
  printf("Enter a large prime number (p): ");
  scanf("%lld", &p);
  printf("Enter a generator (g): ");
  scanf("%lld", &g);

  // Step 2: Alice inputs her private key
  printf("Enter Alice's private key: ");
  scanf("%lld", &privateKeyA);

  // Step 3: Compute Alice's public key (publicKey = g^privateKeyA mod p)
  publicKeyA = modExp(g, privateKeyA, p);
  printf("Alice's public key: %lld\n", publicKeyA);

  // Step 4: Bob inputs the message to be encrypted and selects a random k
  printf("Enter the message to encrypt (as a number): ");
  scanf("%lld", &message);
  printf("Enter a random number k: ");
  scanf("%lld", &k);

  // Step 5: Bob computes ciphertext (c1 = g^k mod p, c2 = (message * publicKeyA^k) mod p)
  c1 = modExp(g, k, p);
  c2 = (message * modExp(publicKeyA, k, p)) % p;
  printf("Encrypted message (c1, c2): (%lld, %lld)\n", c1, c2);

  // Step 6: Alice decrypts the message (decryptedMessage = (c2 * c1^(p-1-privateKeyA)) mod p)
  decryptedMessage = (c2 * modExp(c1, p - 1 - privateKeyA, p)) % p;
  printf("Decrypted message: %lld\n", decryptedMessage);

  return 0;
}
```
## Output:
![image](https://github.com/user-attachments/assets/6a5ad72e-4424-4f6b-b927-a63f7733f2b0)

## Result:
The program for Elgamal encryption and decryption was exceuted successfully. Alice and Bob exchanged an encrypted message and verified that the decrypted message matched the original message.

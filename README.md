
==================================================
QUESTION 1: EUCLIDEAN ALGORITHM, EXTENDED EUCLIDEAN
ALGORITHM AND MODULAR OPERATIONS
==================================================

FULL QUESTION:
Implement a Python program for Euclidean Algorithm, extended version, and mod operations to solve a real-world cryptography problem.

AIM:
To implement Euclidean and Extended Euclidean algorithms and calculate modular operations using Python.

PROCEDURE:
1. Import the required functions.
2. Get two integer values.
3. Calculate GCD using Euclidean algorithm.
4. Calculate modular inverse using Extended Euclidean algorithm.
5. Display the results.

PROGRAM:

a = 17
b = 5
m = 26

# Euclidean Algorithm
x = a
y = b

while y != 0:
    x, y = y, x % y

print("GCD =", x)

# Modular Inverse
if x == 1:
    inverse = pow(a, -1, m)
    print("Modular Inverse =", inverse)

# Modular Operation
print("Modular Addition =", (a + b) % m)
print("Modular Multiplication =", (a * b) % m)

OUTPUT:

GCD = 1
Modular Inverse = 23
Modular Addition = 22
Modular Multiplication = 7

RESULT:
Thus, Euclidean algorithm, Extended Euclidean algorithm and modular operations were successfully implemented.


==================================================
QUESTION 2: FERMAT AND EULER THEOREMS
==================================================

FULL QUESTION:
Implement Fermat and Euler's Theorem. Verify the theorems and apply them for finding modular inverse using Python Program.

AIM:
To verify Fermat's Little Theorem and Euler's Theorem and calculate modular inverse.

PROCEDURE:
1. Get values of a, p and n.
2. Verify Fermat's theorem.
3. Calculate Euler's totient function.
4. Verify Euler's theorem.
5. Calculate the modular inverse.

PROGRAM:

import math

a = 3
p = 7
n = 10

# Fermat's Little Theorem
print("Fermat:", pow(a, p-1, p) == 1)

# Euler's Theorem
phi = sum(1 for i in range(1, n+1)
          if math.gcd(i, n) == 1)

print("Euler:", pow(a, phi, n) == 1)

# Modular Inverse
inverse = pow(a, -1, n)

print("Modular Inverse =", inverse)

OUTPUT:

Fermat: True
Euler: True
Modular Inverse = 7

RESULT:
Thus, Fermat's and Euler's theorems were verified and modular inverse was calculated successfully.


==================================================
QUESTION 3: FERMAT AND MILLER-RABIN PRIMALITY TESTS
==================================================

FULL QUESTION:
Implement Fermat and Miller-Rabin probabilistic primality tests using Python Program.

AIM:
To check whether a number is prime using Fermat and Miller-Rabin tests.

PROCEDURE:
1. Import the random module.
2. Get an integer value.
3. Perform Fermat primality testing.
4. Perform Miller-Rabin primality testing.
5. Display whether the number is probably prime or composite.

PROGRAM:

import random

def fermat(n):
    if n < 4:
        return n in (2, 3)

    for i in range(5):
        a = random.randint(2, n-2)

        if pow(a, n-1, n) != 1:
            return False

    return True


def miller(n):
    if n < 4:
        return n in (2, 3)

    d = n - 1
    s = 0

    while d % 2 == 0:
        d //= 2
        s += 1

    for i in range(5):
        a = random.randint(2, n-2)
        x = pow(a, d, n)

        if x == 1 or x == n-1:
            continue

        for j in range(s-1):
            x = pow(x, 2, n)

            if x == n-1:
                break
        else:
            return False

    return True


n = 17

print("Fermat:", fermat(n))
print("Miller-Rabin:", miller(n))

OUTPUT:

Fermat: True
Miller-Rabin: True

RESULT:
Thus, Fermat and Miller-Rabin primality tests were implemented successfully.

NOTE:
Both tests are probabilistic. Miller-Rabin is generally more reliable. Use sufficiently many rounds for large numbers.


==================================================
QUESTION 4: CHINESE REMAINDER THEOREM
==================================================

FULL QUESTION:
Implement a Python program for a system of congruences using Chinese Remainder Theorem.

AIM:
To solve a system of simultaneous congruences using CRT.

PROCEDURE:
1. Define the remainders.
2. Define the moduli.
3. Calculate the product of moduli.
4. Calculate the modular inverses.
5. Display the final solution.

PROGRAM:

from functools import reduce

remainders = [2, 3, 2]
moduli = [3, 5, 7]

M = reduce(lambda x, y: x*y, moduli)

result = 0

for a, m in zip(remainders, moduli):
    Mi = M // m
    inverse = pow(Mi, -1, m)
    result += a * Mi * inverse

result = result % M

print("Solution =", result)

for a, m in zip(remainders, moduli):
    print(result, "%", m, "=", result % m)

OUTPUT:

Solution = 23
23 % 3 = 2
23 % 5 = 3
23 % 7 = 2

RESULT:
Thus, the system of congruences was successfully solved using Chinese Remainder Theorem.


==================================================
QUESTION 5: SCHNORR IDENTIFICATION PROTOCOL
==================================================

FULL QUESTION:
Implement Schnorr Identification Protocol using Python Program.

AIM:
To implement the Schnorr identification protocol for user authentication.

PROCEDURE:
1. Select prime numbers and a generator.
2. Generate the prover's private and public keys.
3. Generate a random commitment.
4. Calculate the challenge and response.
5. Verify the response.

PROGRAM:

import secrets

p = 23
q = 11
g = 2

# Private key
x = 3

# Public key
y = pow(g, x, p)

# Commitment
r = secrets.randbelow(q-1) + 1
t = pow(g, r, p)

# Challenge
e = 4

# Response
s = (r + e*x) % q

# Verification
left = pow(g, s, p)
right = (t * pow(y, e, p)) % p

print("Public Key =", y)
print("Commitment =", t)
print("Response =", s)

print("Authentication:",
      left == right)

OUTPUT:

Public Key = 8
Commitment = (Random value)
Response = (Calculated value)
Authentication = True

RESULT:
Thus, Schnorr Identification Protocol was successfully implemented.

NOTE:
This is a simplified educational demonstration with a fixed challenge. A real protocol requires a fresh unpredictable challenge and suitable cryptographic parameters.


==================================================
QUESTION 6: FEIGE-FIAT-SHAMIR IDENTIFICATION PROTOCOL
==================================================

FULL QUESTION:
Implement Feige-Fiat-Shamir Identification Protocol using Python Program.

AIM:
To implement the Feige-Fiat-Shamir identification protocol for authentication.

PROCEDURE:
1. Select two prime numbers.
2. Calculate the modulus.
3. Generate private and public values.
4. Generate a random commitment and challenge.
5. Verify the prover's response.

PROGRAM:

import secrets

p = 7
q = 11
n = p * q

# Private key
s = 3

# Public key
v = pow(s, 2, n)

# Random value
r = 2

# Commitment
x = pow(r, 2, n)

# Challenge
e = 1

# Response
y = (r * pow(s, e, n)) % n

# Verification
check = (pow(y, 2, n) ==
         (x * pow(v, e, n)) % n)

print("Modulus =", n)
print("Public Key =", v)
print("Commitment =", x)
print("Response =", y)
print("Authentication =", check)

OUTPUT:

Modulus = 77
Public Key = 9
Commitment = 4
Response = 6
Authentication = True

RESULT:
Thus, Feige-Fiat-Shamir identification protocol was successfully implemented.

NOTE:
This is a single-round educational example. Production protocols require multiple rounds and carefully generated keys.


==================================================
QUESTION 7: DIGITAL SIGNATURE AND VERIFICATION
==================================================

FULL QUESTION:
Implement Digital Signature and verify the Signature using Python Program.

AIM:
To create and verify a digital signature using RSA.

PROCEDURE:
1. Select RSA prime numbers.
2. Generate public and private keys.
3. Create a message.
4. Sign the message using the private key.
5. Verify the signature using the public key.

PROGRAM:

import hashlib

p = 61
q = 53

n = p * q
phi = (p-1) * (q-1)

e = 17
d = pow(e, -1, phi)

message = "Hello Student"

h = int(hashlib.sha256(
    message.encode()).hexdigest(), 16) % n

signature = pow(h, d, n)

verified = pow(signature, e, n) == h

print("Message =", message)
print("Signature =", signature)
print("Verification =", verified)

OUTPUT:

Message = Hello Student
Signature = (Integer value)
Verification = True

RESULT:
Thus, RSA digital signature was created and verified successfully.

NOTE:
This is a small-number RSA demonstration, not secure for real-world signing. Use RSA-PSS with a cryptographic library in practical applications.


==================================================
QUESTION 8: ELGAMAL SIGNATURE SCHEME
==================================================

FULL QUESTION:
Implement Elgamal Signature Scheme using Python Program.

AIM:
To generate and verify a digital signature using ElGamal.

PROCEDURE:
1. Select a prime number and generator.
2. Generate private and public keys.
3. Select a random signing value.
4. Generate the digital signature.
5. Verify the signature.

PROGRAM:

import hashlib
import math

p = 23
g = 5

# Private key
x = 6

# Public key
y = pow(g, x, p)

message = "HELLO"

h = int(hashlib.sha256(
    message.encode()).hexdigest(), 16) % (p-1)

# Random signing value
k = 7

while math.gcd(k, p-1) != 1:
    k += 1

r = pow(g, k, p)

k_inv = pow(k, -1, p-1)

s = (k_inv * (h-x*r)) % (p-1)

left = pow(g, h, p)
right = (pow(y, r, p) * pow(r, s, p)) % p

print("Public Key =", y)
print("Signature =", r, s)
print("Verified =", left == right)

OUTPUT:

Public Key = 8
Signature = (r value) (s value)
Verified = True

RESULT:
Thus, ElGamal digital signature was generated and verified successfully.

NOTE:
Use fresh, secret signing nonces for every signature. This small-parameter program is for learning only.


==================================================
QUESTION 9: ELLIPTIC CURVE CRYPTOSYSTEM
==================================================

FULL QUESTION:
Implement Elliptic Curve Cryptosystem using Python Program.

AIM:
To demonstrate elliptic curve point operations and key generation.

PROCEDURE:
1. Define an elliptic curve.
2. Select a base point.
3. Generate a private key.
4. Calculate the public key.
5. Verify the generated public key.

PROGRAM:

p = 17
a = 2
b = 2

G = (5, 1)

def add(P, Q):

    if P is None:
        return Q

    if Q is None:
        return P

    x1, y1 = P
    x2, y2 = Q

    if x1 == x2 and (y1+y2) % p == 0:
        return None

    if P == Q:
        m = ((3*x1*x1+a) *
             pow(2*y1, -1, p)) % p
    else:
        m = ((y2-y1) *
             pow(x2-x1, -1, p)) % p

    x3 = (m*m-x1-x2) % p
    y3 = (m*(x1-x3)-y1) % p

    return (x3, y3)


def multiply(k, P):

    result = None

    while k:
        if k & 1:
            result = add(result, P)

        P = add(P, P)
        k >>= 1

    return result


private = 3
public = multiply(private, G)

print("Private Key =", private)
print("Public Key =", public)

OUTPUT:

Private Key = 3
Public Key = (10, 6)

RESULT:
Thus, elliptic curve point multiplication and public key generation were successfully implemented.

NOTE:
This is a toy ECC demonstration, not a complete secure ECIES encryption implementation.


==================================================
QUESTION 10: IDENTIFICATION PROTOCOL
==================================================

FULL QUESTION:
Implement any one identification protocol using Python program.

AIM:
To implement a simple challenge-response identification protocol.

PROCEDURE:
1. Define a shared secret.
2. Generate a random challenge.
3. Calculate the response.
4. Verify the response.
5. Display authentication status.

PROGRAM:

import hashlib
import secrets

secret = "mysecret"

challenge = secrets.token_hex(8)

response = hashlib.sha256(
    (secret + challenge).encode()
).hexdigest()

# Verifier calculates expected response
expected = hashlib.sha256(
    (secret + challenge).encode()
).hexdigest()

print("Challenge =", challenge)
print("Response =", response)

if response == expected:
    print("Authentication Successful")
else:
    print("Authentication Failed")

OUTPUT:

Challenge = (Random value)
Response = (SHA-256 hash)
Authentication Successful

RESULT:
Thus, a simple challenge-response identification protocol was implemented successfully.

NOTE:
This is a simplified demonstration, not a standardized authentication protocol. Real systems should use a secure HMAC-based challenge-response design.


==================================================
QUESTION 11: PSEUDO RANDOM AND CRYPTOGRAPHICALLY
SECURE RANDOM NUMBERS
==================================================

FULL QUESTION:
Implement pseudo random and cryptographically secure random numbers using Python Program.

AIM:
To generate pseudo-random and cryptographically secure random numbers.

PROCEDURE:
1. Import random and secrets modules.
2. Generate a pseudo-random number.
3. Generate a secure random number.
4. Display both numbers.
5. Compare their usage.

PROGRAM:

import random
import secrets

# Pseudo random number
random.seed(10)

a = random.randint(1, 100)

# Cryptographically secure random number
b = secrets.randbelow(100) + 1

print("Pseudo Random Number =", a)
print("Secure Random Number =", b)

OUTPUT:

Pseudo Random Number = 74
Secure Random Number = (Random value)

RESULT:
Thus, pseudo-random and cryptographically secure random numbers were generated successfully.


==================================================
QUESTION 12: FERMAT'S AND EULER'S THEOREMS WITH RSA
==================================================

FULL QUESTION:
Using Python, verify Fermat's Little Theorem and Euler's Theorem for different values of a, p, and n. Use Euler's theorem to find the modular inverse of a number used in RSA encryption.

AIM:
To verify Fermat's and Euler's theorems and calculate the RSA modular inverse.

PROCEDURE:
1. Define a, p and n.
2. Verify Fermat's theorem.
3. Calculate Euler's totient.
4. Verify Euler's theorem.
5. Calculate RSA private exponent.

PROGRAM:

import math

a = 3
p = 7
n = 10

print("Fermat Verification:",
      pow(a, p-1, p) == 1)

phi = sum(1 for i in range(1, n+1)
          if math.gcd(i, n) == 1)

print("Euler Verification:",
      pow(a, phi, n) == 1)

# RSA values
p = 11
q = 13

N = p * q
phi = (p-1) * (q-1)

e = 7
d = pow(e, -1, phi)

print("RSA Public Exponent =", e)
print("RSA Private Exponent =", d)

OUTPUT:

Fermat Verification: True
Euler Verification: True
RSA Public Exponent = 7
RSA Private Exponent = 103

RESULT:
Thus, Fermat's and Euler's theorems were verified and the RSA private exponent was calculated.


==================================================
QUESTION 13: LARGE INTEGER PRIMALITY TEST
==================================================

FULL QUESTION:
Write a program to determine whether a large integer is prime using (a) Fermat Test and (b) Miller-Rabin Test. Compare correctness and speed with CrypTool simulations.

AIM:
To identify prime numbers using Fermat and Miller-Rabin tests and compare their results.

PROCEDURE:
1. Enter a large integer.
2. Apply Fermat primality test.
3. Apply Miller-Rabin test.
4. Compare the results.
5. Record execution time.

PROGRAM:

import random
import time

def fermat(n):

    if n < 4:
        return n in (2, 3)

    for i in range(10):
        a = random.randint(2, n-2)

        if pow(a, n-1, n) != 1:
            return False

    return True


def miller(n):

    if n < 4:
        return n in (2, 3)

    d = n-1
    s = 0

    while d % 2 == 0:
        d //= 2
        s += 1

    for i in range(10):

        a = random.randint(2, n-2)
        x = pow(a, d, n)

        if x == 1 or x == n-1:
            continue

        for j in range(s-1):

            x = pow(x, 2, n)

            if x == n-1:
                break

        else:
            return False

    return True


n = 101

start = time.time()
f = fermat(n)
t1 = time.time()-start

start = time.time()
m = miller(n)
t2 = time.time()-start

print("Fermat Test =", f)
print("Miller Rabin =", m)
print("Fermat Time =", t1)
print("Miller Time =", t2)

OUTPUT:

Fermat Test = True
Miller Rabin = True
Fermat Time = (Execution time)
Miller Time = (Execution time)

COMPARISON:

Fermat:
Simple probabilistic test.

Miller-Rabin:
More reliable probabilistic test.

RESULT:
Thus, the primality of an integer was tested using Fermat and Miller-Rabin algorithms.

NOTE:
Execution times vary by computer and input. CrypTool comparison must be performed separately in the application.


==================================================
QUESTION 14: FEIGE-FIAT-SHAMIR ZERO-KNOWLEDGE
IDENTIFICATION PROTOCOL
==================================================

FULL QUESTION:
Simulate an identification scenario where a user (Prover) authenticates to a server (Verifier) using the Feige-Fiat-Shamir zero-knowledge protocol.

AIM:
To simulate user authentication using the Feige-Fiat-Shamir protocol.

PROCEDURE:
1. Generate the prover's private and public keys.
2. Calculate the modulus.
3. Generate a random commitment.
4. Server sends a challenge.
5. Verify the prover's response.

PROGRAM:

p = 7
q = 11
n = p*q

# Prover's private key
s = 3

# Public key
v = pow(s, 2, n)

# Random value
r = 2

# Commitment
x = pow(r, 2, n)

# Server challenge
e = 1

# Prover response
y = (r*s) % n

# Server verification
check = (
    pow(y, 2, n) ==
    (x*pow(v, e, n)) % n
)

print("Prover Commitment =", x)
print("Server Challenge =", e)
print("Prover Response =", y)
print("Authentication =", check)

OUTPUT:

Prover Commitment = 4
Server Challenge = 1
Prover Response = 6
Authentication = True

RESULT:
Thus, the Feige-Fiat-Shamir zero-knowledge identification protocol was simulated successfully.


==================================================
QUESTION 15: RABIN ONE-TIME SIGNATURE SCHEME
==================================================

FULL QUESTION:
Write a Python program to generate keys, sign a message, and verify the signature using the Rabin one-time signature scheme.

AIM:
To demonstrate Rabin signature key generation, signing and verification.

PROCEDURE:
1. Select two suitable prime numbers.
2. Calculate the public modulus.
3. Generate the private key factors.
4. Generate a signature for the message.
5. Verify the signature using the public key.

PROGRAM:

import hashlib

p = 7
q = 11

n = p*q

message = "HELLO"

def H(data):
    return int(hashlib.sha256(
        data.encode()).hexdigest(), 16) % n

# Find a message representative
salt = 0

while True:

    value = H(message + str(salt))

    if value != 0 and pow(value, (p-1)//2, p) == 1 \
       and pow(value, (q-1)//2, q) == 1:
        break

    salt += 1

# Square roots
mp = pow(value, (p+1)//4, p)
mq = pow(value, (q+1)//4, q)

# CRT
signature = (
    mq + q * ((mp-mq) * pow(q, -1, p) % p)
) % n

verified = pow(signature, 2, n) == value

print("Public Key =", n)
print("Salt =", salt)
print("Signature =", signature)
print("Verification =", verified)

OUTPUT:

Public Key = 77
Salt = (Calculated value)
Signature = (Calculated value)
Verification = True

RESULT:
Thus, a simplified Rabin signature was generated and verified successfully.

NOTE:
This is a textbook Rabin-style educational signature demonstration with a salted quadratic-residue representative. It is not a standardized production one-time signature scheme.


==================================================
QUESTION 16: PLAYFAIR CIPHER
==================================================

FULL QUESTION:
Use CrypTool 2 to implement the Playfair cipher to encrypt the message "ATTACK AT DAWN" and decrypt the message.

AIM:
To encrypt and decrypt a message using the Playfair cipher in CrypTool 2.

PROCEDURE:
1. Open CrypTool 2.
2. Select the Playfair cipher component.
3. Enter the key and plaintext.
4. Perform encryption.
5. Decrypt the ciphertext.

KEY:
MONARCHY

PLAINTEXT:
ATTACK AT DAWN

OUTPUT DIAGRAM:

+----------------------+
| Plaintext            |
| ATTACK AT DAWN       |
+----------------------+
           |
           v
+----------------------+
| Playfair Cipher      |
| Key: MONARCHY        |
+----------------------+
           |
           v
+----------------------+
| Ciphertext           |
| RSSRDEOSKQRA         |
+----------------------+
           |
           v
+----------------------+
| Playfair Decryption  |
+----------------------+
           |
           v
+----------------------+
| ATTACKATDAWN         |
+----------------------+

RESULT:
Thus, the Playfair cipher was used to encrypt and decrypt the given message.

NOTE:
Use I/J in the same square and remove spaces before encryption. The displayed ciphertext depends on the standard Playfair convention and key.


==================================================
QUESTION 17: AES ENCRYPTION IN ECB MODE
==================================================

FULL QUESTION:
Use CrypTool 2 to encrypt a file using the AES (Advanced Encryption Standard) algorithm in ECB mode.

AIM:
To encrypt a file using AES algorithm in ECB mode.

PROCEDURE:
1. Open CrypTool 2.
2. Create a new workspace.
3. Add a file input and AES encryption component.
4. Select ECB mode and enter the key.
5. Connect the components and execute.

OUTPUT DIAGRAM:

+------------------+
| Input File       |
| sample.txt       |
+------------------+
         |
         v
+------------------+
| AES Encryption   |
| Mode: ECB        |
| Key: 128-bit     |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
| Encrypted File   |
+------------------+

RESULT:
Thus, the given file was encrypted using AES in ECB mode.

NOTE:
ECB reveals patterns in repeated plaintext blocks and is not recommended for real-world file encryption.


==================================================
QUESTION 18: RSA ENCRYPTION AND DECRYPTION
==================================================

FULL QUESTION:
Using CrypTool 2, generate an RSA key pair. Encrypt a message with the public key and decrypt it with the private key.

AIM:
To generate an RSA key pair and perform encryption and decryption.

PROCEDURE:
1. Open CrypTool 2.
2. Add the RSA key generation component.
3. Generate public and private keys.
4. Encrypt the message using the public key.
5. Decrypt using the private key.

OUTPUT DIAGRAM:

+------------------+
| Plaintext        |
| HELLO STUDENT    |
+------------------+
         |
         v
+------------------+
| RSA Encryption   |
| Public Key       |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
+------------------+
         |
         v
+------------------+
| RSA Decryption   |
| Private Key      |
+------------------+
         |
         v
+------------------+
| HELLO STUDENT    |
+------------------+

RESULT:
Thus, RSA encryption and decryption were successfully performed using CrypTool 2.


==================================================
QUESTION 19: SHA-256, MD5 AND SHA-1
==================================================

FULL QUESTION:
In CrypTool 2, apply the SHA-256 hash function to the string "Semester Exam" and compare the resulting hash with an online SHA-256 generator. Experiment with the MD5 and SHA-1 hash functions.

AIM:
To generate and compare MD5, SHA-1 and SHA-256 hashes.

PROCEDURE:
1. Open CrypTool 2.
2. Enter "Semester Exam".
3. Add the SHA-256 hash component.
4. Generate MD5 and SHA-1 hashes.
5. Compare the results with an online hash generator.

OUTPUT DIAGRAM:

+----------------------+
| Input                |
| Semester Exam        |
+----------------------+
           |
           v
+----------------------+
| Hash Function        |
+----------------------+
     |       |       |
     v       v       v
+-------+ +-------+ +---------+
| MD5   | | SHA-1 | | SHA-256 |
+-------+ +-------+ +---------+
     |       |       |
     v       v       v
+----------------------+
| Hash Values          |
+----------------------+

OUTPUT:

MD5:
32 hexadecimal characters.

SHA-1:
40 hexadecimal characters.

SHA-256:
64 hexadecimal characters.

The online SHA-256 result must match CrypTool for the same exact input and encoding.

RESULT:
Thus, MD5, SHA-1 and SHA-256 hash values were generated and compared successfully.


==================================================
QUESTION 20: RSA DIGITAL SIGNATURE
==================================================

FULL QUESTION:
Use CrypTool 2 to create a digital signature for a message using RSA and a hashing algorithm of your choice (e.g., SHA-256). Verify the digital signature using the public key.

AIM:
To create and verify an RSA digital signature using SHA-256.

PROCEDURE:
1. Open CrypTool 2.
2. Generate an RSA key pair.
3. Enter the message.
4. Create the signature using the private key and SHA-256.
5. Verify using the public key.

OUTPUT DIAGRAM:

+------------------+
| Message          |
+------------------+
         |
         v
+------------------+
| SHA-256 Hash     |
+------------------+
         |
         v
+------------------+
| RSA Signing      |
| Private Key      |
+------------------+
         |
         v
+------------------+
| Digital Signature|
+------------------+
         |
         v
+------------------+
| RSA Verification |
| Public Key       |
+------------------+
         |
         v
+------------------+
| Valid Signature  |
+------------------+

RESULT:
Thus, the RSA digital signature was created and successfully verified using CrypTool 2.


==================================================
QUESTION 21: ELLIPTIC CURVE CRYPTOGRAPHY
==================================================

FULL QUESTION:
Using CrypTool 2, generate an ECC key pair and encrypt a message with the public key. Decrypt the message using the private key.

AIM:
To generate an ECC key pair and demonstrate public-key encryption and decryption.

PROCEDURE:
1. Open CrypTool 2.
2. Select ECC key generation.
3. Generate public and private keys.
4. Use an ECC-based encryption component.
5. Decrypt and verify the original message.

OUTPUT DIAGRAM:

+------------------+
| Plaintext        |
+------------------+
         |
         v
+------------------+
| ECC Encryption   |
| Public Key       |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
+------------------+
         |
         v
+------------------+
| ECC Decryption   |
| Private Key      |
+------------------+
         |
         v
+------------------+
| Original Message |
+------------------+

RESULT:
Thus, ECC-based encryption and decryption were demonstrated using CrypTool 2.

NOTE:
ECC key generation alone does not encrypt arbitrary messages. Use an ECIES or supported hybrid encryption component.


==================================================
QUESTION 22: DIFFIE-HELLMAN KEY EXCHANGE
==================================================

FULL QUESTION:
Using CrypTool 2, simulate the Diffie-Hellman key exchange algorithm. Explain how two parties can securely share a secret key over an insecure channel using Diffie-Hellman.

AIM:
To demonstrate secure shared key generation using Diffie-Hellman.

PROCEDURE:
1. Select a prime number and generator.
2. Generate Alice's private key.
3. Generate Bob's private key.
4. Exchange public keys.
5. Calculate and compare the shared secret.

OUTPUT DIAGRAM:

       PUBLIC VALUES
        p = 23
        g = 5

+----------------+       +----------------+
| Alice          |       | Bob            |
| Private = 6    |       | Private = 15   |
+----------------+       +----------------+
        |                         |
        v                         v
| Public = 8 |             | Public = 19 |
        |                         |
        +------ Exchange --------+
        |                         |
        v                         v
| Shared = 2 |             | Shared = 2  |

OUTPUT:

Alice Shared Key = 2
Bob Shared Key = 2

RESULT:
Thus, both parties generated the same shared secret using Diffie-Hellman key exchange.

NOTE:
Diffie-Hellman requires authentication to prevent man-in-the-middle attacks.


==================================================
QUESTION 23: IMAGE STEGANOGRAPHY
==================================================

FULL QUESTION:
Use CrypTool 2 to hide a secret message in an image file using Steganography Techniques.

AIM:
To hide a secret message inside an image using steganography.

PROCEDURE:
1. Open CrypTool 2.
2. Select image steganography components.
3. Load a cover image.
4. Enter the secret message.
5. Embed and extract the hidden message.

OUTPUT DIAGRAM:

+------------------+
| Cover Image      |
+------------------+
         |
         v
+------------------+
| Secret Message   |
+------------------+
         |
         v
+------------------+
| Steganography    |
| Embedding        |
+------------------+
         |
         v
+------------------+
| Stego Image      |
+------------------+
         |
         v
+------------------+
| Message Extract  |
+------------------+
         |
         v
+------------------+
| Secret Message   |
+------------------+

OUTPUT:

Original Image: image.png

Secret Message: HELLO

Stego Image: Generated successfully.

Extracted Message: HELLO

RESULT:
Thus, a secret message was successfully hidden and extracted from an image.


==================================================
QUESTION 24: CLASSICAL CIPHER TECHNIQUES
==================================================

FULL QUESTION:
Perform the Classical cipher techniques using CrypTool 2 and perform encryption and decryption.

AIM:
To perform classical encryption and decryption using CrypTool 2.

PROCEDURE:
1. Open CrypTool 2.
2. Select a classical cipher component.
3. Enter plaintext and key.
4. Perform encryption.
5. Decrypt and verify the plaintext.

OUTPUT DIAGRAM:

+------------------+
| Plaintext        |
| HELLO            |
+------------------+
         |
         v
+------------------+
| Classical Cipher |
| Caesar           |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
| KHOOR            |
+------------------+
         |
         v
+------------------+
| Decryption       |
+------------------+
         |
         v
+------------------+
| HELLO            |
+------------------+

RESULT:
Thus, classical cipher encryption and decryption were successfully performed.


==================================================
QUESTION 25: MODIFIED CAESAR CIPHER
==================================================

FULL QUESTION:
Using CrypTool 2, implement the Modified Caesar cipher for encrypting and decrypting a plaintext message. Encrypt the message "HELLO STUDENT" with a shift of 3 and decrypt the ciphertext back to plaintext using the Caesar cipher.

AIM:
To encrypt and decrypt a message using Caesar cipher with a shift of 3.

PROCEDURE:
1. Open CrypTool 2.
2. Select Caesar cipher.
3. Enter HELLO STUDENT.
4. Set the shift value to 3.
5. Encrypt and decrypt the message.

OUTPUT DIAGRAM:

+----------------------+
| Plaintext            |
| HELLO STUDENT        |
+----------------------+
           |
           v
+----------------------+
| Caesar Encryption    |
| Shift = 3            |
+----------------------+
           |
           v
+----------------------+
| Ciphertext           |
| KHOOR VWXGHQW        |
+----------------------+
           |
           v
+----------------------+
| Caesar Decryption    |
| Shift = 3            |
+----------------------+
           |
           v
+----------------------+
| HELLO STUDENT        |
+----------------------+

RESULT:
Thus, Caesar cipher encryption and decryption were successfully performed.


==================================================
QUESTION 26: SHA-256, MD5 AND SHA-1
==================================================

FULL QUESTION:
In CrypTool 2, apply the SHA-256 hash function to the string "Applied Cryptography" and compare the resulting hash with an online SHA-256 generator. Experiment with the MD5 and SHA-1 hash functions.

AIM:
To generate and compare SHA-256, MD5 and SHA-1 hashes.

PROCEDURE:
1. Open CrypTool 2.
2. Enter Applied Cryptography.
3. Select SHA-256.
4. Generate MD5 and SHA-1 hashes.
5. Compare the generated values.

OUTPUT DIAGRAM:

+------------------------+
| Applied Cryptography   |
+------------------------+
            |
            v
+------------------------+
| Hash Function          |
+------------------------+
      |       |       |
      v       v       v
   +------+ +------+ +--------+
   | MD5  | | SHA1 | | SHA256 |
   +------+ +------+ +--------+
      |       |       |
      v       v       v
+------------------------+
| Hash Values            |
+------------------------+

OUTPUT:

MD5 = 32 hexadecimal characters
SHA-1 = 40 hexadecimal characters
SHA-256 = 64 hexadecimal characters

RESULT:
Thus, different hash functions were successfully applied and compared.


==================================================
QUESTION 27: MAC AND SHA COMPARISON
==================================================

FULL QUESTION:
Using CrypTool 2, compare the MAC and SHA for the given string "Data Encryption" using Hash functions.

AIM:
To compare Message Authentication Code and SHA hash values.

PROCEDURE:
1. Open CrypTool 2.
2. Enter Data Encryption.
3. Select SHA-256.
4. Select HMAC-SHA-256 and enter a secret key.
5. Compare both outputs.

OUTPUT DIAGRAM:

             +------------------+
             | Data Encryption  |
             +------------------+
                      |
             +--------+--------+
             |                 |
             v                 v
       +-----------+     +-------------+
       | SHA-256   |     | HMAC-SHA256 |
       | No key    |     | Secret key  |
       +-----------+     +-------------+
             |                 |
             v                 v
       +-----------+     +-------------+
       | Hash      |     | MAC         |
       +-----------+     +-------------+

OUTPUT:

SHA-256: 256-bit hash value.

HMAC-SHA-256: 256-bit MAC value.

Both values are different because HMAC uses a secret key.

RESULT:
Thus, SHA and MAC were generated and compared successfully.

==================================================
QUESTION 28: DIGITAL SIGNATURE FOR A FILE
==================================================

FULL QUESTION:
Create a digital signature for a file using RSA (or DSA) and verify the signature using CrypTool Workspace.

AIM:
To create and verify a file's digital signature using RSA.

PROCEDURE:
1. Open CrypTool Workspace.
2. Load the file.
3. Generate an RSA key pair.
4. Sign the file using the private key.
5. Verify the signature using the public key.

OUTPUT DIAGRAM:

+------------------+
| Input File       |
+------------------+
         |
         v
+------------------+
| SHA-256 Hash     |
+------------------+
         |
         v
+------------------+
| RSA Signing      |
| Private Key      |
+------------------+
         |
         v
+------------------+
| Signature File   |
+------------------+
         |
         v
+------------------+
| Verification     |
| Public Key       |
+------------------+
         |
         v
+------------------+
| Valid Signature  |
+------------------+

RESULT:
Thus, a digital signature was created and verified using CrypTool Workspace.


==================================================
QUESTION 29: IMAGE STEGANOGRAPHY IN CRYPTOOL WORKSPACE
==================================================

FULL QUESTION:
Hide a message within an image file using steganography techniques available in CrypTool Workspace.

AIM:
To hide and extract a secret message inside an image file.

PROCEDURE:
1. Open CrypTool Workspace.
2. Load a cover image.
3. Enter a secret message.
4. Embed the message into the image.
5. Extract and verify the message.

OUTPUT DIAGRAM:

+------------------+
| Cover Image      |
+------------------+
         |
         v
+------------------+
| Secret Message   |
+------------------+
         |
         v
+------------------+
| Steganography    |
| Embedding        |
+------------------+
         |
         v
+------------------+
| Stego Image      |
+------------------+
         |
         v
+------------------+
| Extraction       |
+------------------+
         |
         v
+------------------+
| Secret Message   |
+------------------+

OUTPUT:

Secret Message: HELLO

Stego Image: Created.

Extracted Message: HELLO

RESULT:
Thus, image steganography was successfully performed using CrypTool Workspace.


==================================================
QUESTION 30: DIFFIE-HELLMAN KEY EXCHANGE
==================================================

FULL QUESTION:
Perform a key exchange using Diffie-Hellman key exchange algorithm using CrypTool Workspace.

AIM:
To perform a shared secret key exchange using Diffie-Hellman.

PROCEDURE:
1. Open CrypTool Workspace.
2. Select Diffie-Hellman algorithm.
3. Enter public parameters.
4. Generate private and public keys.
5. Exchange public keys and calculate the shared secret.

OUTPUT DIAGRAM:

+------------------+       +------------------+
| Alice            |       | Bob              |
| Private Key = 6  |       | Private Key = 15 |
+------------------+       +------------------+
         |                           |
         v                           v
+------------------+       +------------------+
| Public Key = 8   |       | Public Key = 19  |
+------------------+       +------------------+
         |                           |
         +--------- Exchange --------+
                     |
                     v
           +------------------+
           | Shared Secret    |
           | Same for both    |
           +------------------+

OUTPUT:

Alice Shared Secret = 2
Bob Shared Secret = 2

RESULT:
Thus, Diffie-Hellman key exchange was successfully performed.


==================================================
QUESTION 31: AES ENCRYPTION
==================================================

FULL QUESTION:
Encrypt a plaintext message using AES (Advanced Encryption Standard) with a key of your choice using CrypTool Workspace.

AIM:
To encrypt plaintext using the AES algorithm.

PROCEDURE:
1. Open CrypTool Workspace.
2. Enter a plaintext message.
3. Select AES encryption.
4. Enter a valid AES key.
5. Execute encryption and observe ciphertext.

OUTPUT DIAGRAM:

+------------------+
| Plaintext        |
| HELLO STUDENT    |
+------------------+
         |
         v
+------------------+
| AES Encryption   |
| Secret Key       |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
+------------------+

OUTPUT:

Plaintext: HELLO STUDENT

Algorithm: AES

Encrypted Output: Ciphertext generated successfully.

RESULT:
Thus, plaintext was successfully encrypted using AES.

NOTE:
AES supports 128, 192 and 256-bit keys. Select a supported mode and padding option in CrypTool.


==================================================
QUESTION 32: FILE HASH USING MD5 AND SHA-256
==================================================

FULL QUESTION:
Calculate the hash value of a file using different hash functions (e.g., MD5, SHA-256) and compare the results using CrypTool Workspace.

AIM:
To calculate and compare file hash values using MD5 and SHA-256.

PROCEDURE:
1. Open CrypTool Workspace.
2. Load a file.
3. Select the MD5 hash function.
4. Select the SHA-256 hash function.
5. Compare the generated hashes.

OUTPUT DIAGRAM:

+------------------+
| Input File       |
+------------------+
         |
         v
+------------------+
| Hash Functions   |
+------------------+
       |       |
       v       v
+----------+ +----------+
| MD5      | | SHA-256  |
+----------+ +----------+
       |       |
       v       v
+------------------+
| Hash Comparison  |
+------------------+

OUTPUT:

MD5: 128-bit hash.

SHA-256: 256-bit hash.

RESULT:
Thus, file hash values were calculated and compared using different hash algorithms.


==================================================
QUESTION 33: RSA / DSA DIGITAL SIGNATURE
==================================================

FULL QUESTION:
Create a digital signature for a file using RSA (or DSA) and verify the signature using CrypTool Workspace.

AIM:
To create and verify a file signature using RSA.

PROCEDURE:
1. Open CrypTool Workspace.
2. Select the file.
3. Generate RSA key pair.
4. Sign the file with the private key.
5. Verify the signature with the public key.

OUTPUT DIAGRAM:

+------------------+
| Input File       |
+------------------+
         |
         v
+------------------+
| SHA-256 Hash     |
+------------------+
         |
         v
+------------------+
| RSA Signing      |
+------------------+
         |
         v
+------------------+
| Digital Signature|
+------------------+
         |
         v
+------------------+
| Signature Check  |
+------------------+
         |
         v
+------------------+
| Verification     |
| Successful       |
+------------------+

RESULT:
Thus, a file was digitally signed and verified using CrypTool Workspace.


==================================================
QUESTION 34: RSA SIGNATURE WITH PREDEFINED PRIMES
==================================================

FULL QUESTION:
Create a digital signature for a file using RSA with predefined prime values and verify the signature using CrypTool Workspace.

AIM:
To create an RSA digital signature using predefined prime numbers.

PROCEDURE:
1. Open CrypTool Workspace.
2. Select two prime numbers.
3. Generate RSA public and private keys.
4. Sign the file using the private key.
5. Verify using the public key.

OUTPUT DIAGRAM:

+------------------+
| Prime Numbers    |
| p and q          |
+------------------+
         |
         v
+------------------+
| RSA Key Creation |
+------------------+
         |
         v
+------------------+
| File Hash        |
+------------------+
         |
         v
+------------------+
| RSA Signature    |
| Private Key      |
+------------------+
         |
         v
+------------------+
| Verification     |
| Public Key       |
+------------------+
         |
         v
+------------------+
| Valid Signature  |
+------------------+

OUTPUT:

RSA Key Pair: Generated.

File Signature: Created.

Verification: Successful.

RESULT:
Thus, RSA digital signature was created using predefined prime values and verified successfully.

NOTE:
Use small predefined primes only for a classroom demonstration. Production RSA keys must use large secure primes.


==================================================
QUESTION 35: PLAYFAIR CIPHER
==================================================

FULL QUESTION:
Use CrypTool 2 to implement the Playfair cipher to encrypt the message "MEET AT THE TOGA PARTY" and decrypt the message.

AIM:
To encrypt and decrypt the given plaintext using Playfair cipher.

PROCEDURE:
1. Open CrypTool 2.
2. Select Playfair cipher.
3. Enter the key.
4. Enter MEET AT THE TOGA PARTY.
5. Encrypt and decrypt the message.

KEY:
MONARCHY

PLAINTEXT:
MEET AT THE TOGA PARTY

OUTPUT DIAGRAM:

+--------------------------+
| Plaintext                |
| MEET AT THE TOGA PARTY   |
+--------------------------+
             |
             v
+--------------------------+
| Playfair Encryption      |
| Key: MONARCHY            |
+--------------------------+
             |
             v
+--------------------------+
| Ciphertext               |
| Generated by CrypTool    |
+--------------------------+
             |
             v
+--------------------------+
| Playfair Decryption      |
+--------------------------+
             |
             v
+--------------------------+
| Original Plaintext       |
+--------------------------+

RESULT:
Thus, the given message was encrypted and decrypted using Playfair cipher.

NOTE:
The question does not specify a key. MONARCHY is used as a demonstration key. Enter the same key for decryption.


==================================================
QUESTION 36: HILL CIPHER
==================================================

FULL QUESTION:
Use CrypTool 2 to implement the Hill cipher to encrypt the message "HARDWORK GIVES SUCCESS" and decrypt the message.

AIM:
To perform encryption and decryption using Hill cipher.

PROCEDURE:
1. Open CrypTool 2.
2. Select Hill cipher.
3. Enter the plaintext.
4. Enter a valid invertible key matrix.
5. Encrypt and decrypt the message.

KEY MATRIX:

3  3
2  5

OUTPUT DIAGRAM:

+--------------------------+
| Plaintext                |
| HARDWORK GIVES SUCCESS   |
+--------------------------+
             |
             v
+--------------------------+
| Hill Cipher              |
| Key Matrix               |
| 3  3                     |
| 2  5                     |
+--------------------------+
             |
             v
+--------------------------+
| Ciphertext               |
+--------------------------+
             |
             v
+--------------------------+
| Hill Decryption          |
+--------------------------+
             |
             v
+--------------------------+
| Original Plaintext       |
+--------------------------+

RESULT:
Thus, Hill cipher encryption and decryption were demonstrated using CrypTool 2.

NOTE:
The question does not specify a key matrix. The given matrix is invertible modulo 26. Padding and spaces must follow the selected component's settings.


==================================================
QUESTION 37: ASYMMETRIC KEY CRYPTOGRAPHIC ALGORITHMS
==================================================

FULL QUESTION:
Perform asymmetric key cryptographic algorithms using CrypTool Workspace.

AIM:
To demonstrate asymmetric encryption and decryption.

PROCEDURE:
1. Open CrypTool Workspace.
2. Select RSA algorithm.
3. Generate a public and private key pair.
4. Encrypt the message using the public key.
5. Decrypt using the private key.

OUTPUT DIAGRAM:

+------------------+
| Plaintext        |
+------------------+
         |
         v
+------------------+
| RSA Encryption   |
| Public Key       |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
+------------------+
         |
         v
+------------------+
| RSA Decryption   |
| Private Key      |
+------------------+
         |
         v
+------------------+
| Original Message |
+------------------+

RESULT:
Thus, asymmetric key cryptography was performed using CrypTool Workspace.


==================================================
QUESTION 38: TEXT STEGANOGRAPHY
==================================================

FULL QUESTION:
Perform Text Steganography using CrypTool 2 for the given text:

"This was also part of the routine. A few seconds of hesitation to see if something else would be added to the order before demurring and saying that would be all".

AIM:
To hide a secret message inside the given cover text using steganography.

PROCEDURE:
1. Open CrypTool 2.
2. Select text steganography.
3. Enter the given cover text.
4. Enter the secret message.
5. Hide and extract the message.

COVER TEXT:

This was also part of the routine. A few seconds of hesitation to see if something else would be added to the order before demurring and saying that would be all.

OUTPUT DIAGRAM:

+----------------------+
| Cover Text           |
+----------------------+
           |
           v
+----------------------+
| Secret Message       |
+----------------------+
           |
           v
+----------------------+
| Text Steganography   |
| Embedding            |
+----------------------+
           |
           v
+----------------------+
| Stego Text           |
+----------------------+
           |
           v
+----------------------+
| Message Extraction   |
+----------------------+
           |
           v
+----------------------+
| Secret Message       |
+----------------------+

OUTPUT:

Cover Text: Given paragraph.

Stego Text: Generated successfully.

Extracted Message: Same as the entered secret message.

RESULT:
Thus, text steganography was demonstrated using the given cover text.

NOTE:
The question does not specify the secret message. Enter a sample message such as HELLO for the demonstration.


==================================================
QUESTION 39: RSA DIGITAL SIGNATURE
==================================================

FULL QUESTION:
Use CrypTool 2 to create a digital signature for a message using RSA and a hashing algorithm of your choice. Verify the digital signature using the public key.

AIM:
To create and verify a digital signature using RSA and a hash function.

PROCEDURE:
1. Open CrypTool 2.
2. Enter a message.
3. Generate an RSA key pair.
4. Sign the message using SHA-256 and the private key.
5. Verify the signature using the public key.

OUTPUT DIAGRAM:

+------------------+
| Message          |
+------------------+
         |
         v
+------------------+
| SHA-256          |
+------------------+
         |
         v
+------------------+
| RSA Signing      |
| Private Key      |
+------------------+
         |
         v
+------------------+
| Signature        |
+------------------+
         |
         v
+------------------+
| Verification     |
| Public Key       |
+------------------+
         |
         v
+------------------+
| Valid            |
+------------------+

RESULT:
Thus, RSA digital signature was created and verified successfully.


==================================================
QUESTION 40: MODIFIED CAESAR CIPHER
==================================================

FULL QUESTION:
Using CrypTool 2, implement the Modified Caesar cipher for encrypting and decrypting a plaintext message. Encrypt the message "CRYPTOGRAPHY FUNCTIONS" with a shift of 3 and decrypt the ciphertext back to plaintext using the Caesar cipher.

AIM:
To encrypt and decrypt the given message using Caesar cipher with shift 3.

PROCEDURE:
1. Open CrypTool 2.
2. Select Caesar cipher.
3. Enter CRYPTOGRAPHY FUNCTIONS.
4. Set the shift value to 3.
5. Encrypt and decrypt the message.

OUTPUT DIAGRAM:

+--------------------------+
| Plaintext                |
| CRYPTOGRAPHY FUNCTIONS   |
+--------------------------+
             |
             v
+--------------------------+
| Caesar Encryption       |
| Shift = 3               |
+--------------------------+
             |
             v
+--------------------------+
| Ciphertext               |
| FUBSWRJUDSKB IXQFWLRQV   |
+--------------------------+
             |
             v
+--------------------------+
| Caesar Decryption       |
+--------------------------+
             |
             v
+--------------------------+
| CRYPTOGRAPHY FUNCTIONS  |
+--------------------------+

RESULT:
Thus, the given plaintext was successfully encrypted and decrypted using Caesar cipher.


==================================================
QUESTION 41: HILL CIPHER
==================================================

FULL QUESTION:
Use CrypTool 2 to implement the Hill cipher to encrypt the message "CIPHER BLOCK CHAINING" and decrypt the message.

AIM:
To encrypt and decrypt the given message using Hill cipher.

PROCEDURE:
1. Open CrypTool 2.
2. Select Hill cipher.
3. Enter CIPHER BLOCK CHAINING.
4. Enter an invertible key matrix.
5. Encrypt and decrypt the message.

KEY MATRIX:

3  3
2  5

OUTPUT DIAGRAM:

+--------------------------+
| Plaintext                |
| CIPHER BLOCK CHAINING    |
+--------------------------+
             |
             v
+--------------------------+
| Hill Encryption          |
| Key Matrix               |
+--------------------------+
             |
             v
+--------------------------+
| Ciphertext               |
+--------------------------+
             |
             v
+--------------------------+
| Hill Decryption          |
+--------------------------+
             |
             v
+--------------------------+
| Original Plaintext       |
+--------------------------+

RESULT:
Thus, Hill cipher encryption and decryption were successfully demonstrated.

NOTE:
The key matrix is a demonstration choice because the question does not specify one. Use identical padding and alphabet settings for encryption and decryption.


==================================================
QUESTION 42: MAC AND SHA COMPARISON
==================================================

FULL QUESTION:
Using CrypTool 2, compare the MAC and SHA for the given string "DIFFIE HELLMAN KEY EXCHANGE" using Hash functions.

AIM:
To compare SHA and MAC values for a given message.

PROCEDURE:
1. Open CrypTool 2.
2. Enter the given message.
3. Select SHA-256.
4. Select HMAC-SHA-256 and enter a key.
5. Compare the generated outputs.

OUTPUT DIAGRAM:

+----------------------------+
| DIFFIE HELLMAN KEY EXCHANGE|
+----------------------------+
              |
       +------+------+
       |             |
       v             v
+------------+ +-------------+
| SHA-256    | | HMAC-SHA256 |
+------------+ +-------------+
       |             |
       v             v
+------------+ +-------------+
| Hash Value | | MAC Value   |
+------------+ +-------------+

OUTPUT:

SHA-256: 256-bit hash.

HMAC-SHA-256: 256-bit authentication code.

RESULT:
Thus, SHA and MAC values were generated and compared successfully.


==================================================
QUESTION 43: RSA KEY GENERATION AND ENCRYPTION
==================================================

FULL QUESTION:
Using CrypTool 2, generate an RSA key pair with primality concept. Encrypt a message with the public key and decrypt it with the private key.

AIM:
To generate RSA keys using prime numbers and perform encryption and decryption.

PROCEDURE:
1. Open CrypTool 2.
2. Select two prime numbers.
3. Generate RSA public and private keys.
4. Encrypt a message using the public key.
5. Decrypt using the private key.

OUTPUT DIAGRAM:

+------------------+
| Prime Numbers    |
| p and q          |
+------------------+
         |
         v
+------------------+
| RSA Key Generation|
+------------------+
         |
         v
+------------------+
| Public Key       |
| Private Key      |
+------------------+
         |
         v
+------------------+
| Message          |
+------------------+
         |
         v
+------------------+
| RSA Encryption   |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
+------------------+
         |
         v
+------------------+
| RSA Decryption   |
+------------------+
         |
         v
+------------------+
| Original Message |
+------------------+

RESULT:
Thus, RSA key generation, encryption and decryption were performed successfully.


==================================================
QUESTION 44: SYMMETRIC KEY CRYPTOGRAPHIC ALGORITHMS
==================================================

FULL QUESTION:
Perform symmetric key cryptographic algorithms using CrypTool Workspace.

AIM:
To demonstrate symmetric key encryption and decryption.

PROCEDURE:
1. Open CrypTool Workspace.
2. Select AES encryption.
3. Enter a plaintext message.
4. Enter a secret key.
5. Decrypt using the same secret key.

OUTPUT DIAGRAM:

+------------------+
| Plaintext        |
| HELLO STUDENT    |
+------------------+
         |
         v
+------------------+
| AES Encryption   |
| Secret Key       |
+------------------+
         |
         v
+------------------+
| Ciphertext       |
+------------------+
         |
         v
+------------------+
| AES Decryption   |
| Same Secret Key  |
+------------------+
         |
         v
+------------------+
| HELLO STUDENT    |
+------------------+

RESULT:
Thus, symmetric key encryption and decryption were successfully performed using AES.


==================================================
QUESTION 45: RSA KEY GENERATION, FILE SIGNING AND
SIGNATURE VERIFICATION
==================================================

FULL QUESTION:
Write a Python program to:

a) Generate RSA (or DSA) key pair.
b) Sign a file.
c) Verify the signature.

Repeat the same steps using CrypTool and compare hash values and signatures.

AIM:
To generate RSA keys, digitally sign a file and verify the signature using Python and CrypTool.

PROCEDURE:
1. Generate an RSA public and private key pair.
2. Create a text file.
3. Sign the file using the private key.
4. Verify the signature using the public key.
5. Repeat the process in CrypTool and compare the results.

PROGRAM:

First install the library:

pip install cryptography

Python program:

from cryptography.hazmat.primitives.asymmetric import rsa
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.asymmetric import padding

# Generate RSA keys

private_key = rsa.generate_private_key(
    public_exponent=65537,
    key_size=2048
)

public_key = private_key.public_key()

# Create file

with open("message.txt", "w") as f:
    f.write("Hello Applied Cryptography")

# Read file

with open("message.txt", "rb") as f:
    data = f.read()

# Sign file

signature = private_key.sign(
    data,
    padding.PSS(
        mgf=padding.MGF1(hashes.SHA256()),
        salt_length=padding.PSS.MAX_LENGTH
    ),
    hashes.SHA256()
)

# Verify signature

try:

    public_key.verify(
        signature,
        data,
        padding.PSS(
            mgf=padding.MGF1(hashes.SHA256()),
            salt_length=padding.PSS.MAX_LENGTH
        ),
        hashes.SHA256()
    )

    print("Signature Verified Successfully")

except Exception:

    print("Signature Verification Failed")


OUTPUT:

Signature Verified Successfully


CRYPTOOL WORKSPACE COMPARISON:

1. Open CrypTool Workspace.
2. Generate RSA public and private keys.
3. Load the same message.txt file.
4. Create the SHA-256 hash.
5. Sign and verify the file.
6. Compare the hash and signature results.

OUTPUT DIAGRAM:

+------------------------+
| Input File             |
| message.txt            |
+------------------------+
            |
            v
+------------------------+
| SHA-256 Hash           |
+------------------------+
            |
            v
+------------------------+
| RSA Digital Signing    |
| Private Key            |
+------------------------+
            |
            v
+------------------------+
| Digital Signature      |
+------------------------+
            |
            v
+------------------------+
| RSA Verification       |
| Public Key             |
+------------------------+
            |
            v
+------------------------+
| Signature Verified     |
+------------------------+

COMPARISON:

Python:
RSA key pair generated.
SHA-256 used.
File signature verified.

CrypTool:
RSA key pair generated.
SHA-256 used.
File signature verified.

Note:
The exact hash should match if the same file bytes are used. The signature bytes may differ because RSA-PSS uses random salt.

RESULT:
Thus, RSA key generation, file signing and signature verification were successfully implemented using Python and CrypTool.

==================================================
END OF ALL 45 APPLIED CRYPTOGRAPHY QUESTIONS
==================================================

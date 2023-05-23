---
title: "3. Cryptography"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
math: true
---

# 3. Cryptography

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/ccc/y1/security/3-cryptography)

## What is Cryptography?

**Cryptography** is a way of turning plaintext into ciphertext.

Encrypting something links four elements together:

- The plaintext $m$
- The ciphertext $c$
- The key $k$
- The algorithm $E$

The encryption algorithm turns the plaintext into the ciphertext by means of the key, so

$$ c = E_k(m) $$

## Principles of Modern Cryptography

Modern algorithms abide by the following principles:

1. Large enough key space to resist exhaustive search
2. Resistant to frequency analysis
3. Small change in plaintext results in large change in ciphertext
4. Security depends only on secrecy of key, and not on the secrecy of the algorithm (Kerckhoff’s principle)

## Cryptographic Algorithms

Cryptographic algorithms come in two braod categories:

- **Symmetric Encryption**: Uses the same secret key to encipher and decipher messages
    - Encryption methods can be extremely efficient, requiring minimal processing
    - Both sender and receiver must possess the encryption key
    - If either copy of the key is compromised, an intermediate can decrypt and read messages
- **Asymmetric Encryption**: Uses two different but related keys to encrypt/decrypt messages
    - If Key A encrypts message, only Key B can decrypt
    - Highest value when one key serves as the private key and the other as the public key
    - Typically used to encrypt a symmetric session key rather than the plaintext messages

## Caesar Cipher

- Shift the outer wheel by $k$ letters
- Encrypt: Find each plaintext letter in the outer wheel and replace with letter below
- Decrypt: Find each ciphertext letter in the inner wheel and replace with letter above

### Exhaustive Search

Caesar cipher is susceptible to exhaustive search, which means every possibility can be tried until the correct solution is found.

## Substitution and Transposition

**Substitution**: Substitute one value for another

- Mono-alphabetic cipher (uses only one alphabet)
    - Each given input letter always substitutes to the same output letter
    - Decrypting is done by reversing the substitution/mapping
- Polyalphabetic (uses two or more alphabets)
    - For example: Vigenère cipher: a polyalphabetic code; made up of different Caesar ciphers

**Transposition**: Rearranages values within a block

## Symmetric Cryptosystems

Two common types:

- **Data Encryption Standard (DES)**:
    - Adopted by NIST in 1976 as federal standard
    - 64-bit block size, 56-bit key
    - Can be broken on a desktop PC in minutes
    - Triple DEs (3DES) extended the life-time of the DES algorithm
- **Advanced Encryption Standard (AES)**:
    - Developed to replace both DES and 3DES
    - Approved by NIST in 2001
    - Proposed by Rijmen and Daemon as the Rijndael cipher

### Primary Challenge of Symmetric Key Cryptography

The main problem is key distribution. Let $n$ be the number of parties who want to communicate:

- When $n = 2$, we need one key
- When $n = 3$, we need three keys
- When $n = 4$, we need six keys
- When $n = 5$, we need ten keys
- In general, we need $n \times (n - 1) / 2$ keys

### Diffie-Hellman Key Exchange

DH Key Exchange uses asymmetric encryption to exchange session keys. These are limited-use symmetric keys for temporary communications, using symmetric encryption.

DH based key establishment is incorporated into a number of standard protocols, such as:

- TLS/SSL (Transport Layer)
- IPSec (Network Layer)

## Asymmetric Cryptosystems

Two common types:

- **RSA**:
    - Developed by Rivest, Shamir, and Adleman in 1978
    - Based on number-theoretical properties of natural numbers
- **Elliptic Curves**:
    - Proposted independently in 1985 by Koblitz and Miller
    - Uses similar ideas to RSA but using elliptic curves instead
    - Same complexity as RSA but with smaller keys

### Simplified RSA

1. Choose two large primes $p$ and $q$, and calculate $n = p \times q$
2. From $n$ follow some maths steps to calculate the value of $e$ and $d$
3. Publish $n$ and $e$, keep $d$ secret and destroy $p$ and $q$
4. Encryption of $m$ is now $c = m^e (\text{mod } n)$
5. Decryption of $c$ is then $m = c^d (\text{mod } n)$

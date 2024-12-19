# CTF Week #11 (Weak Encryption)

## Task 1

#### 1. How can I use this ciphersuite to encrypt and decrypt data?

To use this ciphersuite for encrypting and decrypting data, you can rely on the three provided functions: gen() to generate a symmetric key, enc(k, m, nonce) to encrypt a plaintext m using the key k and a unique nonce, and dec(k, c, nonce) to decrypt a ciphertext c using the same key and nonce. The encryption uses AES in CTR mode, and the nonce ensures uniqueness. First, you generate a key using gen(), then encrypt a message by passing the key, plaintext, and nonce to enc. To decrypt, you pass the same key, ciphertext, and nonce to dec.

#### 2. How can I exploit the vulnerability to break the code?

The vulnerability in this ciphersuite lies in the weak key generation within the gen() function. The first 13 bytes of the key are fixed to \x00, and only the last 3 bytes are random, reducing the keyspace to 2^24. This allows an attacker to brute-force all possible keys efficiently. By iterating over all 2^24 possible keys, keeping the first 13 bytes fixed, and varying the last 3 bytes, it is possible to decrypt the ciphertext. The correct key can be identified when the decrypted plaintext matches the expected format, such as flag{xxxxxx}.

#### 3. How can I automate the process to ensure my attack finds the flag?

To automate this attack, you need to convert the provided nonce and ciphertext from hexadecimal to bytes, then iterate over all 2^24 possible keys. For each key, you combine 13 fixed bytes of \x00 with 3 bytes representing the current iteration. Using the dec function, you decrypt the ciphertext with the generated key and nonce. The script should check if the decrypted plaintext matches the expected format (e.g., flag{...}). When it does, the flag is found, and the process stops. This can be implemented efficiently in Python with a brute-force loop that systematically tests all key combinations and verifies the result.


## Task 2

## Task 3


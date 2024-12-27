# CTF Week #12 (RSA)

We created a file ```ctf12.py``` to exploit the structure of the public key.

```

import random

# Miller-Rabin primality test algorithm
def is_prime(n, rounds=40):
    if n <= 1:
        return False
    if n <= 3:
        return True
    if n % 2 == 0:
        return False
    
    r, d = 0, n - 1
    while d % 2 == 0:
        r += 1
        d //= 2

    for _ in range(rounds):
        base = random.randint(2, n - 2)
        result = pow(base, d, n)
        if result == 1 or result == n - 1:
            continue
        for _ in range(r - 1):
            result = pow(result, 2, n)
            if result == n - 1:
                break
        else:
            return False
    return True

# Find primes near a given number and factor n
def find_nearby_primes(n, offset, limit=1000000000):
    t = 500 + offset
    guess = 2 ** t
    
    for delta in range(0, limit):
        p = guess + delta
        if is_prime(p):
            q = n // p
            if n % p == 0 and is_prime(q):
                return p, q
    raise ValueError("Primes not found in range.")

# Extended Euclidean algorithm to find the modular inverse
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    g, x1, y1 = extended_gcd(b, a % b)
    x = y1
    y = x1 - (a // b) * y1
    return g, x, y

# RSA decryption function
def decrypt_rsa(ciphertext, e, n):
    t = 5
    g = 6
    offset = ((t - 1) * 10 + g) // 2
    p, q = find_nearby_primes(n, offset)

    phi = (p - 1) * (q - 1)
    
    _, d, _ = extended_gcd(e, phi)
    d = d % phi
    if d < 0:
        d += phi

    int_ciphertext = int.from_bytes(ciphertext, "little")
    int_plaintext = pow(int_ciphertext, d, n)
    plaintext = int_plaintext.to_bytes((int_plaintext.bit_length() + 7) // 8, 'little')
    return plaintext

# Given public key
e = 65537
n = 1508014301265110212210531135789433919262563062937126445449153766240405586123431823342743394534566435927056356253600209291203385124994765794776479899441737868872418546363079183633889401000409025783035022042209594356324645754050314395741227749602215727578172965940314548672011863667276355354828366761595433318608404057

# Given ciphertext in hexadecimal format
ciphertext_hex = 'e1d89459183d7251219492588d712db792ff44ad2f414abb3c5c71de510f62594cb9c622c970b0a9130913c6768836055499eeea6b4fdab8612b8c822ed410747442c9147938c0e3f04a8cee987efae955627508a2c60eb21b5c9b8f73c3206bdbf08528e31a733ddc94e4cf2dddf3566f16a3ba48ab67c89e17c4fa8bbed950a3c3080000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000'

# Convert the hexadecimal ciphertext to bytes
ciphertext = bytes.fromhex(ciphertext_hex)

# Decrypt the ciphertext
plaintext = decrypt_rsa(ciphertext, e, n)

# Display the decrypted message
print("Decrypted message:", plaintext.decode('utf-8', errors='ignore'))

```


The modulus ```n``` is the product of two large primes, ```p``` and ```q```. By implementing an offset-based heuristic, we searched for nearby primes that divide n evenly. Once we found ```p``` and ```q```, we calculated Euler's totient function, ```φ(n) = (p-1)(q-1)```.

Using the Extended Euclidean Algorithm, we derived the modular inverse of the public exponent ```e``` modulo ```φ(n)```, obtaining the private key ```d```. With this, we converted the given ciphertext from hexadecimal format to bytes and then to an integer. Using modular exponentiation with ```d``` and ```n```, we decrypted the integer into plaintext bytes.

Then, we converted the plaintext bytes into a readable format to reveal the flag.

After running the Python script, the flag was successfully found and printed.

![Image 1.](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/CTF12_flag.png)


---
title: Hash Functions and PBKDF2 for Secure Passwords
description: 
published: true
date: 2023-02-01T03:38:39.152Z
tags: 
editor: markdown
dateCreated: 2023-02-01T03:38:35.465Z
---

- [보안 암호를 위한 해시 함수 및 PBKDF2***Korean** version of this document is available*](/ko/Knowledge-base/Backend/hash-functions-and-pbkdf2-for-secure-passwords)
{.links-list}
- [安全なパスワードのためのハッシュ関数と PBKDF2***Japanese** version of this document is available*](/ja/Knowledge-base/Backend/hash-functions-and-pbkdf2-for-secure-passwords)
{.links-list}
- [用于安全密码的哈希函数和 PBKDF2***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Backend/hash-functions-and-pbkdf2-for-secure-passwords)
{.links-list}




As a developer, you are probably familiar with hashing functions. A hashing function is a mathematical algorithm that maps data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management. In this article, we will discuss how hashing functions can be used to store passwords securely, and how the PBKDF2 algorithm can be used to make them even more secure.

When a user creates a new account on a website, they are typically asked to provide a password. This password is then stored in the database, usually in plain text. This is not secure, because if the database is compromised, the attacker would have access to all of the passwords.

A better solution is to hash the passwords before storing them in the database. When a user tries to log in, the website will hash the password they entered and compare it to the hash stored in the database. If the two hashes match, the user is authenticated.

One of the most popular hashing algorithms is MD5. However, it is not secure, because it is possible to create collisions, where two different inputs produce the same output. This means that an attacker could create a password that would be stored as the same hash as the real password, and gain access to the account.

A more secure hashing algorithm is SHA-256. SHA-256 is used in many applications, such as digital signatures and message authentication. It is also used in the Bitcoin protocol.

When storing passwords, it is important to use a salt. A salt is a random string of data that is used as an additional input to a hashing function. Salts are used to defeat rainbow table attacks. A rainbow table is a precomputed table of hash values for common passwords. If a password is hashed without a salt, an attacker could use a rainbow table to look up the hash and find the password. By using a salt, the attacker would have to compute the hash for each password in the table, which is much more time-consuming.

The PBKDF2 (Password-Based Key Derivation Function 2) algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The more iterations that are used, the more time-consuming the computation is, and the more resistant to brute-force attacks. However, the number of iterations should not be too high, because that would make the computation too slow for practical use.

In summary, hashing functions are a key ingredient in password security. They are used to map data of arbitrary size to a fixed size. The output of a hash function is called a hash value or simply a hash.

Hashing is used in many applications, such as digital signatures, message authentication codes, and data integrity. It is also a key ingredient in password storage and management.

The PBKDF2 algorithm is a standard for deriving keys from passwords. It is a part of the RSA Laboratories Public-Key Cryptography Standards (PKCS) series.

PBKDF2 is designed to be resistant to dictionary attacks and brute-force guessing attacks. It uses a pseudorandom function and a salt to compute the derived key. The pseudorandom function can be any cryptographic hash function, such as SHA-256.

The salt is used to protect against dictionary attacks. A dictionary attack is an attack where the attacker tries to guess the password by trying common words and phrases. By using a salt, the attacker would have to compute the hash for each password in the dictionary, which is much more time-consuming.

PBKDF2 is also designed to be resistant to brute-force guessing attacks. A brute-force attack is an attack where the attacker tries to guess the password by trying every possible combination of characters. By using a salt and a high number of iterations, PBKDF2 makes it computationally infeasible for an attacker to try every possible combination.

The number of iterations is an important parameter in PBKDF2. The
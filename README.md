# Password Cracking with Hashcat

This project demonstrates the process of cracking weak password hashes using dictionary and brute-force attacks with Hashcat in a Kali Linux environment.

---

## 📁 Files in This Repository

* `hashes.txt`: The list of target MD5 hashes.
* `cracked.txt`: The output file from Hashcat containing the successfully cracked passwords.
* `screenshot-dictionary-attack.png`: (Optional) A screenshot showing the successful dictionary attack.
* `screenshot-brute-force.png`: (Optional) A screenshot showing the brute-force attack.

---

## 🎯 Attack Strategy

My strategy involved a two-phase approach to maximize efficiency:

1.  **Dictionary Attack**: I first performed a dictionary attack using the well-known `rockyou.txt` wordlist. This is the most effective initial step, as many users choose common passwords found in this list. This method was fast and successfully cracked the common passwords.
    * **Command:** `hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt --outfile cracked.txt`

2.  **Brute-Force Attack**: To demonstrate a different method, I also conducted a targeted brute-force attack. I used a specific mask (`?l?l?l?d?d`) that matched a known password pattern. This shows how an attacker can crack passwords if they have some knowledge of the password's structure, but it is much slower for longer, more complex passwords.

---

## 💡 Key Learnings and Defense Strategies

This task provided clear insight into how easily weak passwords can be compromised and, more importantly, how to defend against these attacks.

### How Weak Passwords are Cracked

* **Speed:** Common, dictionary-based passwords can be cracked in seconds. My dictionary attack proved this by instantly finding passwords like `password123` and `sunshine`.
* **Predictability:** Short passwords or those with simple patterns (like `abc12`) are trivial to crack with a targeted brute-force attack because the number of possible combinations is very small.

### How to Defend Against Such Attacks

Based on these findings, here are the best practices for robust password security:

1.  **Use Long and Complex Passwords:** Aim for passwords that are at least 16 characters long and include a mix of uppercase letters, lowercase letters, numbers, and symbols. This exponentially increases the time required for a brute-force attack.
2.  **Avoid Dictionary Words:** Never use common words, names, or phrases found in a dictionary, as these are the first things an attacker will try.
3.  **Use a Password Manager:** A password manager can generate and store highly complex, unique passwords for every account, which is the most practical way to maintain strong security.
4.  **Enable Multi-Factor Authentication (MFA):** MFA is the single most effective defense. Even if an attacker cracks your password, they cannot access your account without the second factor (e.g., a code from your phone).
5.  **For Developers (Salting):** On the server side, always use a strong hashing algorithm (like Argon2 or bcrypt) and **salt** every password. Salting adds a unique random string to each password before hashing, making pre-computed attacks like rainbow tables useless.

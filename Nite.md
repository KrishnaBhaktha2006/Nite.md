# La Casa De Papel

*Flag:* nite{El_Pr0f3_0f_Prec1s10n_Pl4ns}

How you approached the challenge:

- step 1: I actually Started reading the source code that is given below
```
import hashlib
import base64
import pyfiglet

def secret():
    return "XXXXXXXXXXXXXXXXXXXXX"  # Length = 21

def md5(secret, msg):
    hash = hashlib.md5(secret + msg).hexdigest().encode()
    return base64.b64encode(hash).decode()

def menu(secret):
    while True:
        print("\n1. Practice Convo")
        print("2. Let's Fool Alice!")
        print("3. Crack the Vault")
        print("4. Exit")
        choice = input("Choose an option: ")
        if choice == '1':
            practice_convo(secret)
        elif choice == '2':
            fool_alice(secret)
        elif choice == '3':
            crack_the_vault()
        elif choice == '4':
            print("Exiting...")
            break
        else:
            print("Invalid choice. Please try again.")

def practice_convo(secret):
    message = input("Send a message: ")
    hash = md5(secret, message.encode('latin-1'))
    print(f"Here is your encrypted message: {hash}")

def fool_alice(secret):
    print("\nBot: Okay, let's see if you're the real deal. What's your name?")
    user_name = input("Your name: ").encode('latin-1')
    user_name = user_name.decode('unicode_escape').encode('latin-1')
    print("\nBot: Please provide your HMAC")
    user_hmac = input("Your HMAC: ").encode('latin-1')

    if b"Bob" in user_name:
        hash = base64.b64decode(md5(secret, user_name))
        if user_hmac == hash:
            print("\nAlice: Oh hey Bob! Here is the vault code you wanted:")
            with open('secret.txt', 'r') as file:
                secret_content = file.read()
                print(secret_content)
        else:
            print("\nAlice: LIARRRRRRR!!")
    else:
        print("\nAlice: IMPOSTERRRR")

def crack_the_vault():
    print("\nVault Person: Enter password")
    passs = input("Password: ")

    with open('secret.txt', 'r') as file:
        secret_content = file.read().strip()
        if passs == secret_content:
            with open('flag.txt', 'r') as flag_file:
                flag_content = flag_file.read().strip()
                print(f"\nVault Unlocked! The flag is: {flag_content}")
        else:
            print("Incorrect password!")

if _name_ == "_main_":
    secret_key = secret().encode()
    ascii_art = pyfiglet.figlet_format("La Casa de Papel")
    print(ascii_art)
    menu(secret_key)
```
so on reading this u can tell that Basically first we need to click 1 and enter a message now that message is sent in a func called md5 and after that we need to click 2 and type something and it stores it in var user_hash then it base 64's the md5 of user_hash and store it in var hash
so now basically if the user_hash == hash we get a password which can be used to open the vault when we click 3 .And i forgot to mention that for click 2 that is username it must have the word Bob in it
This is the basic understanding of the question.

- step 2: There are 3 ways of doing this,
First: Write anything for message after that for name write anything that involves Bob and then user some tools for md5 and base 64 and enter it and u should get the flag.<br>
Second: Here we need to waste a try enter a message containing Bob write the hash down somewhere and after wards for the next try the message of the first try will be the the user_hash but without the base 64 so ye this will also give u the flag.<br>
Third: This is my solution that is we keep the message and username as the same thing so that for user_hash == hash we just need to base 64 the hash which they provided and that on continuing gives you flag 

- step 3: I eneter user name as AliceBob and it gave me this as hash "ZWZjZGE3MzcyZGZjZDcwOWYxYTFlMDI1YmZlYjFiOGM=" So now i had to just enter the user_hash as the base 64 of this that is "efcda7372dfcd709f1a1e025bfeb1b8c" on doing i got the password as "G0t_Th3_G0ld_B3rl1nale"
on the entering as the vault password it gave the flag as "nite{El_Pr0f3_0f_Prec1s10n_Pl4ns}"

![WhatsApp Image 2024-12-14 at 23 25 09_d6dfe83f](https://github.com/user-attachments/assets/44037e82-5e0a-4675-a849-744e3fbd5abf)

What you learned through solving this challenge:

1. Analyse the Question correctly 

Other incorrect methods you tried:

- No incorrect methods tried

References

- No references

<hr>
<hr>

# Cybernotes

*Flag:* nite{7rY_XKcD_S3b_f0R_3xPl4nA7i0n}


**I have not Solved this challenge**


How you approached the challenge:

- step 1: Actually in start i had tried some random stuff like /robots.txt and stuff and /uploads worked!! and so after tht there i got like 8 files and on opening log 1 i got the username and password.

- step 2: Then i went back to login page and entered the credentials to get a page having like 4 notes and then i was stuck. Apparently on setting up the dockerfile we get our secret jwt key and on opening burpsuite with this username and password should give us a token and on refreshing the page while proxy is turned on, then send the request to repeater, where you’ll see the original token, change it to the one we got, then send it and ye we should get the flag!

What you learned through solving this challenge:

1. About Jwt keys
2. About tokens

Other incorrect methods you tried:

- I tried Sqli 
- Nmap
- Gobuster
- Even after using numerous tools i wasnt able to search the vulnerability.

References

- https://github.com/Cryptonite-MIT/niteCTF-2024/tree/main/webex/cybernotes
- https://abuctf.github.io/posts/NiteCTF2024/#web-exploitation

<hr>
<hr>

# U Are T Detective

*Flag:* nite{n0n_std_b4ud_r4t3s_ftw}


**I have not solved this challenge**


How you approached the challenge:

- step 1: In this challenge i had downloaded sigrok pulseview and opened sigmal.sr but had no idea how to continue apparently just seeing the ups and down like fe sub we can get binary codes

- step 2:And after that going to terminal opening python3 and writing this.
```
>>> binary = ('01101110','01101001','01110100','01100101', '01111011','01101110','00110000','01101110','01011111','01110011','01110100','01100100','01011111','01100010','00110100','01110101','01100100','01011111','01110010','00110100','01110100','00110011','01110011','01011111','01100110','01110100', '01110111', '01111101')
>>> convert = [chr(int(b, 2)) for b in binary]
>>> ascii = ''.join(convert)
>>> print(ascii)
nite{n0n_std_b4ud_r4t3s_ftw}
```
Should give the flag!

What you learned through solving this challenge:

1. I think if i thought about it for a little longer and not given up i would have gotten the flag

Other incorrect methods you tried:

- No incorrect methods tried

References

- https://github.com/Cryptonite-MIT/niteCTF-2024/tree/main/hardware/u-are-t-detective
- https://abuctf.github.io/posts/NiteCTF2024/#u-are-t-detective

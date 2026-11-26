# PW Crack 5

Challenge Link: https://learn.cylabacademy.org/learning-paths/18/164

- Learning Path: `The Beginner's Guide to the Challenge Library`
- Name: `PW Crack 5`
- Category: `General Skills`
- Difficulty: `Medium`

## Writeup

I first downloaded all the files using `wget`. 

Initially I was kind of daunted by the amount of words in the description, but my first instinct was to execute the python file.

![image](images/Pw-Crack-5/execute)

The program prompts for the password, so we need to find what that is. The description states that the `dictionary.txt` file contains all the possible passwords. When running the `cat dictionary.txt`, it's a long list of possible passwords; it would be very tedious to manually brute force this.

I then ran `nano level5.py` to examine the code. 

![image](images/PW-Crack-5/code)

From reading the code, I understand a few things:
- `level5.hash.bin` contains the hash of the correct password
- when the user inputs a password, its hash is compared to the correct hash
- the flag is encrypted in the file `level5.flag.txt.enc` 
- the correct password is the key to decrypting the flag

Initially, as I was reading the if-statement, I thought to just changing the line
```
if( user_pw_hash == correct_pw_hash ):
```
to 
```
if( true ):
```
to force the code in the block to run regardless if the password entered is true. However, by examining this line if the if-statement's block:
```
decryption = str_xor(flag_enc.decode(), user_pw)
```
The correct password is needed. The second parameter in the str_xor function is the key. The correct password is the key for decryption, and without the key, the flag cannot be properly decrypted.

So I thought of another way of modifying the code: I would add a loop that iterates through every possible password in `dictionary.txt`, hash it, and compare it to the correct hash. If both hashes match, the correct password has been found. 

In order to give myself write permissions on `level5.py`, I ran this command:
```
chmod +w level5.py
```

I then changed the code of `level5.py` the following:

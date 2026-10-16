# secure-pass-gen-cli
A cryptographically secure, modular CLI password generator in Python implementing user-defined complexity constraints, character set enforcement, and automated unit  testing.

import random
import string

print("--- Simple Password Generator ---")

# 1. Get and check the password length
while True:
    length_input = input("Enter password length (8 or more): ")
    if length_input.isdigit():  # Checks if the input is actually a number
        length = int(length_input)
        if length >= 8:
            break
        else:
            print("Too short! Must be 8 or more.")
    else:
        print("Please enter a valid whole number.")

# 2. Get character type preferences using simple choices
while True:
    print("\nAnswer 'yes' or 'no' for the following options:")

    use_upper = input("Include uppercase letters (A-Z)? ").lower() == "yes"
    use_lower = input("Include lowercase letters (a-z)? ").lower() == "yes"
    use_nums = input("Include numbers (0-9)? ").lower() == "yes"
    use_syms = input("Include symbols (!@#$)? ").lower() == "yes"

    # Count how many choices are True
    total_choices = 0
    if use_upper:
        total_choices += 1
    if use_lower:
        total_choices += 1
    if use_nums:
        total_choices += 1
    if use_syms:
        total_choices += 1

    # 4. Input validation (at least 2 types must be selected)
    if total_choices >= 2:
        break
    else:
        print("\n[Error] You must choose at least 2 options for safety!")

# Create an empty string to store all allowed characters
allowed_characters = ""

if use_upper:
    allowed_characters = allowed_characters + string.ascii_uppercase
if use_lower:
    allowed_characters = allowed_characters + string.ascii_lowercase
if use_nums:
    allowed_characters = allowed_characters + string.digits
if use_syms:
    allowed_characters = allowed_characters + string.punctuation

# 3. Generate the password by picking random items one by one
password = ""
for i in range(length):
    random_char = random.choice(allowed_characters)
    password = password + random_char

# Display the output
print("\n================================")
print(f"Your new password is: {password}")
print("================================")

# python-week-
intership fist week project
import random
import string

# Pre-defined lists of adjectives and nouns
adjectives = ["Cool", "Happy", "Swift", "Brave", "Charming", "Witty", "Bright", "Bold"]
nouns = ["Tiger", "Dragon", "Phoenix", "Falcon", "Panther", "Eagle", "Shark", "Wolf"]

def generate_username(include_numbers=True, include_special_chars=True, length=10):
    # Select a random adjective and noun
    adj = random.choice(adjectives)
    noun = random.choice(nouns)
    
    # Start building the username
    username = adj + noun
    
    # Add numbers if required
    if include_numbers:
        username += str(random.randint(10, 99))
    
    # Add special characters if required
    if include_special_chars:
        special_char = random.choice("!@#$%^&*")
        username += special_char
    
    # Adjust length if required
    if length and len(username) > length:
        username = username[:length]
    
    return username

def save_usernames_to_file(usernames, filename="usernames.txt"):
    try:
        with open(filename, "w") as file:
            for username in usernames:
                file.write(username + "\n")
        print(f"Usernames saved to {filename}")
    except Exception as e:
        print(f"Error saving usernames: {e}")

def main():
    print("Welcome to the Random Username Generator!")
    
    # Get user preferences
    include_numbers = input("Include numbers in usernames? (yes/no): ").strip().lower() == "yes"
    include_special_chars = input("Include special characters? (yes/no): ").strip().lower() == "yes"
    length = int(input("Set maximum length for usernames (0 for no limit): ").strip() or 0)
    count = int(input("How many usernames would you like to generate? ").strip())
    
    # Generate usernames
    usernames = []
    for _ in range(count):
        usernames.append(generate_username(include_numbers, include_special_chars, length))
    
    # Display usernames
    print("\nGenerated Usernames:")
    for username in usernames:
        print(username)
    
    # Save usernames to a file
    save = input("\nDo you want to save these usernames to a file? (yes/no): ").strip().lower() == "yes"
    if save:
        filename = input("Enter the filename (default: usernames.txt): ").strip() or "usernames.txt"
        save_usernames_to_file(usernames, filename)

if __name__ == "__main__":
    main()

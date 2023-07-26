import random
import string
import multiprocessing

def generate_random_alphanumeric(length):
    letters_and_digits = string.ascii_uppercase + string.digits
    return ''.join(random.choice(letters_and_digits) for _ in range(length))

def generate_random_strings(num_strings, min_length, max_length):
    pool = multiprocessing.Pool()
    lengths = [random.randint(min_length, max_length) for _ in range(num_strings)]
    results = pool.map(generate_random_alphanumeric, lengths)
    pool.close()
    pool.join()
    return results

def add_same_uppercase_and_digit(strings):
    results = []
    uppercase_letter = random.choice(string.ascii_uppercase)
    digit = random.choice(string.digits)
    for _ in strings:
        final_string = _ + uppercase_letter + digit
        results.append(final_string)
    return results

if __name__ == "__main__":
    num_strings_to_generate = 5
    min_length = 8
    max_length = 12

    random_strings = generate_random_strings(num_strings_to_generate, min_length, max_length)
    strings_with_same_uppercase_and_digit = add_same_uppercase_and_digit(random_strings)

    for i, random_str in enumerate(strings_with_same_uppercase_and_digit, start=1):
        print(f"Random Uppercase and Number {i}: {random_str}")

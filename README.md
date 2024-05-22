Certainly! Here’s the report structure with code snippets included to demonstrate how the OOP principles and design patterns are implemented in the code.

---

# Password Generator Application

## Introduction

This application is a Password Generator implemented using Python and Tkinter. It allows users to generate secure passwords based on selected criteria such as length, inclusion of uppercase letters, lowercase letters, digits, and special characters.

### How to Run the Program

1. Ensure you have Python installed on your system.
2. Install the required libraries using:
    ```bash
    pip install pyperclip
    ```
3. Run the program using:
    ```bash
    python password_generator.py
    ```

### How to Use the Program

- Enter the desired password length.
- Select the character sets you wish to include in the password (uppercase letters, lowercase letters, digits, special characters).
- Click "Generate Password" to create a new password.
- Click "Copy Password" to copy the generated password to the clipboard.

## Body/Analysis

### Object-Oriented Programming (OOP) Pillars

#### Encapsulation

Encapsulation is used to bundle the data (password settings) and methods (saving and loading settings) into a single `Config` class. This class controls access to the settings and ensures they are used consistently throughout the application.

```python
class Config:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super(Config, cls).__new__(cls)
            cls._instance.settings = {
                "length": 12,
                "uppercase": True,
                "lowercase": True,
                "digits": True,
                "special": True,
            }
        return cls._instance

    def save_settings(self, filename):
        with open(filename, 'w') as file:
            json.dump(self.settings, file)

    def load_settings(self, filename):
        try:
            with open(filename, 'r') as file:
                self.settings = json.load(file)
        except FileNotFoundError:
            pass
```

#### Abstraction

Abstraction is implemented using the `PasswordFactory` abstract class, which defines the interface for creating passwords. This allows the implementation details to be hidden and provides a clear interface for generating passwords.

```python
from abc import ABC, abstractmethod

class PasswordFactory(ABC):
    @abstractmethod
    def create_password(self, length, include_uppercase, include_lowercase, include_digits, include_special):
        pass
```

#### Inheritance

The `RandomPasswordFactory` class inherits from the `PasswordFactory` abstract class and implements the `create_password` method. This demonstrates inheritance by providing a concrete implementation for password generation.

```python
class RandomPasswordFactory(PasswordFactory):
    def create_password(self, length, include_uppercase, include_lowercase, include_digits, include_special):
        character_sets = ""
        if include_uppercase:
            character_sets += string.ascii_uppercase
        if include_lowercase:
            character_sets += string.ascii_lowercase
        if include_digits:
            character_sets += string.digits
        if include_special:
            character_sets += string.punctuation

        if not character_sets:
            raise ValueError("No character sets selected")

        return ''.join(secrets.choice(character_sets) for _ in range(length))
```

#### Polymorphism

Polymorphism is achieved by using the `PasswordFactory` interface. Different classes can implement this interface in various ways, allowing for different password generation strategies without changing the code that uses the factory.

```python
def generate_password(self):
    try:
        length = int(self.length_entry.get())
    except ValueError:
        self.result_label.config(text="Please enter a valid number for password length.")
        return

    if length < 8:
        self.result_label.config(text="Password length must be at least 8 characters.")
        return

    try:
        password = RandomPasswordFactory().create_password(
            length,
            bool(self.uppercase_var.get()),
            bool(self.lowercase_var.get()),
            bool(self.digits_var.get()),
            bool(self.special_var.get())
        )
    except ValueError as e:
        self.result_label.config(text=str(e))
        return

    self.result_label.config(text=f"Generated Password: {password}")
    self.copy_button.config(state=tk.NORMAL)
    self.generated_password = password

    # Save settings
    self.config.settings['length'] = length
    self.config.settings['uppercase'] = bool(self.uppercase_var.get())
    self.config.settings['lowercase'] = bool(self.lowercase_var.get())
    self.config.settings['digits'] = bool(self.digits_var.get())
    self.config.settings['special'] = bool(self.special_var.get())
    self.config.save_settings('config.json')
```

### Design Patterns

#### Singleton Pattern

The `Config` class uses the Singleton pattern to ensure that only one instance of the configuration settings exists. This is useful for maintaining consistent settings throughout the application.

```python
class Config:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super(Config, cls).__new__(cls)
            cls._instance.settings = {
                "length": 12,
                "uppercase": True,
                "lowercase": True,
                "digits": True,
                "special": True,
            }
        return cls._instance
```

#### Abstract Factory Pattern

The `PasswordFactory` and `RandomPasswordFactory` classes implement the Abstract Factory pattern. This pattern allows for the creation of objects (passwords) without specifying the exact class of object that will be created. This makes it easy to extend the application with different password generation strategies in the future.

```python
from abc import ABC, abstractmethod

class PasswordFactory(ABC):
    @abstractmethod
    def create_password(self, length, include_uppercase, include_lowercase, include_digits, include_special):
        pass

class RandomPasswordFactory(PasswordFactory):
    def create_password(self, length, include_uppercase, include_lowercase, include_digits, include_special):
        character_sets = ""
        if include_uppercase:
            character_sets += string.ascii_uppercase
        if include_lowercase:
            character_sets += string.ascii_lowercase
        if include_digits:
            character_sets += string.digits
        if include_special:
            character_sets += string.punctuation

        if not character_sets:
            raise ValueError("No character sets selected")

        return ''.join(secrets.choice(character_sets) for _ in range(length))
```

### File Reading and Writing

The application saves and loads configuration settings from a `config.json` file. This ensures that the user's preferences are retained between sessions. The `Config` class handles reading and writing these settings.

```python
class Config:
    # ... (Singleton implementation)

    def save_settings(self, filename):
        with open(filename, 'w') as file:
            json.dump(self.settings, file)

    def load_settings(self, filename):
        try:
            with open(filename, 'r') as file:
                self.settings = json.load(file)
        except FileNotFoundError:
            pass
```

## Results and Summary

- Implemented a password generator with a graphical user interface.
- Utilized OOP principles and design patterns to structure the application.
- Added functionality to save and load user settings.
- Successfully created a user-friendly application for generating secure passwords.

## Conclusions

This work resulted in a functional password generator application that leverages object-oriented programming principles and design patterns. The application is extendable and maintains user preferences across sessions. Future enhancements could include adding more customization options for password generation and improving the user interface.

## Optional: Resources, References List

- [Tkinter Documentation](https://docs.python.org/3/library/tkinter.html)
- [PEP8 Style Guide](https://pep8.org/)
- [Design Patterns](https://refactoring.guru/design-patterns/)

```

This revised report includes code snippets to illustrate how each OOP pillar and design pattern is implemented, providing a comprehensive understanding of the code's structure and functionality.

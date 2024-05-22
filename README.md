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

#### Abstraction
Abstraction is implemented using the `PasswordFactory` abstract class, which defines the interface for creating passwords. This allows the implementation details to be hidden and provides a clear interface for generating passwords.

#### Inheritance
The `RandomPasswordFactory` class inherits from the `PasswordFactory` abstract class and implements the `create_password` method. This demonstrates inheritance by providing a concrete implementation for password generation.

#### Polymorphism
Polymorphism is achieved by using the `PasswordFactory` interface. Different classes can implement this interface in various ways, allowing for different password generation strategies without changing the code that uses the factory.

### Design Patterns

#### Singleton Pattern
The `Config` class uses the Singleton pattern to ensure that only one instance of the configuration settings exists. This is useful for maintaining consistent settings throughout the application.

#### Abstract Factory Pattern
The `PasswordFactory` and `RandomPasswordFactory` classes implement the Abstract Factory pattern. This pattern allows for the creation of objects (passwords) without specifying the exact class of object that will be created. This makes it easy to extend the application with different password generation strategies in the future.

### File Reading and Writing

The application saves and loads configuration settings from a `config.json` file. This ensures that the user's preferences are retained between sessions. The `Config` class handles reading and writing these settings.

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


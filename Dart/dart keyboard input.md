# 📖 dart keyboard input

```dart
import 'dart:io';

void main()
{
	print("Enter your name?");
	// Reading name of the Geek
	String? name = stdin.readLineSync(); // null safety in name string

	// Printing the name
	print("Hello, $name! \nWelcome to GeeksforGeeks!!");
}

```

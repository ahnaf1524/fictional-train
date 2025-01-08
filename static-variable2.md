Yes, it is **true** that static methods can **only** access static member variables directly.

### Explanation:
- **Static Methods** are associated with the class itself rather than with an instance (object) of the class. They are independent of any object and do not have access to non-static (instance-specific) members.
- Static methods can only directly access **static member variables** because static variables are shared across all instances of the class, and static methods are part of the class itself, not any individual object.
  
### Why Static Methods Can Only Access Static Members:
- Static methods do not have an implicit `this` pointer (which refers to the current instance). Without a `this` pointer, they cannot access non-static members, which are tied to specific objects.
- Static members are not tied to any particular object either, which makes them accessible from a static method, since static methods are also tied to the class.

### Example to Illustrate This:

```cpp
#include <iostream>
using namespace std;

class MyClass {
private:
    static int staticVar;  // Static member variable
    int instanceVar;       // Non-static member variable

public:
    MyClass(int value) {
        instanceVar = value;
    }

    // Static method can only access static members directly
    static void staticMethod() {
        // Accessing static member
        cout << "Static variable: " << staticVar << endl;
        
        // Error: Cannot access non-static member from static method
        // cout << "Instance variable: " << instanceVar << endl; // This will cause a compile-time error
    }

    // Non-static method can access both static and non-static members
    void nonStaticMethod() {
        cout << "Static variable: " << staticVar << endl; // Can access static member
        cout << "Instance variable: " << instanceVar << endl; // Can access non-static member
    }

    // Method to set static variable (for demonstration)
    static void setStaticVar(int value) {
        staticVar = value;
    }

    // Method to set instance variable (for demonstration)
    void setInstanceVar(int value) {
        instanceVar = value;
    }
};

// Initialize the static variable
int MyClass::staticVar = 0;

int main() {
    MyClass obj1(10), obj2(20);

    // Setting the static variable using the static method
    MyClass::setStaticVar(100);

    // Calling static method
    MyClass::staticMethod();  // Works fine

    // Calling non-static method
    obj1.nonStaticMethod();   // Works fine, can access both static and non-static

    return 0;
}
```

### Key Takeaways:
1. **Static Methods** can only directly access **static members** because they are not tied to a specific object.
2. **Non-static Methods** can access both **static and non-static members** because they are tied to a specific object (which gives them access to both instance-specific data and class-wide data).
3. Static members are shared among all instances of a class, and static methods work at the class level, so they do not have access to instance-specific data.

### Example Output:
```
Static variable: 100
Static variable: 100
Instance variable: 10
```

In this example:
- The `staticMethod()` only accesses the `staticVar` directly because it is static.
- The `nonStaticMethod()` accesses both `staticVar` and `instanceVar` because non-static methods can access both static and non-static members.

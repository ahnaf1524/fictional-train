### **Protected Access Modifier in C++**

In C++, the `protected` access modifier is primarily used to achieve **encapsulation** while allowing access to class members in derived classes. This access level is often used in inheritance hierarchies where data or methods need to be shared between the base and derived classes but not exposed publicly.

---

### **Characteristics of Protected Access Modifier**
1. **Access Scope**:
   - Accessible within the class itself.
   - Accessible within derived classes (directly).
   - Not accessible from outside the class or through objects.

2. **Inheritance Behavior**:
   - **Public Inheritance**: Protected members of the base class remain `protected` in the derived class.
   - **Protected Inheritance**: Protected members of the base class remain `protected` in the derived class.
   - **Private Inheritance**: Protected members of the base class become `private` in the derived class.

3. **Encapsulation**:
   - Provides better control over member access, ensuring they are not directly accessible from outside but can still be used in derived classes.

---

### **Example: Protected Access Modifier**

```cpp
#include <iostream>
using namespace std;

// Base class
class Base {
protected:
    int protectedVar; // Protected member variable

public:
    void setProtectedVar(int value) {
        protectedVar = value;
    }

    void showProtectedVar() {
        cout << "ProtectedVar in Base: " << protectedVar << endl;
    }
};

// Derived class
class Derived : public Base {
public:
    void accessProtected() {
        // Accessing protected member of the base class
        protectedVar += 10; // Allowed in the derived class
        cout << "ProtectedVar in Derived (Modified): " << protectedVar << endl;
    }
};

int main() {
    Base baseObj;
    Derived derivedObj;

    // Direct access to protectedVar is not allowed
    // baseObj.protectedVar = 5; // Error: protected member

    // Accessing protectedVar through public methods
    baseObj.setProtectedVar(20);
    baseObj.showProtectedVar();

    // Accessing protectedVar in derived class
    derivedObj.setProtectedVar(30); // Using public setter from Base
    derivedObj.accessProtected();

    return 0;
}
```

---

### **Output**:
```
ProtectedVar in Base: 20
ProtectedVar in Derived (Modified): 40
```

---

### **Notes on the Code**:
1. **Protected Member in Base Class**:
   - `protectedVar` is declared as `protected` in the `Base` class.
   - It cannot be accessed directly through an object of the `Base` or `Derived` class.

2. **Access through Derived Class**:
   - The `Derived` class accesses and modifies `protectedVar` directly within its own method `accessProtected()`, as it is inherited as `protected`.

3. **Encapsulation**:
   - The `setProtectedVar()` and `showProtectedVar()` methods allow controlled access to `protectedVar` without exposing it directly.

---

### **Behavior of Protected with Different Inheritance Modes**

| **Access Modifier in Base** | **Public Inheritance** | **Protected Inheritance** | **Private Inheritance** |
|-----------------------------|------------------------|---------------------------|--------------------------|
| **Protected Members**       | Protected in Derived   | Protected in Derived      | Private in Derived       |
| **Private Members**         | Not Inherited          | Not Inherited             | Not Inherited            |
| **Public Members**          | Public in Derived      | Protected in Derived      | Private in Derived       |

---

### **Why Use Protected?**
1. **Controlled Access**: Ensures members are only accessible within the class hierarchy.
2. **Encapsulation with Inheritance**: Allows derived classes to reuse functionality without exposing it publicly.
3. **Abstraction**: Helps design clean, modular, and secure code by limiting access to critical data.

---

### **Advanced Example: Multiple Levels of Inheritance**
```cpp
#include <iostream>
using namespace std;

// Base class
class Grandparent {
protected:
    int age;

public:
    void setAge(int a) {
        age = a;
    }
};

// Intermediate derived class
class Parent : public Grandparent {
public:
    void displayAge() {
        cout << "Age accessed in Parent: " << age << endl;
    }
};

// Further derived class
class Child : public Parent {
public:
    void modifyAge() {
        age += 5; // Allowed since age is protected
        cout << "Age modified in Child: " << age << endl;
    }
};

int main() {
    Child childObj;

    // Setting and accessing protected data through hierarchy
    childObj.setAge(50); // Grandparent's public method
    childObj.displayAge(); // Parent's public method
    childObj.modifyAge(); // Child's method modifies protected member

    return 0;
}
```

---

### **Output**:
```
Age accessed in Parent: 50
Age modified in Child: 55
```

---

### **Key Points**:
1. **Multiple Levels of Inheritance**:
   - `age` is declared as `protected` in the `Grandparent` class.
   - It is accessible in `Parent` and `Child` through inheritance.

2. **Hierarchical Access**:
   - `Parent` class uses `age` for display purposes.
   - `Child` class modifies `age`.

3. **Encapsulation and Reusability**:
   - Protected access ensures secure data sharing across the hierarchy without exposing it outside the classes.

---

### **When to Use Protected**:
1. When you want derived classes to have access to base class members but not expose them to external code.
2. In situations where only classes in a hierarchy need to share certain information or methods.

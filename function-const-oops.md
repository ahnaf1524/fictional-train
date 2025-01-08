In C++, the `const` keyword is used in member function declarations to indicate that the function does **not** modify the object on which it is called. Specifically, the functions `getItemName()`, `getPrice()`, and `getQuantity()` are marked as `const` because they only access the object’s state (i.e., the data members) and do not alter it in any way. This makes it clear that these functions are **read-only**.

### Why use `const` in these functions?
1. **Guarantees No Modification of the Object**:
   - The `const` qualifier in a member function tells the compiler and users of the class that calling this function will not change the internal state of the object. It provides a guarantee that calling this function will not modify any member variables, which makes the function safer to use, especially in situations where you want to ensure that objects are not accidentally modified.
   
2. **Enables Use with Const Objects**:
   - If an object is declared as `const`, you cannot call non-const member functions on it because they might modify the object. However, **const member functions** can be called on const objects. This allows you to safely access data from a constant object without altering it.
   
3. **Improves Readability and Design**:
   - By marking a function as `const`, you make it clear to anyone using the class that the function is meant to only read the object’s state and not modify it. It improves the readability of the code and helps maintain clear design patterns in object-oriented programming.

### Example:
If you had a `const` object of the `GroceryItem` class, you wouldn’t be able to call non-const methods, like one that modifies data. However, you can still call `const` methods like `getItemName()`, `getPrice()`, and `getQuantity()` because they don’t modify the object.

```cpp
const GroceryItem item("Milk", 3.0, 2);  // Create a constant object

// You can call these const member functions on a const object:
cout << "Item name: " << item.getItemName() << endl;
cout << "Price: " << item.getPrice() << endl;
cout << "Quantity: " << item.getQuantity() << endl;
```

If you did not declare the getters as `const`, you wouldn't be able to call them on `const` objects.

### What happens if you don't use `const`?
If you do not mark the getter methods with `const`, calling them on a `const` object would result in a compilation error because the compiler would assume that these methods might modify the object. This violates the rule that `const` objects should not be modified.

### Example Without `const`:
```cpp
class GroceryItem
{
private:
    string itemName;
    double price;
    int quantity;

public:
    // Without const, you cannot call these functions on const objects
    string getItemName() { return itemName; }
    double getPrice() { return price; }
    int getQuantity() { return quantity; }
};
```

If you try to use these methods on a `const` object:
```cpp
const GroceryItem item("Milk", 3.0, 2);

// This will cause a compilation error because getItemName() is not marked as const
cout << "Item name: " << item.getItemName() << endl;
```

### In Summary:
The `const` keyword is used here to:
1. Indicate that the function does not modify the object.
2. Enable calling these functions on `const` objects.
3. Improve clarity, safety, and enforce good design practices.

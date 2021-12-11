# const and '&' uses


## **const uses:**

1. const variable

- a const variable must be initialized a value, and that value cannot be changed whatsoever anywhere
in the code in the runtime or compile time or else an error will occur.

```
const PI = 3.141592653589793;
PI = 3.14;      // This will give an error
PI = PI + 10;   // This will also give an error

```



2. const pointers

- the pointer can not be changed whereas the variable that it points has a changeable value.
  ( const pointer, variable variable)

  Example: 

```
int main()
{
int x{ 10 };
char y{ 'M' };

    const int* i = &x;
    const char* j = &y;
 
    // Value of x and y can be altered,
    // they are not constant variables
    x = 9;
    y = 'A';
 
    // Change of constant values because,
    // i and j are pointing to const-int
    // & const-char type value
    // *i = 6;
    // *j = 7;
 
    cout << *i << " " << *j;
}
```

                              
- the pointer value can be changed whereas the value of the variable that it points to cannot be changed.
  ( changeable pointer, const variable )

```
// Driver Code
int main()
{
// x and z non-const var
int x = 5;
int z = 6;

    // y and p non-const var
char y = 'A';
char p = 'C';
 
    // const pointer(i) pointing
    // to the var x's location
int* const i = &x;
 
    // const pointer(j) pointing
    // to the var y's location
char* const j = &y;
 
 
    // The values that is stored at the memory location can modified
    // even if we modify it through the pointer itself
    // No CTE error
    *i = 10;
    *j = 'D';
 
    // CTE because pointer variable
    // is const type so the address
    // pointed by the pointer variables
    // can't be changed
    // *i = &z;
    // *j = &p;
 
cout << *i << " and " << *j
     << endl;
cout << i << " and " << j;
 
return 0;
}     
```
                         

- the pointer has a const value, so does the variable it points to.
  ( const pointer value, const variable value )

```
// Driver code
int main()
{
int x{ 9 };

    const int* const i = &x;
   
    // *i=10;  
    // The above statement will give CTE
    // Once Ptr(*i) value is
    // assigned, later it can't
    // be modified(Error)
 
char y{ 'A' };
 
const char* const j = &y;
   
    // *j='B';
    // The above statement will give CTE
    // Once Ptr(*j) value is
    // assigned, later it can't
    // be modified(Error)
 
cout << *i << " and " << *j;
 
return 0;
}
```
                              
3. const data members 

- data variables in class defined using const keyword. They are not initialized during declaration, but 
in the constructor.

```
const Date date1; // initialize using default constructor
const Date date2(2020, 10, 16); // initialize using parameterized constructor
const Date date3 { 2020, 10, 16 }; // initialize using parameterized constructor (C++11)
```

4. const objects 

- When an object is declared or created using the const keyword, its data members can never be 
changed, during the object's lifetime.

```
class Something
{
public:
int m_value {};

    Something(): m_value{0} { }

    void setValue(int value) { m_value = value; }
    int getValue() { return m_value ; }
};

int main()
{
const Something something{}; // calls default constructor

    something.m_value = 5; // compiler error: violates const
    something.setValue(5); // compiler error: violates const

    return 0;
}
```

5. const functions

* A const member functions can never modify data members in an object.

Syntax:

return_type function_name() const;

```
class Something
{
public:
    int m_value {};

    Something(): m_value{0} { }

    void resetValue() { m_value = 0; }
    void setValue(int value) { m_value = value; }

    int getValue() const { return m_value; } // note addition of const keyword after parameter list, but before function body
};

``` 

```
class Something
{
public:
    int m_value {};

    void resetValue() const { m_value = 0; } // compile error, const functions can't change member variables.
};
```
Here, we can see, that const member function never changes data members of class, and it can be used 
with both const and non-const objects. But a const object cannot be used with a member function which 
tries to change its data members.

6. const iterators

- A const iterator points to an element of constant type which means the element which is being pointed
to by a const_iterator can’t be modified. Though we can still update the iterator.
(i.e., the iterator can be incremented or decremented but the element it points to can not be changed).
It can be used for access only, and can’t be used for modification. If we try to modify the value of 
the element using const iterator then it generates an error, whereas A regular or non const_iterator 
points to an element inside the container and can be used to modify the element to which it is pointing.

```
// C++ program to demonstrate a regular
// and const_iterator
#include <iostream>
#include <iterator>
#include <vector>
using namespace std;
  
// Function that demonstrate regular
// iterators
void regularIterator(vector<int>& v)
{
    // Declare a regular iterator
    // to a vector
    vector<int>::iterator i;
  
    // Printing the elements of the
    // vector v using regular iterator
    for (i = v.begin(); i < v.end(); i++) {
  
        // Update elements of vector
        *i += 1;
        cout << *i << " ";
    }
}
  
// Function that demonstrate const
// iterators
void constIterator(vector<int>& v1)
{
    // Declare a const_itearor
    // to a vector
    vector<int>::const_iterator ci;
  
    // Printing the elements of the
    // vector v1 using regular iterator
    for (ci = v1.begin(); ci < v1.end(); ci++) {
  
        // Below line will throw an error
        // as we are trying to modify the
        // element to which const_iterator
        // is pointing
  
        //*ci += 1;
  
        cout << *ci << " ";
    }
}
  
// Driver Code
int main()
{
    // Declaring vectors
    vector<int> v = { 7, 2, 4 };
    vector<int> v1 = { 5, 7, 0 };
  
    // Demonstrate Regular iterator
    regularIterator(v);
  
    cout << endl;
  
    // Demonstrate Const iterator
    constIterator(v1);
    return 0;
}
```

--- 

## **Ampersand $ uses:**

1. declare a reference to a type 

-if you use the & on the left hand-side of a variable deceleration, it means that you are making 
a reference to the declared type.

Example:
```
std::string mrSamberg("Andy");
std::string& theBoss = mrSamberg;
```

2. get the address of a variable 

-if you use the $ on the right hand-side of an assignment equation, it means that you are assigning a 
pointer to a certain variable, and it'll return the address of that variable instead of the value stored 
in it itslef.

Example:

```
std::string mrSamberg("Andy");
std::string* theBoss;

theBoss = &mrSamberg;
```

3. as a bit-wise operator 

- represents the AND operator where you perform an AND operation on two numbers, where the two numbers 
are represented as a set of bits and each bit is AND=ed with the corresponding bit, and only 
producing 1 if both bits are ones, otherwise output bit is zero.

Example:

number     |  16  |  8  |  4  |  2  |  1
------|-----|------|-----|-----|-----
25  |  1  |  1  |  0  |  0 |   1
15  |  0  |  1  |  1  |  1  |  1
25&12|  0  |  1  |  0  | 0   | 1

4. && in a conditional expression
 
- the performance of an AND operation where true is returned only if both inputs are true, otherwise
it returns false.

```
#include <iostream>
using namespace std;
int main() { 
bool result;
int X;
cin>›X;
if (X>0 && X%2==0) 
result = true;
else result= false;
cout<<result;
return 0;
}
```

5. for declaring rvalue references

- An lvalue (locator value) represents an object that occupies some identifiable location in memory
(i.e. has an address). (typically found at the left hand-side of an assignment operation).
- An rvalue is an expression that does not represent an object occupying some identifiable 
location in memory. (i.e. does not have an address). 
(typically found at the right hand-side of an assignment operation).

```
int a = 10;

// Declaring lvalue reference
int& lref = a;

// Declaring rvalue reference
int&& rref = 20; 
```

- Although rvalues can only appear on the right-hand side, still one can reference to 
them. This is called rvalue references and such variables have to be declared with double ampersands (&&).
  (i.e. you can reference an rvalue by using a variable declared with double ampersands.)
```
// C++ program to illustrate the
// lvalue and rvalue

#include <iostream>
using namespace std;

// Driver Code
int main()
{
// Declaring the variable
int a{ 10 };

    // Declaring reference to
    // already created variable
    int& b = a;
 
    // Provision made to display
    // the boolean output in the
    // form of True and False
    // instead of 1 and
    cout << boolalpha;
 
    // Comparing the address of both the
    // variable and its reference and it
    // will turn out to be same
    cout << (&a == &b) << endl;
    return 0;
}
```
6. for declaring universal references

- the same way of referencing an rvalue can be used in declaring a universal reference. shortly, 
if type deduction takes place, you declare a universal reference, if not an rvalue reference.

Example:

```
Vehicle car;
auto&& car2 = car; // type deduction! this is a universal reference!
Vehicle&& car3 = car; // no type deduction, so it's an rvalue reference
``` 

7. & or && for function overloading

you can limit the use of a member FUNCTION based on whether *this is a lvalue or an rvalue.

Example:

``` 
class Tool {
public:
// ...
void doSomething() &; // used when *this is a lvalue
void doSomething() &&; // used when *this is a rvalue
};

Tool makeTool(); //a factory function returning an rvalue

Tool t; // t is an lvalue

t.doSomething(); // Tool::doSomething & is called

makeTool().doSomething(); // Tool::doSomething && is called
```

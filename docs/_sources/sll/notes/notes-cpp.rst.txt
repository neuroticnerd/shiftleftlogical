:date: 2013-02-05
:modified: 2019-09-09

=================
C++ Notes
=================

CONST VS NON-CONST MEMBER FUNCTIONS:

In short, they're used to add 'const correctness' to your program.
value_type& top() { return this.item }


This is used to provide mutable access to item. It is used so you can modify the element in the container.
For example:
c.top().set_property(5);  // OK - sets a property of 'item'
cout << c.top().get_property();  // OK - gets a property of 'item'


One common example for this pattern is returning mutable access to an element with vector::operator[int index].
std::vector<int> v(5);
v[0] = 1;  // Returns operator[] returns int&.


On the other hand:
const value_type& top() const { return this.item }


This is used to provide const access to item. It's more restrictive than the previous version - but it has one advantage - you can call it on a const object.
void Foo(const Container &c) {
   c.top();  // Since 'c' is const, you cannot modify it... so the const top is called.
   c.top().set_property(5);  // compile error can't modify const 'item'.
   c.top().get_property();   // OK, const access on 'item'.
}


To follow the vector example:
const std::vector<int> v(5, 2);
v[0] = 5;  // compile error, can't mutate a const vector.
std::cout << v[1];  // OK, const access to the vector.




STATIC MEMBER VARIABLES

Member variables of a class can be made static by using the static keyword. Static member variables only exist once in a program regardless of how many class objects are defined! One way to think about it is that all objects of a class share the static variables. Consider the following program:
class Something
{
public:
    static int s_nValue;
};

int Something::s_nValue = 1;

int main()
{
    Something cFirst;
    cFirst.s_nValue = 2;

    Something cSecond;
    std::cout << cSecond.s_nValue;

    return 0;
}




& AMPERSAND OPERATOR DIFFERENCES:


Bitwise AND


a & b
a bitand b
Yes
Yes
R T::operator &(S b);
R operator &(S a, T b);

reference

address-of



WHY PUT ALL OF TEMPLATE DEFINITION IN THE HEADER:

The compiler needs to have access to the entire template definition (not just the signature) in order to generate code for each instantiation of the template, so you need to move the definitions of the functions to your header.

The definition of a class template and the implementation of its member functions has to be visible to every place that instantiates it with a distinct type. i.e. in order to instantiate myTemplate<int> you need to see the full definition and implementation of myTemplate.
The easiest way to do this is to put the definition of the template and its member functions in the same header, but there are other ways. For example, you could put the member function implementations in a separate file that was included separately. You could then include it from the first header, or only include the implementation file where you needed it.
For example, one practise is to explicitly instantiate a template for distinct set of parameters in one .cpp file and declare those instantiations extern in the header. This way, those instantiations can be used in other source files without requiring the implementation of the template member functions to be visible. However, unless you include the implementation file you won't be able to use other sets of template parameters.
i.e. if you have myTemplate<int> and myTemplate<std::string> defined as extern then you can use them fine, but if myTemplate<double> is not defined extern then you cannot use that without the implementation



REFERENCES VS POINTERS:

I know references are syntactic sugar, so easier code to read and write :)
But what are the differences?
Summary from answers and links below:
A pointer can be re-assigned any number of times while a reference can not be reassigned after initialization.
A pointer can point to NULL while reference can never point to NULL
You can't take the address of a reference like you can with pointers
There's no "reference arithmetics" (but you can take the address of an object pointed by a reference and do pointer arithmetics on it as in &obj + 5).
To clarify a misconception:
The C++ standard is very careful to avoid dictating how a compiler must implement references, but every C++ compiler implements references as pointers. That is, a declaration such as:
int &ri = i;


allocates the same amount of storage as a pointer, and places the address of i into that storage.
So pointer and reference occupies same amount of memory
As a general rule,
Use references in function parameters and return types to define attractive interfaces.
Use pointers to implement algorithms and data structures.



INITIALIZER LIST:

If you don't use the initializer list, the member or base class gets default constructed before the opening curly brace.
So, your calls to set it later will add an operator=() call.
If you use the initializer list, the member or base class has the proper constructor is called.
Depending on your classes, this might be required or faster.

For primitives, there is no difference between using initializer lists or constructing them via assignment.
For other types, initializer lists might afford you performance improvements when constructing objects.
Do note that the order of initializing (in initializer lists) depends on the order of declaration in the class. If the declarations are out of order and you need to construct data that depends on something else already being initialized before hand, that is an exception to the 'use initialization lists when possible rule'.
More info: http://www.parashift.com/c++-faq-lite/ctors.html#faq-10.6

Also, never perform unmanaged resource acquisition in initializer lists. In other words, either use "resource acquisition is initialization" (thereby avoiding unmanaged resources entirely) or else perform the resource acquisition in the constructor body.
And warning #2 Perform every resource allocation (e.g., new) in its own code statement which immediately gives the new resource to a manager object (e.g., auto_ptr).
http://www.gotw.ca/gotw/056.htm


RESOURCE ACQUISITION IS INITIALIZATION:



EXPLICITLY CALLING A CONSTRUCTOR:

you cannot explicitly call a constructor in c++. you can implicitly invoke one by creating a new object such as by using the new operator, or a temporary object as a parameter to a function call

In general you do not call the constructor directly. The new operator calls it for you or a subclass calls the parent class' constructors. In C++, the base class is guarenteed to be fully constructed before the derived class' constructor starts.
The only time you would call a constructor directly is in the extremely rare case where you are managing memory without using new. And even then, you shouldn't do it. Instead you should use the placement form of operator new.



PLACEMENT NEW OPERATOR:

Placement new allows you to construct an object on memory that's already allocated.
You may want to do this for optimizations (it is faster not to re-allocate all the time) but you need to re-construct an object multiple times. If you need to keep re-allocating it might be more efficient to allocate more than you need, even though you don't want to use it yet.
devex gives a good example:
Standard C++ also supports placement new operator, which constructs an object on a pre-allocated buffer. This is useful when building a memory pool, a garbage collector or simply when performance and exception safety are paramount (there's no danger of allocation failure since the memory has already been allocated, and constructing an object on a pre-allocated buffer takes less time):
void placement() {

char *buf  = new char[sizeof(string)];   //pre-allocated buffer
    string *p = new (buf) string("hi");  //placement new
    string *q = new string("hi");  //ordinary heap allocation


You may also want to be sure there can be no allocation failure at a certain part of critical code (maybe you work on a pacemaker for example). In that case you would want to use placement new.
Deallocation in placement new:
You should not deallocate every object that is using the memory buffer. Instead you should delete[] only the original buffer. You would have to then call the destructors directly of your classes manually. For a good suggestion on this please see Stroustrup's FAQ on: Is there a "placement delete"?

Strictly, it's undefined behaviour to call delete[] on the original char buffer. Using placement new has ended the lifetime of the original char objects by re-using their storage. If you now call delete[] buf the dynamic type of the object(s) pointed to no longer matches their static type so you have undefined behaviour. It is more consistent to use operator new/operator delete to allocate raw memory intended for use by placement new



PURE VIRTUAL FUNCTIONS AND 0:

The reason =0 is used is that Bjarne Stroustrup didn't think he could get another keyword, such as "pure" past the C++ community at the time the feature was being implemented. This is described in his book, The Design & Evolution of C++, section 13.2.3:
The curious =0 syntax was chosen ... because at the time I saw no chance of getting a new keyword accepted.
He also states explicitly that this need not set the vtable entry to NULL, and that doing so is not the best way of implementing pure virtual functions.

As with most "Why" questions about the design of C++, the first place to look is The Design and Evolution of C++, by Bjarne Stroustrup1:
The curious =0 syntax was chosen over the obvious alternative of introducing a new keyword pure or abstract because at the time I saw no chance of getting a new keyword accepted. Had I suggested pure, Release 2.0 would have shipped without abstract classes. Given a choice between a nicer syntax and abstract classes, I chose abstract classes. Rather than risking delay and incurring the certain fights over pure, I used the tradition C and C++ convention of using 0 to represent "not there." The =0 syntax fits with my view that a function body is the initializer for a function also with the (simplistic, but usually adequate) view of the set of virtual functions being implemented as a vector of function pointers. [ ... ]



What is polymorphism.
What is overriding and overloading.
What is heap and stack.
Describe the process to take a single-file hello-world source file and make it into an executable.
What is a hash table.
What is a linked list. Why would you prefer to use this rather than e.g. an array.
Describe the binary search algorithm
Reference vs pointer and how to dereference with syntax
STL and templating
Auto pointers





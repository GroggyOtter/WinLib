# WinLib

This is a library I'm currently creating to make working with Window's structs, constants, data types, etc easier.  
This is a WIP and I have no idea if I'll even finish it.  
Just trying something new and seeing what happens.

Goals:
To consolidate as many data types, constants, structs, and other similar pieces of data as I could into one library.  
I'm currently designing struct classes that will take any struct definition and convert it into the proper buffer.
This is done by reading each line and determining member identity as well as member type.  
WinLib then calls on it's Data Type class to cross convert any data type to is actual byte size.  

Implemented so far:
* Data Types
* Structures
* Constants

When these are done, you should be able any common data type, structure, or constant on-demand.

Struct Example:
Using a basic [RECT struct](https://learn.microsoft.com/en-us/windows/win32/api/windef/ns-windef-rect).  
```
typedef struct tagRECT {
  LONG left;
  LONG top;
  LONG right;
  LONG bottom;
} RECT, *PRECT, *NPRECT, *LPRECT;
```

RECT structs contain 4 `LONG` numbers.  
left, top, right, bottom (in order)
Size is 16 because 4 bytes * 4 longs.  

Create a RECT struct with WinLib using:
```
myRECT := WinLib.Struct("RECT")
```

This builds a new struct class which contains a buffer to handle the binary data.  
Struct members can now be accessed as properties of the class.  
`myRECT.left myRECT.top myRECT.right myRECT.bottom`
This allows you to set/get data from the struct using normal AHK syntax and without having to deal with numput/numget.

In addition to a buffer, the struct class also has:

Priavte (Meaning don't use these)
* `mem` = Each member is stored in the mem map and includes that member's type, offset, and size
* `order` = Stores the order of the members

Public:
* `Size` = Allows you to set/get the total size of the buffer
* `Ptr` = Returns the buffer's pointer




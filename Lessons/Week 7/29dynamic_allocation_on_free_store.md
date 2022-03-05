# 03/02/2022: Dynamic allocation of objects on the free store

## Dynamically allocated objects
- Resides in the free store (heap)
- Indicate free store object using **new** operator, this operator returns based address of region in memory allocated for that object 

``` cpp
int* free_store_object = new int; 
const size_t kFreeStoreArrayCapacity = 10;
int* free_store_array = new int[kFreeStoreArrayCapacity];
```

- We are responsible for deallocating memory once we are done using the object
- **NOTE**: WE THE VARIABLE HOLDS THE ADDRESS OF THE OBJECT (it's a pointer), SO THE DELETE OPERATOR GOES TO THAT ADDRESS AND DEALLOCATES MEMORY
```cpp
delete free_store_object;
delete[] free_store_array;
```

To avoid narrowing conversion
``` cpp
int* p_int = new int{0};
double* p_double = new double{0.0};
```

## What's on the stack vs free store?
- Must update to **nullptr** to disconnect the pointer in the free store
- Just deleting leaves you with a **DANGLING pointer**

```cpp
size_t free_store_array_capacity = 4;
int* free_store_array = new int[free_store_array_capacity]{10, 20, 30, 40};
delete[] free_store_array;
// disconnecting pointer!
free_store_array = nullptr;
```

STACK: The value of named objects
- **value is 4**, identified by the int *free_store_array_capacity*
- **value is address of an integer object (array)**, identified by the pointer *free_store_array*

FREE STORE
- space allocated {10, 20, 30, 40}

## delete Operator
- delete
- delete[]

## Resizing dynamically allocated array 
1. Datermine the capacity/size of new array
2. Create a new array with that capacity and store address somewhere, so you do not lose the pointer
3. Copy the contents of the old array into the new array
4. delete[] old array (dangling pointer remains)
5. Update the pointer of array with address of new array
6. Update the variable storing array capacity/size

```cpp
MyArray ReadDataFromFile(const std::string& file_name) {
    std::ifstream ifs{file_name};
    MyArray data{new int[2], 2, 0};
    int value_read;
    while (ifs >> value_read) {
        if (data.size == data.capacity) {
            ResizeMyArray(data);
        }
        data.array[data.size] = value_read;
        data.size += 1;
    }
    return data;
}

// pass by reference to actually modify the object
void ResizeMyArray(MyArray& data) {
    size_t updated_capacity = data.capcity * 2;
    int* tmp = new int[updated_capacity];
    for (size_t i = 0; i < data.size; i++) {
        temp[i] = data.array[i];
    }
    // dangling pointer
    delete[] data.array;
    // reassign pointer
    data.array = temp;
    data.capacity = updated_capacity;
}
```

## HW Notes
- Read operators right to left
```cpp
int*& ptr; // this a REFERENCE to a POINTER
```
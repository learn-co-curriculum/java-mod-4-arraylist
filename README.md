# ArrayList

## Learning Goals

- Explain how an ArrayList differs from an Array.
- Create ArrayLists.
- Access, add, and remove elements from ArrayLists.
- Understand the performances of different methods.

## Array Review

An array is a fixed-length data structure that stores a collection of ordered
items. Here are a few array operations for review:

```java
public class ArrayListExample {
    public static void main(String[] args) {
        String[] names = {"Bob", "John", "Kate", "Lee"};
        int[] numbers = new int[5];

        System.out.println(names[0]); // -> "Bob"
        names[0] = "Bobby";
        System.out.println(names[0]); // -> "Bobby"

        numbers[0] = 1;
        System.out.println(numbers[5]); // -> array index out of bounds
    }
}
```

Note that we have to specify the exact number of elements when initializing the
array. The size cannot be modified once it’s been initialized although we can
modify elements at specific indexes.

## What is an ArrayList?

An `ArrayList` is also an ordered collection of elements but it supports
addition and removal of elements unlike an Array. Both Arrays and ArrayLists
allow for duplicate elements.

Internally, `ArrayList` use an Array and dynamically resizes itself if an
insertion requires more space than is available in the array.

## Creating an ArrayList

There are three ways of creating an ArrayList:

- Initialize an Empty ArrayList
- Initialize an ArrayList with Initial Capacity Specified
- Initialize an ArrayList from an Existing Collection

### Initialize an Empty ArrayList

The default constructor is called without any arguments. It initializes an empty
ArrayList instance. We have to provide the element type within the `<>` to tell
Java what type of data is being stored in the ArrayList instance.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>();
    }
}
```

### Initialize an ArrayList with Initial Capacity Specified

The default ArrayList size is very small and each resize operation is O(n) which
can become quite expensive if we’re putting in a lot of data.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>(100);
    }
}
```

### Initialize an ArrayList from an Existing Collection

The ArrayList constructor can also take in a different collection and create an
ArrayList from it.

```java
import java.util.ArrayList;
import java.util.Arrays;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<String>(Arrays.asList(
                "Bobby",
                "Kate",
                "Bedelia",
                "Ali"
        ));
        System.out.println(names); // -> [Bobby, Kate, Bedelia, Ali]
    }
}
```

## Adding Elements

We can add a single element at the end of an ArrayList or a specific index.
Multiple elements can also be added from another collection.

### Adding an Element at the End of an ArrayList

The `add(E e)` method is used for adding elements at the end of ArrayLists. The
ArrayList checks its own capacity before adding an element and resizes itself if
the capacity is about to be exceeded. This is an O(1) operation since the
element is added at an empty space at the end.

**NOTE:** The O(1) time complexity is the
[amortized cost](https://cs.stackexchange.com/questions/63752/amortized-time-cost-of-insertion-into-an-array-list).

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("mango");
        fruits.add("apple");
        fruits.add("grape");
        System.out.println(fruits); // -> [mango, apple, grape]

        fruits.add(1, "strawberry");
        System.out.println(fruits); // -> [mango, strawberry, apple, grape]
    }
}
```

### Adding an Element at a Specific Index

The `add(int index, E element)` method inserts an element at the given index. It
shifts the element at the given index and any following element to the right.

### Adding Multiple Elements from Other Collections

The `addAll` method is used to add the elements of one collection into another.
It has two signatures: `addAll(Collection c)` and
`addAll(int index, Collection c)`.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("mango");
        fruits.add("apple");

        ArrayList<String> favoriteFruits = new ArrayList<>();
        favoriteFruits.add("grape");
        favoriteFruits.addAll(fruits);

        System.out.println(favoriteFruits); // -> [grape, mango, apple]
    }
}
```

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("mango");
        fruits.add("apple");

        ArrayList<String> favoriteFruits = new ArrayList<>();
        favoriteFruits.add("grape");
        favoriteFruits.addAll(0, fruits);

        System.out.println(favoriteFruits); // -> [mango, apple, grape]
    }
}
```

## Retrieving Elements

The `get(int index)` method gets the element at the given index. It is an O(1)
operation since an ArrayList uses an array under the hood to keep track of the
elements.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("mango");
        fruits.add("apple");
        fruits.add("grape");

        System.out.println(fruits); // -> [mango, apple, grape]
        System.out.println(fruits.get(1)); // -> apple
    }
}
```

## Removing Elements

There are several methods to remove elements from an ArrayList. We’ll look at
the most common methods.

### Removing an Element at a Given Index

The `remove (int index)` method removes the element at the index. The ArrayList
resizes itself after removing the element. Any removal except for the last
element is O(n) because of this resizing operation.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("mango");
        fruits.add("apple");
        fruits.add("grape");

        System.out.println(fruits); // -> [mango, apple, grape]
        fruits.remove(1);
        System.out.println(fruits); // -> [mango, grape]
    }
}
```

### Removing a Specific Element

The `remove (Object o)` searches for the element in the ArrayList and removes
the first occurrence of the given object `o`.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("mango");
        fruits.add("apple");
        fruits.add("grape");

        System.out.println(fruits); // -> [mango, apple, grape]
        fruits.remove("apple");
        System.out.println(fruits); // -> [mango, grape]
    }
}
```

For removing integers using this method, we have to convert the integer to an
`Integer`.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<Integer> nums = new ArrayList<>();
        nums.add(10);
        nums.add(20);
        nums.add(30);

        nums.remove(Integer.valueOf(20));
        System.out.println(nums); // -> [10, 30]
    }
}
```

### Removing All Elements

The `clear()` method removes all the elements from the ArrayList.

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("mango");
        fruits.add("apple");
        fruits.add("grape");

        fruits.clear();
        System.out.println(fruits); // -> []
    }
}
```

## Conclusion

The `ArrayList` is one of the most used data structures in Java. Make sure to
understand the performance implications of the methods so you can better design
your program.

## References

- [ArrayList Java Docs](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/ArrayList.html)

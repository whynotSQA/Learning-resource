# Learning-resource
resources link collection 
https://www.ibm.com/developerworks/cn/java/j-lo-classloader/  深入探讨 Java 类加载器
http://www.jianshu.com/p/6f6bb2f0ece9 代理模式及Java实现动态代理
---------------------------------------------------------------------------------------------------------------
Generic 范型 http://docs.oracle.com/javase/tutorial/java/generics/index.html
a. Strong type checks at compile time
b. elimination of casts
c. enable to implement generic algorithms on collections of different types.

Type Parameter and Type Argument Terminology: Many developers use the terms "type parameter" and "type argument" interchangeably, but these terms are not the same. When coding, one provides type arguments in order to create a parameterized type. Therefore, the T in Foo<T> is a type parameter and the String in Foo<String> f is a type argument. This lesson observes this definition when using these terms.

An invocation of a generic type is generally known as a parameterized type.
没有指定任何type arguments 的范型类或者接口称为 raw types. 用raw types 的对象访问访问一个已定义类型的范型方法会报"unchecked invocation" warnings.
Bounded type parameters: public class NaturalNumber<T extends Integer> {}.
Mutiple Bounded: <T extends B1 & B2 & B3> if one of bounds is a class, must be list as first one. class D <T extends A & B & C> { /* ... */ }  A is a class which specified first.B or C can be interfaces.

Operator ">" can only apply to primitive types, so for objects will need to use a type parameter bounded by comparable<T> interface:
public interface Comparable<T> {
    public int compareTo(T o);
}
public static <T extends Comparable<T>> int counterGreaterThan(T[] anArray, T elem) {
  int count = 0;
    for (T e : anArray)
        if (e.compareTo(elem) > 0)
            ++count;
    return count;
}

which not like public static <T> int countGreaterThan(T[] anArray, T elem) {
    int count = 0;
    for (T e : anArray)
        if (e > elem)  // compiler error
            ++count;
    return count;
}

Box<Integer> is not a subtype of Box<Number> even though Integer is a subtype of Number.
You can subtype a generic class or interface by extending or implementing it. The relationship between the type parameters of one class or interface and the type parameters of another are determined by the extends and implements clauses.
Using the Collections classes as an example, ArrayList<E> implements List<E>, and List<E> extends Collection<E>. So ArrayList<String> is a subtype of List<String>, which is a subtype of Collection<String>. So long as you do not vary the type argument, the subtyping relationship is preserved between the types.

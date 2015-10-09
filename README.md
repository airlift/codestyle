# Code style for Airlift projects

## IntelliJ IDEA 14 on Mac OS X

To install, copy `IntelliJIdea14/Airlift.xml` into `~/Library/Preferences/IntelliJIdea14/codestyles`

## IntelliJ IDEA 14 on Linux

To install, copy `IntelliJIdea14/Airlift.xml` into `$HOME/.IdeaIC14/config/codestyles`

## Programming guidelines

* Commit messages should follow the format described [here](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html). Ideally, you should be able to look at the commit and:
    * be able to tell whether this fix applies to something they may be seeing,
    * understand the reason why it's broken,
    * have some context when looking at the actual changes in the commit (trying to reverse-engineer the observed behavior from the code changes can be very hard).

  Commit message are the way developers communicate with their future selves and other
  colleagues so special care should be taken when writing them.
* End every file with a newline. To enable this automatically on save in IntelliJ 14: File->Settings->General->Other (section on the right when you click on General)->Check "Ensure line feed at file end on Save".
* Don't use `else`, if the `if` has a return in it.
* Don't mix concurrency and inheritance. Concurrent classes should not compose/inherit because that forces you to reason about the memory visibility of each member and understand the locking semantics of the class' parent(s). Generally, inheritance makes concurrency semantics implicit and harder to follow.
* Favor early termination (return) on certain input values to methods. This improves readability because it divides the method into two sections: the first where you enumerate exit conditions and the second where the actual method logic lives.
* Inline variables that are used only once. However, if the expression is very complicated and assigning it a descriptive variable name improves readability then that's what you should do.
* Avoid using Mockito style mocking frameworks in tests because they make tests brittle and less readable. Use such frameworks as a last resort when you're testing against libraries that don't have good abstractions.

## General Java style guidelines

* Do not abbreviate Java variable names: `command` and not `cmd`.
* Google's Guava is seen as an extension of the JDK. You should use it when
    * certain functionality doesn't exist in the JDK or
    * Guava presents you with a clearly superior API and doesn't degrade performance.

  For example, do not use `Guava.checkNotNull()` because the same functionality exists
  in the JDK as `Objects.requireNonNull()`.
* Do not use .* style imports since they cause name conflicts. If you're using the Airlift codestyle, then IntelliJ is configured to not add such imports automatically.
* Do not vertically align characters; avoid vertical alignment of the `=` character as is common in C/C++.
* Use static imports where appropriate. For example, do not statically import `Optional.of()` or `ImmutableSet.Builder()`, `ImmutableList.Builder()`, `ImmutableMap.Builder()`. Sometimes the enclosing class qualifies the method and a static import doesn't make sense.
* Use [jmh](http://openjdk.java.net/projects/code-tools/jmh/) for all micro benchmarking (measuring performance of a single method). Do not attempt to write your own harness.
* Follow synchronization best practices: design objects to be as immutable as possible, document the concurrency semantics of your objects using annotations (`@GuardedBy`, `@ThreadSafe`). For more info we recommend you read [Java Concurrency in Practice](http://jcip.net.s3-website-us-east-1.amazonaws.com/).
* Do not use Java Serialization because it is very slow.
* Defensively check for `NULL`s on your public interfaces. Add `@Nullable` when arguments to constructors can be `NULL`, otherwise ensure arguments are not `NULL`. Consider using `Optional`s in place of nullable fields.

## Examples

Generated from Intellij IDEA's code formatting preview.

### Tabs and Indents
```java
public class Foo
{
    public int[] X = new int[] {1, 3, 5 7, 9, 11};

    public void foo(boolean a, int x, int y, int z)
    {
        label1:
        do {
            try {
                if (x > 0) {
                    int someVariable = a ? x : y;
                    int anotherVariable = a ? x : y;
                }
                else if (x < 0) {
                    int someVariable = (y + z);
                    someVariable = x = x + y;
                }
                else {
                    label2:
                    for (int i = 0; i < 5; i++) {
                        doSomething(i);
                    }
                }
                switch (a) {
                    case 0:
                        doCase0();
                        break;
                    default:
                        doDefault();
                }
            }
            catch (Exception e) {
                processException(e.getMessage(), x + y, z, a);
            }
            finally {
                processFinally();
            }
        }
        while (true);

        if (2 < 3) {
            return;
        }
        if (3 < 4) {
            return;
        }
        do {
            x++
        }
        while (x < 10000);
        while (x < 50000) {
            x++;
        }
        for (int i = 0; i < 5; i++) {
            System.out.println(i);
        }
    }

    private class InnerClass
            implements I1, I2
    {
        public void bar()
                throws E1, E2
        {
        }
    }
}
```

### Spaces
```java
@Annotation(param1 = "value1", param2 = "value2")
@SuppressWarnings({"ALL"})
public class Foo<T, U>
{
    int[] X = new int[] {1, 3, 5, 6, 7, 87, 1213, 2};

    public void foo(int x, int y)
    {
        Runnable r = () -> {
        };
        Runnable r1 = this::bar;
        for (int i = 0; i < x; i++) {
            y += (y ^ 0x123) << 2;
        }
        do {
            try (MyResource r1 = getResource(); MyResource r2 = null) {
                if (0 < x && x < 10) {
                    while (x != y) {
                        x = f(x * 3 + 5);
                    }
                }
                else {
                    synchronized (this) {
                        switch (e.getCode()) {
                            //...
                        }
                    }
                }
            }
            catch (MyException e) {
            }
            finally {
                int[] arr = (int[]) g(y);
                x = y >= 0 ? arr[y] : -1;
            }
        }
        while (true);
    }

    void bar()
    {
        {
            return;
        }
    }
}

class Bar {}
```

### Wrapping and Braces
```java
/*
 * This is a sample file.
 */

public class ThisIsASampleClass
        extends C1
        implements I1, I2, I3, I4, I5
{
    private int f1 = 1;
    private String field2 = "";

    public void foo1(int i1, int i2, int i3, int i4, int i5, int i6, int i7) {}

    public static void longerMethod()
            throws Exception1,
            Exception2, Exception3
    {
// todo something
        int
                i = 0;
        int[] a = new int[] {1, 2,
                             0x0052,
                             0x0053,
                             0x0054};
        int var1 = 1;
        int var2 = 2;
        foo1(0x0051, 0x0052, 0x0053, 0x0054, 0x0055, 0x0056, 0x0057);
        int x = (3 + 4 + 5 + 6) * (7 + 8 + 9 + 10) * (11 + 12 + 13 + 14 + 0xFFFFFFFF);
        String s1, s2, s3;
        s1 = s2 = s3 = "012345678901456";
        assert i + j + k + l + n + m <= 2 :
                "assert description";
        int y = 2 > 3 ? 7 + 8 + 9 : 11 + 12 + 13;
        super.getFoo().foo().getBar().bar();

        label:
        if (2 < 3) {
            return;
        }
        else if (2 > 3) {
            return;
        }
        else {
            return;
        }
        for (int i = 0; i < 0xFFFFFF; i += 2) {
            System.out.println(i);
        }
        while (x < 50000) {
            x++;
        }
        do {
            x++
        }
        while (x < 10000);
        switch (a) {
            case 0:
                doCase0();
                break;
            default:
                doDefault();
        }
        try (MyResource r1 = getResource(); MyResource r2 = null) {
            doSomething();
        }
        catch (Exception e) {
            processException(e);
        }
        finally {
            processFinally();
        }
        do {
            x--;
        }
        while (x > 10)
    }

    public static void test()
            throws Exception
    {
        foo.foo().bar("arg1",
                "arg2");
        new Object() {};
    }

    class TestInnerClass {}

    interface TestInnerInterface {}
}

enum Breed
{
    Dalmatian(), Labrador(), Dachshund()
}

@Annotation1
@Annotation2
@Annotation3(param1 = "value1", param2 = "value2")
@Annotation4
class Foo
{
    @Annotation1
    @Annotation3(param1 = "value1", param2 = "value2")
    public static void foo()
    {
    }

    @Annotation1 @Annotation3(param1 = "value1", param2 = "value2") public static int myFoo;

    public void method(@Annotation1 @Annotation3(param1 = "value1", param2 = "value2") final int param)
    {
        @Annotation1 @Annotation3(param1 = "value1", param2 = "value2") final int localVariable;
    }
}
```

### Blank Lines
```java
/*
 * This is a sample file.
 */
package com.intellij.samples;

import com.intellij.idea.Main;

import javax.swing.*;

import java.util.Vector;

public class Foo
{
    private int field1;
    private int field2;

    public void foo1()
    {
        new Runnable()
        {
            public void run()
            {
            }
        }
    }

    public class InnerClass
    {
    }
}

class AnotherClass
{
}

interface TestInterface
{
    int MAX = 10;
    int MIN = 1;

    void method1();

    void method2();
}
```

### JavaDoc

#### General guidelines

* Do not include `@author` tags. The commit history is enough for this purpose.

#### Example

```java
package sample;

public class Sample
{
    /**
     * This is a method description that is long enough to exceed right margin.
     * <p/>
     * Another paragraph of the description placed after blank line.
     * <p/>
     * Line with manual
     * line feed.
     *
     * @param i short named parameter description
     * @param longParameterName long named parameter description
     * @param missingDescription
     * @return return description.
     * @throws XXXException description.
     * @throws YException description.
     * @throws ZException
     * @invalidTag
     */
    public abstract String sampleMethod(int i, int longParameterName, int missingDescription)
            throws XXXException, YException, ZException;

    /**
     * One-line comment
     */
    public abstract String sampleMethod2();

    /**
     * Simple method description
     *
     * @return
     */
    public abstract String sampleMethod3();
```

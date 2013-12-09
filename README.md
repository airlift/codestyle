# Code style for Airlift projects

## IntelliJ IDEA 13 on Mac OS X

To install, copy `IntelliJIdea13/Airlift.xml` into `~/Library/Preferences/IntelliJIdea13/codestyles`


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
            throws XXXException, YException,
            ZException;

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

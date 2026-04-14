# Java Notes (TCS IPA Quick Reference)

This file is a compact cheat sheet for common TCS IPA-style Java programs: read input → create objects → call static methods → print results.

## 1) Scanner input (common pitfall)

When mixing `nextInt()/nextDouble()/nextBoolean()` with `nextLine()`, remember `nextLine()` reads the *rest of the current line*.

```java
Scanner sc = new Scanner(System.in);

int rollNo = sc.nextInt();
sc.nextLine();          // consume endline after nextInt

String name = sc.nextLine();
double score = sc.nextDouble();
boolean dayScholar = sc.nextBoolean();
sc.nextLine();          // consume endline after nextBoolean (if next read is nextLine)
```

## 2) Classes and objects

```java
class Student {
    private int rollNo;
    private String name;
    private String branch;
    private double score;
    private boolean dayScholar;

    public Student(int rollNo, String name, String branch, double score, boolean dayScholar) {
        this.rollNo = rollNo;
        this.name = name;
        this.branch = branch;
        this.score = score;
        this.dayScholar = dayScholar;
    }

    public int getRollNo() { return rollNo; }
    public String getName() { return name; }
    public String getBranch() { return branch; }
    public double getScore() { return score; }
    public boolean isDayScholar() { return dayScholar; }

    public void setRollNo(int rollNo) { this.rollNo = rollNo; }
    public void setName(String name) { this.name = name; }
    public void setBranch(String branch) { this.branch = branch; }
    public void setScore(double score) { this.score = score; }
    public void setDayScholar(boolean dayScholar) { this.dayScholar = dayScholar; }
}

// Creating objects
Student s1 = new Student(101, "John", "IT", 85.5, true);

// Array of objects
Student[] students = new Student[4];
students[0] = new Student(101, "John", "IT", 85.5, true);
students[1] = new Student(102, "Jane", "ECE", 90.0, false);
```

## 3) Loops

```java
// for
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

// enhanced for (for-each)
for (Student s : students) {
    System.out.println(s.getName());
}

// while
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}

// do-while
int j = 0;
do {
    System.out.println(j);
    j++;
} while (j < 5);
```

## 4) Conditionals

```java
// if / else-if / else
if (score > 80) {
    System.out.println("Pass");
} else if (score > 50) {
    System.out.println("Average");
} else {
    System.out.println("Fail");
}

// null check
if (obj != null) {
    System.out.println(obj.toString());
} else {
    System.out.println("Not found");
}

// boolean check
if (s.isDayScholar()) {
    // true
}
if (!s.isDayScholar()) {
    // false
}

// ternary
String result = (score > 80) ? "Pass" : "Fail";

// switch
switch (grade) {
    case "A":
        System.out.println("Excellent");
        break;
    case "B":
        System.out.println("Good");
        break;
    default:
        System.out.println("Average");
}
```

## 5) String operations

```java
String s = "Hello World";

// basic
s.length();
s.charAt(0);
s.substring(0, 5);
s.substring(6);

// case
s.toUpperCase();
s.toLowerCase();

// search
s.contains("World");
s.indexOf("World");
s.lastIndexOf("l");
s.startsWith("Hello");
s.endsWith("World");

// comparison
s.equals("Hello World");
s.equalsIgnoreCase("hello world");
s.compareTo("Hello");
s.compareToIgnoreCase("hello");

// modification (returns new String)
s.trim();
s.replace("Hello", "Hi");
s.replaceAll("[aeiou]", "*");

// split
String[] parts = s.split(" ");

// concatenation
String joined = String.join("-", "a", "b", "c");

// empty checks
s.isEmpty();
// s.isBlank(); // Java 11+
```

## 6) Arrays

```java
int[] arr = new int[5];
int[] arr2 = {1, 2, 3, 4, 5};

arr[0] = 10;
int len = arr.length;

Arrays.sort(arr2);

// descending (needs wrapper type)
Integer[] arr3 = {5, 3, 8, 1};
Arrays.sort(arr3, Collections.reverseOrder());

int[] copy = Arrays.copyOf(arr2, arr2.length);
int[] partial = Arrays.copyOfRange(arr2, 1, 4);

System.out.println(Arrays.toString(arr2));

Arrays.fill(arr, 0);

// binarySearch requires sorted array
int index = Arrays.binarySearch(arr2, 3);
```

## 7) ArrayList

```java
ArrayList<Student> list = new ArrayList<>();

list.add(s1);
list.add(0, new Student(103, "Alex", "IT", 88.0, false));

Student first = list.get(0);
int size = list.size();

list.set(0, new Student(104, "Sam", "CSE", 77.0, true));

list.remove(0);      // by index
list.remove(s1);     // by object

list.contains(s1);
list.isEmpty();
list.indexOf(s1);

for (Student st : list) {
    System.out.println(st.getName());
}

// Array -> ArrayList
String[] stringArray = {"a", "b"};
ArrayList<String> list2 = new ArrayList<>(Arrays.asList(stringArray));

// ArrayList -> Array
String[] arr = list2.toArray(new String[0]);
```

## 8) Sorting (arrays and lists)

```java
// arrays
Arrays.sort(arr2);

// list: ascending / descending by score
list.sort((a, b) -> Double.compare(a.getScore(), b.getScore()));
list.sort((a, b) -> Double.compare(b.getScore(), a.getScore()));

// list: by name (alphabetical)
list.sort((a, b) -> a.getName().compareTo(b.getName()));
list.sort((a, b) -> a.getName().compareToIgnoreCase(b.getName()));

// list: by rollNo
list.sort((a, b) -> Integer.compare(a.getRollNo(), b.getRollNo()));

// comparator helper methods
list.sort(Comparator.comparingDouble(Student::getScore));
list.sort(Comparator.comparingDouble(Student::getScore).reversed());
list.sort(Comparator.comparingInt(Student::getRollNo));
list.sort(Comparator.comparing(Student::getName));

// multiple criteria: branch asc, score desc
list.sort(
    Comparator.comparing(Student::getBranch)
        .thenComparing(Comparator.comparingDouble(Student::getScore).reversed())
);
```

## 9) Finding max / min / second highest

```java
// max
Student maxStudent = students[0];
for (Student s : students) {
    if (s.getScore() > maxStudent.getScore()) {
        maxStudent = s;
    }
}

// min
Student minStudent = students[0];
for (Student s : students) {
    if (s.getScore() < minStudent.getScore()) {
        minStudent = s;
    }
}

// second highest by sorting (ensure size >= 2)
ArrayList<Student> list = new ArrayList<>();
Collections.addAll(list, students);
list.sort((a, b) -> Double.compare(b.getScore(), a.getScore()));
Student secondHighest = (list.size() >= 2) ? list.get(1) : null;

// second highest without sorting
double highest = Double.NEGATIVE_INFINITY;
double second = Double.NEGATIVE_INFINITY;
for (Student s : students) {
    double val = s.getScore();
    if (val > highest) {
        second = highest;
        highest = val;
    } else if (val > second && val < highest) {
        second = val;
    }
}
```

## 10) Counting and filtering

```java
// count with condition
int count = 0;
for (Student s : students) {
    if (s.isDayScholar() && s.getScore() > 80) {
        count++;
    }
}

// filter to new list
ArrayList<Student> nonDayScholars = new ArrayList<>();
for (Student s : students) {
    if (!s.isDayScholar()) {
        nonDayScholars.add(s);
    }
}

// case-insensitive equals
ArrayList<Student> itStudents = new ArrayList<>();
for (Student s : students) {
    if (s.getBranch().equalsIgnoreCase("IT")) {
        itStudents.add(s);
    }
}

// case-insensitive contains
if (s.getName().toLowerCase().contains("kumar")) {
    // ...
}

// startsWith / endsWith (case-insensitive)
if (s.getName().toLowerCase().startsWith("a")) {
    System.out.println(s.getName());
}
```

## 11) HashMap

```java
HashMap<String, Integer> map = new HashMap<>();
map.put("John", 85);
map.put("Jane", 90);

map.get("John");
map.getOrDefault("Unknown", 0);

map.containsKey("John");
map.containsValue(85);
map.size();
map.isEmpty();

map.remove("John");

for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " : " + entry.getValue());
}

for (String key : map.keySet()) {
    System.out.println(key);
}

for (int value : map.values()) {
    System.out.println(value);
}

// count occurrences pattern
HashMap<String, Integer> countMap = new HashMap<>();
for (Student s : students) {
    String branch = s.getBranch();
    countMap.put(branch, countMap.getOrDefault(branch, 0) + 1);
}
```

## 12) Common IPA problem patterns

```java
// return object or null
public static Student findStudent(Student[] students) {
    for (Student s : students) {
        if (s.getScore() > 90) {
            return s;
        }
    }
    return null;
}

// formatted output
System.out.println(s.getRollNo() + "#" + s.getName() + "#" + s.getScore());

// average pattern
double sum = 0;
int count = 0;
for (Student s : students) {
    if (s.getBranch().equalsIgnoreCase("IT")) {
        sum += s.getScore();
        count++;
    }
}
double average = (count > 0) ? sum / count : 0;
```

## 13) Type casting and parsing

```java
// numeric conversions
int a = 5;
double b = (double) a;

double x = 9.8;
int y = (int) x;

// string -> number
int n = Integer.parseInt("123");
double d = Double.parseDouble("12.5");
float f = Float.parseFloat("3.14");
long l = Long.parseLong("123456");
boolean ok = Boolean.parseBoolean("true");

// number -> string
String s1 = String.valueOf(123);
String s2 = Integer.toString(123);
String s3 = Double.toString(12.5);

// char <-> int
char c = 'A';
int ascii = (int) c;
char ch = (char) 65;
```

## 14) Exception handling

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
} catch (Exception e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("This always runs");
}
```

## 15) Common imports

```java
import java.util.Scanner;
import java.util.Arrays;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

// or
import java.util.*;
```

## 16) Sample full program template (common IPA style)

```java
import java.util.*;

public class Solution {
    public static int findCountOfDayScholarStudents(Student[] students) {
        int count = 0;
        for (Student s : students) {
            if (s.isDayScholar() && s.getScore() > 80) {
                count++;
            }
        }
        return count;
    }

    // Example: 2nd highest score among NON day-scholars
    public static Student findStudentWithSecondHighestScore(Student[] students) {
        ArrayList<Student> list = new ArrayList<>();
        for (Student s : students) {
            if (!s.isDayScholar()) {
                list.add(s);
            }
        }
        if (list.size() < 2) {
            return null;
        }
        list.sort((a, b) -> Double.compare(b.getScore(), a.getScore()));
        return list.get(1);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        Student[] students = new Student[4];
        for (int i = 0; i < students.length; i++) {
            int rollNo = sc.nextInt();
            sc.nextLine();
            String name = sc.nextLine();
            String branch = sc.nextLine();
            double score = sc.nextDouble();
            boolean dayScholar = sc.nextBoolean();
            sc.nextLine();

            students[i] = new Student(rollNo, name, branch, score, dayScholar);
        }

        int count = findCountOfDayScholarStudents(students);
        System.out.println(count > 0 ? count : "No students found");

        Student second = findStudentWithSecondHighestScore(students);
        if (second != null) {
            System.out.println(second.getRollNo() + "#" + second.getName() + "#" + second.getScore());
        } else {
            System.out.println("No student found");
        }
    }
}

class Student {
    private int rollNo;
    private String name;
    private String branch;
    private double score;
    private boolean dayScholar;

    public Student(int rollNo, String name, String branch, double score, boolean dayScholar) {
        this.rollNo = rollNo;
        this.name = name;
        this.branch = branch;
        this.score = score;
        this.dayScholar = dayScholar;
    }

    public int getRollNo() { return rollNo; }
    public String getName() { return name; }
    public String getBranch() { return branch; }
    public double getScore() { return score; }
    public boolean isDayScholar() { return dayScholar; }
}
```

## Quick reference table

| Operation | Syntax | Notes |
|---|---|---|
| Read `int` | `sc.nextInt()` | Use `sc.nextLine()` after if next is a full line |
| Read `String` line | `sc.nextLine()` | Reads the rest of the current line |
| Read `double` | `sc.nextDouble()` | Don’t put `nextLine()` before reading a same-line boolean |
| Read `boolean` | `sc.nextBoolean()` | Call `nextLine()` after if next read is `nextLine()` |
| Array length | `arr.length` | No parentheses |
| ArrayList size | `list.size()` | Has parentheses |
| String length | `str.length()` | Has parentheses |
| Sort ascending | `list.sort(Comparator.comparingDouble(...))` | Or lambda `(a,b) -> ...` |
| Sort descending | `list.sort(Comparator.comparingDouble(...).reversed())` |  |
| Case-insensitive equals | `a.equalsIgnoreCase(b)` |  |
| Null check | `if (obj != null)` |  |
| Boolean check | `if (flag)` / `if (!flag)` | Prefer `isX()` for booleans |
| Print formatted | `System.out.println(a + "#" + b + "#" + c)` | Common IPA output style |

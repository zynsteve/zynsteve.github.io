---
title: Java Language Features
description: Java language features
categories:
- Notes
tags:
- Java
---


![java](/assets/images/post/java-language-features/java.png)


```Java
/**
 * Parses the specified string as a signed decimal integer value.
 *
 * @param string
 *            the string representation of an integer value.
 * @return an {@code Integer} instance containing the integer value
 *         represented by {@code string}.
 * @throws NumberFormatException
 *             if {@code string} cannot be parsed as an integer value.
 * @see #parseInt(String)
 */
public static Integer valueOf(String string) throws NumberFormatException {
    return valueOf(parseInt(string));
}
```

```Java
/**
 * Parses the specified string as a signed decimal integer value. The ASCII
 * character \u002d ('-') is recognized as the minus sign.
 *
 * @param string
 *            the string representation of an integer value.
 * @return the primitive integer value represented by {@code string}.
 * @throws NumberFormatException
 *             if {@code string} cannot be parsed as an integer value.
 */
public static int parseInt(String string) throws NumberFormatException {
    return parseInt(string, 10);
}
```
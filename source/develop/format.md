# Code Format

The _T2-Project_ uses the following conventions to format (Java) code:

- max line length between 100 to 120 chars (except for long String literals)
- spaces instead of tabs
- 4 spaces per indentation level
- LF instead of CRLF
- lines that were broken up in the middle (i.e. new parameter or array value) are indented by +1:
```java
@SpringBootApplication(scanBasePackageClasses = {
    Some.class,
    SomeOther.class })
```
- `*` imports as soon as there are 2 imports of the same package:
- blank lines must also be empty (no `            ` lines)
- one space between parameters (`doSomething(String a, String b)`)
- one space between the curly parentheses of arrays (`{ "Hi", "Second String" }`)
- no inline annotations except for parameters (no `@Autowired Someservice service;`)
- no aligned assignments
- aligned javadoc parameters:
```java
/**
 * Do something.
 *
 * @param x       a small parameter
 * @param longerY another longer parameter
 */
```


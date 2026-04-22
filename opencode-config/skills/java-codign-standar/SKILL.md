---
name: java-coding-standar
description: "Java coding standards"
---

# Java Coding Standards

Standards for readable, maintainable Java (21+) code in Spring Boot services.

## When to activate

- Structuring packages and project layout
- Enforcing naming, immutability, or exception handling conventions
- Writing or reviewing Java code in Spring Boot projects
- Working with records, sealed classes, or pattern matching (Java 21+)
- Reviewing use of Optional, streams, or generics

## Core Principles

- Prefer clarity over cleverness
- Immutable by default; minimize shared mutable state
- Fail fast with meaningful exceptions
- Consistent naming and package structure

## Project Structure (build.gradle.kts)

```
src/
	main/
		java/org/example/app/
			config/
			controller/
			datatype/
			dto/
			entity/
			exception/
			repository/
			service/
			util/
		resources/
			application.yml
	test/
		java/org/example/app/
			(mirrors main)
		test/resources
			application.yml
```

## Naming

```java
// Classes and Records as: PascalCase
public class ServiceName {}
public record RecordName(String name) {}

// Methods, Fields and Variables as: camelCase
private final FinalVariable finalVariable;
public void methodName(String variable) {}
String variableName = "";

// Constants as: UPPER_SNAKE_CASE
private static final String NAMING = "naming";
```

## Variable Declaration

```java
// PASS: Always use `var` when the variable's type is known on the same line
final var name = "named";
final var list = new ArrayList<ClassName>();

// FAIL: Using `var` when type is not known in the lane
final var name = doSomething();

// PASS: Use explicit variable type when not known in the lane
final String name = doSomething();
```

## Optional Usage

```java
public ClassName getById(final Long id) {
	Optional<ClassName> variableName = repository.findById(id);
	return variableName.orElseThrow(() -> new RuntimeException("Exception"));
}
```

## Streams Best Practices

```java
// PASS: Use streams for transformations, keep pipelines short
List<String> names = markets.stream()
    .map(Market::name)
    .filter(Objects::nonNull)
    .toList();

// FAIL: Avoid complex nested streams; prefer loops for clarity
```

## Exceptions

- Use unchecked exceptions for domain errors; wrap technical exceptions with context
- Create domain-specific exceptions (e.g., `MarketNotFoundException`)
- Avoid broad `catch (Exception ex)` unless rethrowing/logging centrally

```java
throw new MarketNotFoundException(slug);
```

## Code Formatting and Style

- Use 2 or 4 spaces consistently (project standard)
- One public top-level type per file
- Keep methods short and focused; extract helpers
- Order members: constants, fields, constructors, public methods, protected, private

## Code Smells to Avoid

- Long parameter lists → use DTO/builders
- Deep nesting → early returns
- Magic numbers → named constants
- Static mutable state → prefer dependency injection
- Silent catch blocks → log and act or rethrow

## Logging

```java
private static final Logger log = LoggerFactory.getLogger(MarketService.class);
log.info("fetch_market slug={}", slug);
log.error("failed_fetch_market slug={}", slug, ex);
```

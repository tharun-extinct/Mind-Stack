# Spring Boot Starter

`spring-boot-starter` pulls in the foundational modules of the Spring Framework:
- `spring-core`
- `spring-context`

*These modules are the heart of how Spring works.*

---

## ⚙️ Spring Core

**Spring Core** contains the core features of the Spring Framework:
- **Dependency Injection (DI)**
- **Inversion of Control (IoC) Container**
- **BeanFactory**
- **Core utilities** (reflection, resource loading, type conversion)

*This is the lowest-level module.*

> **💡 Analogy:**
> Think of Spring Core like **"The engine of a car."** Everything else sits on top of it. Without `spring-core`, nothing in Spring works.

---

## 🧠 Spring Context

**Spring Context** builds on top of Spring Core. 

It provides the **`ApplicationContext`** (the major component), which is the advanced container that manages:
- Bean creation & lifecycle
- Dependency wiring
- Event handling
- Internationalization (i18n)
- Resource loading
- Profiles & Environment abstraction

It also loads key annotations like:
`@Component` | `@Service` | `@Controller` | `@Repository` | `@Autowired` | `@Configuration` | `@Bean`

---

## 🔄 The Flow

- ✅ **Spring Core** = DI Infrastructure
- ✅ **Spring Context** = DI + extra features used by real applications

**How it all connects:**
1. **Core** provides the internal engine (`BeanFactory`).
2. **Context** enhances it and creates the `ApplicationContext`.
3. **Spring Boot** builds on top of Context to auto-configure everything.

---

## 📊 Summary Comparison

| Module | Role | Analogy |
| :--- | :--- | :--- |
| `spring-core` | Handles bean creation, wiring | The engine of a car |
| `spring-context` | Adds features, annotation support, events, `ApplicationContext` | The dashboard + controls using the engine |





`spring-boot-starter` pulls in the foundational modules of the Spring Framework:
    - `spring-core`
    - `spring-context`
They are the heart of how Spring works.


### Spring Core

Spring Core contains, the core features of the Spring Framework:

    - Dependency Injection (DI)
    - Inversion of Control (IoC) Container
    - `BeanFactory`
    - Core utilities (reflection, resource loading, type conversion)
This is the lowest-level module.

Think of Spring Core like:
> “The engine of a car. Everything else sits on top of it.” Without `spring-core`, nothing in Spring works.


### Spring Context 

Spring Context builds on top of Spring Core.
It provides:
`ApplicationContext` (major component)
This is the advanced container that manages:
    - Bean creation
    - Bean lifecycle
    - Dependency wiring
    - Event handling
    - Internationalization (i18n)
    - Resource loading
    - Profiles
    - Environment abstraction


It also loads annotations like:
    - `@Component`
    - `@Service`
    - `@Controller`
    - `@Repository`
    - `@Autowired`
    - `@Configuration`
    - `@Bean`




✅ Spring Core = DI Infrastructure
✅ Spring Context = DI + extra features used by real applications
Flow:
    1. Core provides the internal engine (`BeanFactory`)
    2. Context enhances it and creates the `ApplicationContext`
    3. Spring Boot builds on top of Context to auto-configure everything


| Module | Role | Analogy |
|---|---|---|
| `spring-core` | Handles bean creation, wiring | The engine of a car |
| `spring-context` | Adds features, annotation support, events, `ApplicationContext` | The dashboard + controls using the engine |

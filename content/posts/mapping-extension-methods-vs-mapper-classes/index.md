+++
title = 'Kotlin extension methods vs mapper classes for data transformation'
date = 2025-01-16T12:00:00+02:00
categories = ['Android development']
tags = ['blog', 'android', 'architecture']
+++ 
---
As an Android Developer like me, you're likely familiar with the concept of data mapping: converting data between different layers of your application, such as from the data layer to the domain layer or presentation layer. Kotlin offers two popular ways to achieve this: **extension methods** and **mapper classes**. But when should you use which approach? In this blog post, we'll compare both methods and demonstrate how to use them in practice.

---

## **What are Extension Methods?**

Extension methods in Kotlin are a powerful feature that allows you to add new functions to existing classes without modifying them. This makes them ideal for simple, straightforward mapping logic.

### **Example: Mapping with Extension Methods**

Here is an example where a simple DTO (Data Transfer Object) is converted to a domain model:

```
// Data Transfer Object (DTO)
data class UserDto(val id: String, val name: String)

// Domain model
data class User(val userId: String, val fullName: String)

// Extension Method for mapping
fun UserDto.toDomainModel(): User {
    return User(
        userId = this.id,
        fullName = this.name
    )
}

// Usage
fun main() {
    val userDto = UserDto(id = "123", name = "John Doe")
    val user = userDto.toDomainModel()
    println(user) // Output: User(userId=123, fullName=John Doe)
}
```

### **Advantages of Extension Methods**

- **Compact and readable**: Less boilerplate code.
    
- **Scoped**: Mapping logic is defined close to the model.
    
- **Lightweight**: No need for additional classes.
    

---

## **What are Mapper Classes?**

A mapper class is a separate component dedicated to converting data. This approach follows the **Single Responsibility Principle** (SRP) and is ideal for more complex or reusable mappings.

### **Example: Mapping with a Mapper Class**

Here is an example of a mapper class:

```
// Data Transfer Object (DTO)
data class UserDto(val id: String, val name: String)

// Domain model
data class User(val userId: String, val fullName: String)

// Mapper Class
class UserMapper {
    fun mapToDomain(userDto: UserDto): User {
        return User(
            userId = userDto.id,
            fullName = userDto.name
        )
    }
}

// Usage
fun main() {
    val userDto = UserDto(id = "123", name = "John Doe")
    val mapper = UserMapper()
    val user = mapper.mapToDomain(userDto)
    println(user) // Output: User(userId=123, fullName=John Doe)
}
```

### **Advantages of Mapper Classes**

- **Scalability**: Ideal for complex mappings.
    
- **Reusability**: Mapping logic can be easily shared.
    
- **Testability**: Easy to unit test without depending on specific objects.
    
- **Architectural consistency**: Keeps your codebase organized in larger projects.
    

---

## **When to Use What?**

The choice between extension methods and mapper classes depends on the complexity of your project and your architectural requirements:

### Use Extension Methods:

- For simple, direct mappings.
    
- When your codebase is small, and you want to minimize overhead.
    

### Use Mapper Classes:

- For complex mappings or mappings dependent on external sources (e.g., configurations).
    
- When reusability and testability are key factors.
    
- In larger projects where clear separation of responsibilities is needed.
    

---

## **Conclusion**

The choice between extension methods and mapper classes depends on the context of your project. For simple mappings, extension methods are quick and effective. For larger, more complex projects, mapper classes offer better scalability, reusability, and testability.

By experimenting with both approaches, you can determine what works best for your codebase. Happy coding! 🚀
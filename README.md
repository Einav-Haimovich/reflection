# .NET Reflection

Hands-on .NET Reflection examples covering type lookup, member invocation, generics, and unsafe accessors.

---

## What Is Reflection

**[WhatIsReflection](WhatIsReflection/)** - Entry point to runtime type introspection via `GetType()` and the `Type` object.

Useful when you need to inspect an object's type at runtime without knowing it at compile time — the foundation for everything that follows.

_Learned: every object carries its type metadata at runtime; `GetType()` is the gateway to all reflection APIs._

---

## Finding Types

**[FindingTypes](FindingTypes/)** - Scanning assemblies, looking up types by name or namespace, and filtering by characteristics (sealed, abstract, interface, etc.).

Useful for plugin systems, dependency injection containers, or any tool that discovers types at startup rather than hard-coding them.

_Learned: `Assembly.GetTypes()` gives you everything in an assembly; use `Type` predicates to filter down to what you need._

---

## Attributes

**[Attributes](Attributes/)** - Defining custom attributes, applying usage restrictions (`AttributeUsage`), and reading attribute values from types at runtime.

Useful for frameworks that attach metadata to types or members — validation libraries, serializers, ORMs.

_Learned: attributes are just classes; `GetCustomAttribute<T>()` retrieves them, and `AttributeUsage` controls where they can appear._

---

## Member Information

**[MemberInformation](MemberInformation/)** - Enumerating members with `BindingFlags`, reading and writing properties and fields, invoking methods and constructors dynamically.

Useful for generic mappers, serializers, or test helpers that need to interact with members without knowing them at compile time.

_Learned: `BindingFlags` is the key to controlling which members you see (public/private, instance/static); `MethodInfo.Invoke` and `PropertyInfo.SetValue` let you drive them dynamically._

---

## Generics

**[Generics](Generics/)** - Inspecting open vs closed generic types, calling generic methods with `MakeGenericMethod`, and instantiating generic types at runtime.

Useful when writing utility code that must work with `List<T>`, `Dictionary<K,V>`, or any user-defined generic type discovered at runtime.

_Learned: generic types have an "open" form (`List<>`) you can close at runtime with `MakeGenericType`; same pattern applies to methods with `MakeGenericMethod`._

---

## Performance

**[Benchmarks](Benchmarks/)** - BenchmarkDotNet comparisons of object creation and member invocation: `Activator.CreateInstance` vs compiled expressions vs direct construction; raw reflection vs caching.

**[UnsafeAccessor](UnsafeAccessor/)** - `[UnsafeAccessor]` attribute as a zero-overhead alternative to reflection for accessing private members and methods.

_Learned: reflection pays a cost per-call; caching `MethodInfo`/`PropertyInfo` recovers most of it. `UnsafeAccessor` eliminates the cost entirely for private-member access — as fast as direct calls._

---

## How to Run

```bash
# build everything
dotnet build Reflection.slnx

# run a specific module
dotnet run --project FindingTypes/FindingTypes.csproj
dotnet run --project MemberInformation/MemberInformation.csproj

# run benchmarks (release mode required)
dotnet run --project Benchmarks/Benchmarks.csproj -c Release
```

---

## Folder Structure

```
reflection/
├── WhatIsReflection/   intro — GetType() and Type basics
├── FindingTypes/       assembly scanning and type lookup
├── Attributes/         custom attributes and runtime discovery
├── MemberInformation/  BindingFlags, properties, fields, methods
├── Generics/           open/closed generics and MakeGenericMethod
├── Benchmarks/         BenchmarkDotNet performance comparisons
├── UnsafeAccessor/     zero-cost private member access
└── SharedTypes/        support library used by FindingTypes and Benchmarks
```

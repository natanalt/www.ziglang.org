---
title: "Dlaczego Zig, skoro już istnieją C++, D czy Rust?"
mobile_menu_title: "Dlaczego Zig, skoro..."
toc: true
---


## Brak ukrytego przepływu kontroli

Jeśli kod Zig nie wygląda, że może przeskoczyć do potencjalnie wywołanej funkcji, to on tego nie robi. Dzięki temu możesz mieć pewność, że poniższy kod jedynie wywołuje funkcje `foo()`, a potem `bar()` i to zachowanie jest gwarantowane, bez wymaganej wiedzy o typach czegokolwiek:

```zig
var a = b + c.d;
foo();
bar();
```

Przykłady ukrytego przepływu kontroli:

* D posiada `@property`, czyli metody, które są wywołane w sposób który wygląda jak dostęp do pola, więc w powyższym przykładzie, `c.d` mogłoby wywołać funkcję.
* C++, D oraz Rust mają przeładowywanie operatorów, więc operator `+` może potencjalnie wywołać funkcję.
* C++, D oraz Go posiadają wyjątki w postaci throw/catch, więc `foo()` może wywołać wyjątek, sprawiając, że funkcja `bar()` nie zostanie wykonana. (Oczywiście, nawet w języku Zig funkcja `foo()` może spowodować tzw. deadlock, przez co `bar()` nigdy się nie wykona. Jest to jednak nieunikalne w każdym języku, którego cechuje kompletność Turinga.)

Celem tej decyzji projektowej jest polepszenie czytelności kodu.

## Brak ukrytych alokacji

Zig ma bardzo proste podejście do dynamicznej alokacji pamięci. Nie ma słowa kluczowego typu `new`,
ani żadnych innych elementów językowych, które mogłyby go używać (np. opeartor konkatenacji ciągów[1]).
Dynamiczna alokacja jest zarządzana przez kod bibliotek i aplikacji, nie przez język.

Przykłady ukrytych alokacji::

* Słowo `defer` w języku Go alokuje pamięć na lokalnym stosie funkcji. Jest to nieintuicyjna metoda na
  zarządzanie przepływem kontroli, może spowodować błędy braku pamięci, jeśli `defer` jest użyte w pętli.
* W języku C++, wywoływanie funkcji tzw. coroutine powoduje dynamiczną alokację pamięci.
* W Go, wywoływanie funkcji może powodować dynamiczną alokację pamięci, gdy tzw. goroutiny alokują małe
  stosy, gdy miejsce na głównym stosie się zmniejsza.
* Główna standardowa biblioteka języka Rust panic'uje, gdy zabraknie pamięci. Alternatywne interfejsy
  dla alokatorów są drugorzędne ([rust-lang/rust#29802](https://github.com/rust-lang/rust/issues/29802))

Nearly all garbage collected languages have hidden allocations strewn about, since the
garbage collector hides the evidence on the cleanup side.

The main problem with hidden allocations is that it prevents the *reusability* of a
piece of code, unnecessarily limiting the number of environments that code would be
appropriate to be deployed to. Simply put, there are use cases where one must be able
to rely on control flow and function calls not to have the side-effect of memory allocation,
therefore a programming language can only serve these use cases if it can realistically
provide this guarantee.

In Zig, there are standard library features that provide and work with heap allocators,
but those are optional standard library features, not built into the language itself.
If you never initialize a heap allocator, you can be confident your program will not heap allocate.

Every standard library feature that needs to allocate heap memory accepts an `Allocator` parameter
in order to do it. This means that the Zig standard library supports freestanding targets. For
example `std.ArrayList` and `std.AutoHashMap` can be used for bare metal programming!

Custom allocators make manual memory management a breeze. Zig has a debug allocator that
maintains memory safety in the face of use-after-free and double-free. It automatically
detects and prints stack traces of memory leaks. There is an arena allocator so that you can
bundle any number of allocations into one and free them all at once rather than manage
each allocation independently. Special-purpose allocators can be used to improve performance
or memory usage for any particular application's needs.

[1]: Actually there is a string concatenation operator (generally an array concatenation operator), but it only works at compile time, so it still doesn't do any runtime heap allocation.

## First-class support for no standard library

As hinted above, Zig has an entirely optional standard library. Each std lib API only gets compiled
into your program if you use it. Zig has equal support for either linking against libc or
not linking against it. Zig is friendly to bare-metal and high-performance development.

It's the best of both worlds; for example in Zig, WebAssembly programs can both use
the normal features of the standard library, and still result in the tiniest binaries when
compared to other programming languages that support compiling to WebAssembly.

## A Portable Language for Libraries

One of the holy grails of programming is code reuse. Sadly, in practice, we find ourselves re-inventing the wheel many times over again. Often it's justified.

 * If an application has real-time requirements, then any library that uses garbage collection or any other non-deterministic behavior is disqualified as a dependency.
 * If a language makes it too easy to ignore errors, and thus hard to verify that a library correctly handles and bubbles up errors, it can be tempting to ignore the library and re-implement it, knowing that one handled all the relevant errors correctly. Zig is designed such that the laziest thing a programmer can do is handle errors correctly, and thus one can be reasonably confident that a library will properly bubble errors up.
 * Currently it is pragmatically true that C is the most versatile and portable language. Any language that does not have the ability to interact with C code risks obscurity. Zig is attempting to become the new portable language for libraries by simultaneously making it straightforward to conform to the C ABI for external functions, and introducing safety and language design that prevents common bugs within the implementations.

## A Package Manager and Build System for Existing Projects

Zig is a programming language, but it also ships with a build system and package manager that are intended to be useful even in the context of a traditional C/C++ project.

Not only can you write Zig code instead of C or C++ code, but you can use Zig as a replacement for autotools, cmake, make, scons, ninja, etc. And on top of this, it (will) provide a package manager for native dependencies. This build system is intended to be appropriate even if the entirety of a project's codebase is in C or C++.

System package managers such as apt-get, pacman, homebrew, and others are instrumental for end user experience, but they can be insufficient for the needs of developers. A language-specific package manager can be the difference between having no contributors and having many. For open source projects, the difficulty of getting the project to build at all is a huge hurdle for potential contributors. For C/C++ projects, having dependencies can be fatal, especially on Windows, where there is no package manager. Even when just building Zig itself, most potential contributors have a difficult time with the LLVM dependency. Zig is (will be) offering a way for projects to depend on native libraries directly - without depending on the users' system package manager to have the correct version available, and in a way that is practically guaranteed to successfully build projects on the first try regardless of what system is being used and independent of what platform is being targeted.

Zig is offering to replace a project's build system with a reasonable language using a declarative API for building projects, that also provides package management, and thus the ability to actually depend on other C libraries. The ability to have dependencies enables higher level abstractions, and thus the proliferation of reusable high-level code.

## Simplicity

C++, Rust, and D have such a large number of features that they can be distracting from the actual meaning of the application you are working on. One finds oneself debugging one's knowledge of the programming language instead of debugging the application itself.

Zig has no macros and no metaprogramming, yet is still powerful enough to express complex programs in a clear, non-repetitive way. Even Rust has macros with special cases like `format!`, which is implemented in the compiler itself. Meanwhile in Zig, the equivalent function is implemented in the standard library with no special case code in the compiler.

## Tooling

Zig can be downloaded from [the downloads section](/download/).  Zig provides binary archives for Linux, Windows, macOS and FreeBSD. The following describes what you get with one of these archives:

* installed by downloading and extracting a single archive, no system configuration needed
* statically compiled so there are no runtime dependencies
* uses the mature well-supported LLVM infrastructure which enables deep optimization and support for most major platforms
* out of the box cross-compilation to most major platforms
* ships with source code for libc that will be dynamically compiled when needed for any supported platform
* includes build system with caching
* compiles C and C++ code with libc support

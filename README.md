introduction to our project:
We developed a live chatting server using some implementations (sockets, blinding and other
implementations that we will explain about it in details), Our Project runs by two devices, Server and
Client, there can be more than one client connected to the server with different names and Password, for
all clients to connect to the same server using different computers and networks they must all be
connected to the same VPN tunnel. The connection is between 2 devices, each device has different port
number and IP, every device plays a different role and perform different tasks, in our case the two
devices are “Server” and “Client”, While server is active it is continually waiting for incoming connections
and that is called “Listening”.
Explanation of the project:
1. We first create a User.h header file that contains the following:
• name: a string representing the user's name
• password: a string representing the user's password
• ip: an object of type IpAddress representing the user's IP address
• port: an unsigned short integer representing the port number that the user is connected through
• isActive: a boolean variable representing whether the user is currently active or not. This variable
is initialized to 0, or false.
The #pragma once directive tells the compiler to include this header file only once in a single compilation.
This can be useful for preventing multiple definitions of the same entity in a project.
2. Then we create Server.h header file that is implementing a simple chat server in C++
using the SFML library. The server listens for incoming messages on a socket and
processes them based on their type:
The Server namespace contains several variables and functions:
• ip: an object of type IpAddress representing the server's local IP address.
• sock: an object of type UdpSocket representing the server's socket, through which it listens for
incoming messages.
• port: an unsigned short integer representing the port number that the server is listening on.
• Users: a vector of User objects, representing the clients that are currently connected to the
server.
• DownloadUsers(): a function that reads in a list of user accounts from a file called "Accounts.txt",
and stores them in the Users vector.
• UploadUsers(): a function that writes the list of user accounts in the Users vector to the
"Accounts.txt" file.
• NewMessage(): a function that listens for incoming messages on the socket, and processes them
based on their type.
COE303 - Operating Systems Term Project Report.
Fouad Fares - 200722115, Majd Al-Ali Al-Hamad - 200722129, Usama Ahmet Kamil – 200722106
2
The NewMessage() function contains a loop that listens for incoming messages indefinitely. When a
message is received, it is processed based on its type:
• If the type is "Connect", the server attempts to either register a new user account or log in an
existing user, based on the username and password provided in the message. If registration is
successful, the new user's information is added to the Users vector, and the "Accounts.txt" file is
updated. If login is successful, the user's isActive flag is set to true.
• If the type is "Message", the server broadcasts the message to all connected users.
• If the type is "Disconnect", the server sets the user's isActive flag to false and removes them from
the Users vector.
3. Then we create Client.h header file that is implementing a simple chat client in C++ using
the SFML library. The client connects to a server, and allows the user to send and receive
messages:
The Client namespace contains several variables and functions:
• sendIP: an object of type IpAddress representing the IP address of the server to which the client is
connecting.
• sock: an object of type UdpSocket representing the client's socket, through which it
communicates with the server.
• port: an unsigned short integer representing the port number that the client is using for its
socket.
• SPort: an unsigned short integer representing the port number of the server.
• CheckMessage(): a function that allows the user to enter and send messages to the server.
• Connect(): a function that prompts the user for the server's IP address and port, and sends a
"Connect" message to the server to initiate the connection.
• Startup(): a function that calls the Connect() function to establish a connection with the server,
and then starts a separate thread to handle user input and message sending. It also listens for
incoming messages indefinitely, and prints them to the console when they are received.
The Startup() function first calls the Connect() function to establish a connection with the server. It then
starts a separate thread to handle user input and message sending using the CheckMessage() function.
The Startup() function then enters a loop that listens for incoming messages indefinitely, and prints them
to the console when they are received.
4. Then we create Chat.cpp that is the main entry point for a simple chat program in
C++ using the SFML library. It allows the user to run the program either as a server
or a client, based on user input:
The code begins by setting the console code page to 1251, which allows it to display and handle Cyrillic
characters. It then prompts the user to enter either 's' or 'c', indicating whether they want to run the
program in server mode or client mode.
COE303 - Operating Systems Term Project Report.
Fouad Fares - 200722115, Majd Al-Ali Al-Hamad - 200722129, Usama Ahmet Kamil – 200722106
3
If the user enters 's', the program calls the Startup() function from the Server namespace, which starts
the chat server. If the user enters 'c', the program calls the Startup() function from the Client
namespace, which starts the chat client.
This code includes several header files:
• SFML/Network.hpp: the SFML library's networking module, which provides classes for
networking and communication over a network.
• Windows.h: a Windows-specific header file that provides various functions and variables for
interacting with the Windows operating system.
• iostream: the input/output stream library, which provides input and output streams (e.g., cin,
cout) for reading and writing data.
• fstream: the file stream library, which provides classes for reading and writing to files.
• string: the string library, which provides string manipulation functions and the string class.
• thread: the thread library, which provides classes and functions for creating and manipulating
threads.
• chrono: the chrono library, which provides classes and functions for representing and
manipulating time.
The code also includes three header files that are specific to this project:
• User.h: a header file that defines the User struct, which represents a user in the chat program.
• Client.h: a header file that defines the Client namespace, which contains functions and
variables for the chat client.
• Server.h: a header file that defines the Server namespace, which contains functions and
variables for the chat server.

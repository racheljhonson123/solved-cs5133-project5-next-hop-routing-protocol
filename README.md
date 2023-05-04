Download Link: https://assignmentchef.com/product/solved-cs5133-project5-next-hop-routing-protocol
<br>
The objective of this programming project is to implement a software router which can route data packets from source client to destination host machine. This will help students to understand router to router interaction using UDP socket interface in C programming language. After completing the project, students will have an intermediate understanding of the adapted next-hop routing protocol and steps require for developing a networking application to route data packets to destination node.

<ol start="2">

 <li><strong>Project Specification:</strong></li>

</ol>

<ul>

 <li><strong>Overall System Behavior: </strong></li>

</ul>

You are required to implement an adapted next-hop routing protocol which will route the client packet(s) to a destination node. The following figure shows high-level overall system requirements.

In this project, you are required to write four programs, source client, server, router, and destination client. Client and server programs are very close to earlier projects where you had to implement user authentication using TCP connection and send data packets from clients to another node using UDP socket. The router program is new in which it will route the data packet received from client to proper destination based on neighbor list text file. Detail description of the client, server, and the router program along with input formats are specified below.

<ul>

 <li><strong>Input Format: </strong></li>

</ul>

Client, Server, and Router must be command-line tools that allow transmitting messages and supports the following parameters:

<strong>SourceClient</strong> &lt;clientPort&gt; &lt;serverIP&gt; &lt;serverPort&gt; &lt;routerIP&gt; &lt;routerPort&gt; &lt;destClientName&gt;

<strong> </strong>

<strong>Server</strong> &lt;server_port&gt;

<strong>Router</strong> &lt;routerPort&gt; &lt;neighborRouterIP&gt; &lt;neighborRouterPort&gt; &lt;neighborClientList_File&gt; <strong>DestinationClient</strong> &lt;clientPort&gt; &lt;routerIP&gt; &lt;routerPort&gt;




<ul>

 <li><strong>Client Behavior: </strong>

  <ul>

   <li>Your source client program takes <strong>six arguments</strong> from user during startup that specifies the port number of the client program, IP address and port number of the authentication server, IP address and port number of the <em>neighbor router</em> it will be associated with, and name of the destination host machine (e.g., gpel8.cs.ou.edu) where it wants to send the message (string).</li>

   <li>You have to use (<em>4000+last 4 digits of your student-id number</em>) to avoid requesting same port by multiple students. Incrementally use the client <strong>port number +1</strong> for the next client to avoid duplication.</li>

   <li>After a successful startup, client program will print a welcome message and ask the user to input <em>username and password</em> for login into the server. You need to create TCP connection between client and server program. The authentication process and error handling is same as earlier project(s). If login fails, the client will send <em>another pair of username and password</em> to server. Your program should handle all input errors.</li>

   <li>After successful login, your client program will send the <strong>destination client name</strong> (e.g., gpel8.cs.ou.edu) to retrieve the IP and port number of the machine. <u>If the name doesn’t match</u>, the server program will send appropriate negative message to resend a valid name.</li>

   <li>After retrieving IP and port from the server, your client program will prompt user to input a <em>message</em> that will be send to the destination client machine through <u>router</u>.</li>

   <li>Your source client program will send the message to the neighbor router (the IP and port number of the router is taken as arguments during startup) using UDP packet. If the packet is sent to a wrong neighbor router, the router will <u>drop the message</u> and send an <u>error message</u> back to client.</li>

   <li>If the message is properly sent to the <em>destination client machine</em>, the neighbor router will send a <u>message</u> along with the IP and Port of the router who has delivered the message back to the source client program. You need to print these messages into the output.</li>

   <li>Similarly, if the message is lost for any reason, an <u>error message</u> is sent back to the client which needs to be printed into the output.</li>

   <li>Finally, the source client program will go back and prompt whether the user wants to send another message.</li>

   <li>Your destination client program takes <strong>three arguments</strong> from user during startup that specifies the port number of the client program, IP address and port number of the <em>neighbor router</em> it will be associated with.</li>

   <li>After startup, destination client program will wait for an incoming UDP packet containing the <em>source client message</em>. Destination client program will <u>accept</u> UDP packet only from the associated route which is given during the startup. If a received packet source is <u>different</u>, then it should drop the packet and send a negative message.</li>

   <li>If packet arrives from a valid source, then it will <em>print the message</em> along with the IP addresses and port numbers of all the routers the packet has passed on the way as a list. After printing the complete trace of route, it should go back and wait for another packet.</li>

  </ul></li>

</ul>




<ul>

 <li><strong>Server Behavior: </strong>

  <ul>

   <li>At startup, the server takes only <strong>one argument</strong> that specifies the port number that it is listening to. You have to use (<em>5000</em>+<em>last 4 digits</em> of your student-id number) to avoid requesting same port by multiple students.</li>

   <li>After successful startup, the server program will wait for a TCP client interaction for <strong>user authentication</strong>. Server has <em>txt</em> file which contains username and password separated by a blank space. If authentication fails, server sends negative feedback and client will provide new pair of data for login.</li>

   <li>If authentication is successful, then server will wait for a destination host name (e.g., gpel8.cs.ou.edu) from client. Server will use this name and search the <em>txt</em> file to retrieve the IP and Port number of the destination client machine. Server will send back a negative message if name doesn’t match else it will send the IP and Port of the destination client machine back to the client program.</li>

   <li>You need to print relevant messages into the output after <em>sending/receiving data</em> so that we can see your processes are working correctly or not.</li>

   <li>After serving one client, the server program should go back and wait for a next client request.</li>

  </ul></li>

</ul>




<ul>

 <li><strong>Router Behavior: </strong>

  <ul>

   <li>At startup, the router program takes <strong>four arguments</strong> that specify the port number that it is listening to, IP address and Port number of the neighbor router it’s associated with (a router has only one neighbor router), and a text file containing neighbor clients list.</li>

   <li>You have to use (6<em>000</em>+<em>last 4 digits</em> of your student-id number) to avoid requesting same port by multiple students. Incrementally use the router <strong>port number +1</strong> for the next router to avoid duplication.</li>

   <li>After startup, router will send a packet to its neighbor router to inform that it is the source router. Next, router will wait for incoming UDP packets (containing a message) to be transmitted from the source client machine to a destination client machine. Router verifies whether the source client is in the neighbor client list text file or not. Only neighbor clients are allowed to use their router.</li>

   <li>If the client has permission (<em>in the neighbor list</em>) to use this router, then router will accept the UDP packet and extract the destination host machine IP and port from the packet. This information will be used to check whether the destination host is in the same neighbor client list of the router. If a match is found, the router will send the packet to the destination host.</li>

   <li>If the destination host is not in the client list, then the packet will be sent to the next neighbor router for delivery. <u>Note:</u> each router has only one neighbor router associated with it. If a packet comes from a different source, the router should drop it and inform that the client/router doesn’t have permission to use this router.</li>

   <li>The packet will propagate through the network until it’s delivered, or it has passed all the routers to avoid looping. After passing all the routes, if the packet can’t be delivered, router which is currently holding the <em>packet will drop</em> it and inform the source client that the <em>destination host doesn’t exists</em>.</li>

   <li>After receiving a message (either from source client or router), your router program should <em>print the message along with message source</em> (IP &amp; Port). Similarly, after routing the message to another router or destination, your router program should <em>print the</em> <em>message delivery information</em> (IP &amp; Port) of the node.</li>

   <li>Your router program should handle all input/output errors. After routing a packet to next router or destination client machine, your router program should go back and wait for another UDP packet to route.</li>

  </ul></li>

</ul>




<ol start="3">

 <li><strong>Programming Notes: </strong></li>

</ol>

<strong> </strong>

The content of the input files You have to use TCP socket for client to server interaction during user authentication and UDP sockets for client to router and router to router communications. You should program each process to print an informative statement whenever it takes an action (e.g., sends or receives a message, detects termination of input, etc.), so that one can see and determine that your processes are working correctly (or not!). You should hand in screen shots of these informative messages.

Make sure, your client, server, and router allow the user to specify the listening port number for communication during startup. You have to close every socket that you use in your program. If you abort your program, the socket may still hang around and the next time you try and bind a new socket to the port ID you previously used (but never closed), you may get an error. Also, please be aware that port ID’s, when bound to sockets, are system-wide values and thus other students may be using the port number you are trying to use though it’s prohibited. . If you need to kill a process after you have started it, you can use the LINUX <em>kill</em> command. Use the LINUX <em>ps</em> command to find the process id of your server.

Any clarifications and revisions to the project will be posted on the course web page on Canvas. Students are encouraged to start this project early and use the project discussion group on Canvas for any general question so that everyone can benefit from the replies.

<strong>File names:</strong>

File names for this project are as follows:

Clients: <em>lastNameSourceClient.c, lastNameDestinationClient.c </em>

Server:<em> lastNameServer.c </em>Router:<em> lastNameRouter.c </em>
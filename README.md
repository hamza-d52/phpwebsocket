# phpwebsocket
Automatically exported from code.google.com/p/phpwebsocket
PHP and WebSockets

Quick hack to implement websockets in php. As of Feb/10 the only browsers that support websockets are Google Chrome and Webkit Nightlies. Get it from here http://www.google.com/chrome

###Browse the source code
,,,js
Changelog
010.02.16 - Added basic demo and chatbot
010.02.16 - Added users list to keep track of handshakes
010.02.16 - Organized everything in a reusable websocket class
010.02.16 - Minor cosmetic changes
,,,
###Client side
,,,js
var host = "ws://localhost:12345/websocket/server.php";
try{
  socket = new WebSocket(host);
  log('WebSocket - status '+socket.readyState);
  socket.onopen    = function(msg){ log("Welcome - status "+this.readyState); };
  socket.onmessage = function(msg){ log("Received: "+msg.data); };
  socket.onclose   = function(msg){ log("Disconnected - status "+this.readyState); };
}
catch(ex){ log(ex); }
,,,
###View source code for the client

###Server side
,,,
log("Handshaking...");
list($resource,$host,$origin) = getheaders($buffer);
$upgrade = "HTTP/1.1 101 Web Socket Protocol Handshake\r\n" .
           "Upgrade: WebSocket\r\n" .
           "Connection: Upgrade\r\n" .
           "WebSocket-Origin: " . $origin . "\r\n" .
           "WebSocket-Location: ws://" . $host . $resource . "\r\n" .
           "\r\n";
$handshake = true;
socket_write($socket,$upgrade.chr(0),strlen($upgrade.chr(0)));
,,,
###View source code for the server

Steps to run the test:
Save both files, client.php and server.php, in a folder in your local server running Apache and PHP.
From the command line, run the server.php program to listen for socket connections.
Open Google Chrome (dev build) and point to the client.php page
Done, your browser now has a full-duplex channel with the server.
Start sending commands to the server to get some responses.

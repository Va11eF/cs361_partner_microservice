# cs361_partner_microservice
To request data from the microservice you will first need to import zmq.
Once imported, you can setup a connecet to the server with the following lines:
    context = zmq.Context()
    socket = context.socket(zmq.REP)
    socket.bind("tcp://*:5555")    

To request from the server, you will need to use the command socket.send() and make sure to have the arguments passed as bytes
For example, to send a string such as "requestJokes" you would request as follows:  socket.send(b"requestJokes")
The prefix of b indicates that it will become a bytes literal.


Whenever a request is sent, you must be prepared for a response. You can set a variable = socket.recv() to handle what was sent from the server.
When the strings of jokes are sent over, they will be sent as byte literals as mentioned previously, but you can easily change it back into a normal sting with the following command : str(socket.recv(), encoding='utf-8')
That way the variable will already be a string

The first request command is requestJokes which should return every joke that the given user has saved. After sending the request, and acknowledgement will be sent back and the server awaits a username.
Once the user has sent their username, you will recieve the number of jokes you have saved. I recommened setting up a for loop after that, since you will be sending a combination of ready requests and recieving 
the strings of the jokes you have saved.


The other request command that the server will recognize is saveJoke which saves a joke that the user liked, which will respond with a general acknowledgement.
Afterwards, you will need to send the joke over, if you are sending it over as a string literal, then it can be done the same way as the previous commands. 
However, if the string is in a variable, then you can simply add .encode('utf-8') to the variable for it to be transferred through the socket. E.G. joke.encode('utf-8')
Once the joke has been sent, the user will recieve a response from the server asking for a username, send your username to the server so that it can be entered into the db alongside the username.
Afterwards you recieve the final response for this sequence indicating that the joke has been saved.


<img width="800" alt="image" src="https://github.com/Va11eF/cs361_partner_microservice/assets/156148160/f974e401-2b43-46bf-9ba4-5ec575de7864">

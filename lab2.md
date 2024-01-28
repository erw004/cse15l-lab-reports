# **Lab Report 2**

## Code:
![Image](ChatServer.png)

## Two Screenshots:
![Image](first_ss.png)
The methods `main()` and `handleRequest()` are called. `main()` takes a `String` array `args` as an argument, which stores the port number. `handleRequest()` takes an argument `url`, which is the page's URL. The `Handler` class has the field variable `page`, which is a `String` stores the messages that will be displayed on the page. From this request, the value of `page` gets changed from an empty string `""` to `"Eric: hi\n"` since we add a new message `Eric: hi` and `page` stores the messages.

![Image](second_ss.png)
The methods `main()` and `handleRequest()` are called. `main()` takes a `String` array `args` as an argument, which stores the port number. `handleRequest()` takes an argument `url`, which is the page's URL. The `Handler` class has the field variable `page`, which is a `String` stores the messages that will be displayed on the page. From this request, the value of `page` gets changed from `"Eric: hi"` to `"Eric: hi\nEric Wang: Hello my friend\n"` since we add a new message `Eric Wang: Hello my friend` and `page` stores the messages.

Prior to Lab 2 and Lab 3, I did not know what `ssh` was at all. Now, I know how to connect to the UCSD CS server with my own laptop as the client. Additionally, I didn't know how to write a web server. Now, I know how to write one and handle incoming requests.

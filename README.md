# RconCpp

I coded this simple Source RCON API for c++. It uses boost asio so you can run it on UNIX and windows systems

# Example
You can create a Rcon object via this example:
```
RconCpp::RconCpp rcon(port, ip);
```
Just pass the port and ip.

To establish the Rcon connection, use the connect() function.
The function throws a std::runtime_error exception if the connection failed.
```
try
{
  rcon.connect();
}
catch (std::runtime_error e)
{
  std::cout << e.what() << std::endl;
  return -1;
}
```

The same goes for the authentication procedure.
The only difference is the variable that you pass to the function. This time it is the Rcon password.
```
try
{
  rcon.authenticate(rcon_pwd);
}
catch (std::runtime_error e)
{
  std::cout << e.what() << std::endl;
  return -1;
}
```

At this point, the connection is established and authenticated. 
You can now use the sendAndRecv() function to send commands and receive the answer. If the answer failed after 5 seconds, the function return a string containing "error".
```
std::string players = rcon.sendAndRecv("listplayers");
std::cout << players << std::endl;
```

# Multiple-packet Responses
Not implemented but if you really have answers bigger than 4096 then you can easily implement it yourself

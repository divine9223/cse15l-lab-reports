# Part 1
StringServer.java
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;
import java.net.URLDecoder;
import java.io.UnsupportedEncodingException;


class Handler implements URLHandler {
    StringBuilder strings = new StringBuilder();
    int count = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String query = url.getQuery();
            if (query != null && query.startsWith("s=")) {
                String encodedMessage = query.substring(2);
                try {
                    String decodedMessage = URLDecoder.decode(encodedMessage, "UTF-8");
                    count++;
                    strings.append(count).append(". ").append(decodedMessage).append("\n");
                    return strings.toString();
                } catch (UnsupportedEncodingException e) {
                    return "Error decoding message!";
                }
            } else {
                return "No message provided!";
            }
        }
        return "";
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
## Screenshots
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/64d6d50f-e567-4701-a9af-8300efdb38df)
### Methods called:
`handleRequest, toString, substring, getQuery, decode, append`
### Relevant arguments for the above methods and values of any relevant fields of the class:
handleRequest: URI url, looks at the url provided; substring: 2, starts to add the query after the 2nd index (skips s= and adds message after the =), decode: encodedMessage, "UTF-8", takes the encoded message and decodes it assuming its encoded in UTF-8; append: count, . , decodedMessage, \n, all are arguments for the method because it needs to create the message line with the count of the line, a period next to the count indicating which line, the message, and to start the message that follows on a new line.
### How the values of relevant fields of the class change from the request:
URI url changes based on what is to be added: http://0-0-0-0-2003-9mt64d73n3g27ubknqquvfvbc.us.edusercontent.com/add-message?s=Hello, substring's argument 2 will not change because it will always take the message after the = sign at index 2, decode's encodedMessage will change based on what the encoded message is: Hello, append's count and decoded message will change because if you call /add-message multiple times the count will continue to go up and the decoded message can change each time it's inputted: 1, Hello
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/9e97c3d3-028d-4eb6-87bf-792d23568c2d)
### Methods called:
Same methods are called from before: handleRequest, toString, substring, getQuery, decode, append
### Relevant arguments for the above methods and values of any relevant fields of the class:
The same arguments are relevant due to the same methods being called. handleRequest: URI url, looks at the url provided; substring: 2, starts to add the query after the 2nd index (skips s= and adds message after the =), decode: encodedMessage, "UTF-8", takes the encoded message and decodes it assuming its encoded in UTF-8; append: count, . , decodedMessage, \n, all are arguments for the method because it needs to create the message line with the count of the line, a period next to the count indicating which line, the message, and to start the message that follows on a new line.
### How the values of relevant fields of the class change from the request:
Same values are being changed. URI url changes based on what is to be added: http://0-0-0-0-2003-9mt64d73n3g27ubknqquvfvbc.us.edusercontent.com/add-message?s=How%20are%20you, substring's argument 2 will not change because it will always take the message after the = sign at index 2, decode's encodedMessage will change based on what the encoded message is: How%20are%20you, append's count and decoded message will change because if you call /add-message multiple times the count will continue to go up and the decoded message can change each time it's inputted: 2, How are you



# Part 2
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/748d61e8-dca2-48ca-8cae-f953b7fb4d95)
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/6799b541-9273-4e13-a4f8-8cd56dd577cd)
# Part 3
Something I learned from this lab is how to code a server and more specifically how to make sure that a space in the URL, which gets turned into %20, would be converted into a space when being shown on the server. I also learned how to add a message so that the server remembers it for the next prompt.

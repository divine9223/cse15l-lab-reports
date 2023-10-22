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
Methods called:
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/9e97c3d3-028d-4eb6-87bf-792d23568c2d)
Methods called:
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.


# Part 2
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/748d61e8-dca2-48ca-8cae-f953b7fb4d95)
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/6799b541-9273-4e13-a4f8-8cd56dd577cd)
# Part 3
Something I learned from this lab is how to code a server and more specifically how to make sure that a space in the URL, which gets turned into %20, would be converted into a space when being shown on the server. I also learned how to add a message so that the server remembers it for the next prompt.

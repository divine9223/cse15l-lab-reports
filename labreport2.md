#Part 1
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
Server.java < taken from the previous lab
```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started!");
    }
}
```
#Part 2
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/748d61e8-dca2-48ca-8cae-f953b7fb4d95)
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/6799b541-9273-4e13-a4f8-8cd56dd577cd)
#Part 3
Something I learned from this lab is how to code a server and more specifically how to make sure that a space in the URL, which gets turned into %20, would be converted into a space when being shown on the server. I also learned how to add a message so that the server remembers it for the next prompt.

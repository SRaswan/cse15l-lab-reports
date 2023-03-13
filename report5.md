# Lab Report 5
by Shaurya Raswan
## Lab Report 2: Creating my own web server
### What I learned:
Learning how to create my own web server was extremely interesting and made a lot of different ideas click into place with me. I never exactly knew how websites function behind the scenes and understanding the basic core of remotely connecting to a server and running the web server with Java was a whole new revelation for me. I was even able to connect to other people's web servers with the right port number and URI. Adding a microservice, backend SQL server, and some CSS/HTML/Java would really allow for a massive website that anyone in the world can access. 
By interacting with their website and incrementing their number, I came to a better understanding of the backend and how data like integers or ArrayLists are stored on the web server. Our programs evolved from just being local files to now something that more people can remotely interact with. SearchEngine.java was my favorite problem to solve in lab Week 2 because I was able to apply my Java skills to a real application by compiling my code and running it on a web server. Other people are able to connect and add or search for their own words. Here is my code for NumberServer.java below:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> words = new ArrayList<String>();
    ArrayList<String> found;

    public String handleRequest(URI url) {
        found = new ArrayList<String>();
        if (url.getPath().equals("/")) {
            return String.format(words.toString());
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    words.add(parameters[1]);
                    return String.format("Added %s", parameters[1]);
                }
            }
            if (url.getPath().contains("/search")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    for (int i = 0; i < words.size(); i++) {
                        if (words.get(i).contains(parameters[1])) {
                            found.add(words.get(i));
                        }
                    }
                    return String.format(found.toString());
                }
            }
            return "404 Not Found!";
        }
    }
}

class NumberServer {
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
Learning how data can seamlessly display on different systems was super engaging, and I hope to learn more about web development in the future.

# Lab Report 5
by Shaurya Raswan
## Lab Report 2: Creating my own web server
## Part 1: What I learned
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

## Part 2: Explanation of NumberServer.java in the format of Lab Report 2
Questions:\
Which methods in your code are called?\
What are the relevant arguments to those methods, and the values of any relevant fields of the class?\
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
1. Screenshot with "Hello?" added\
<img width="641" alt="Screen Shot 2023-01-29 at 11 09 34 PM" src="https://user-images.githubusercontent.com/42948407/215411022-d3df586c-16c7-4a52-8ce8-04ed2d60a782.png">\
The handleRequest method is called with the parameter, URI url. The url variable is "http://ieng6-201.ucsd.edu:4444/add-message?s=Hello?". The parameter passed contains the path "/add-message" and the query with the message we need to add. To see the data that the URI url object has for us, 2 main methods are called. One method is getPath(), which gets the path "/add-message" as a string in this request. Then the next method is getQuery(), which returns the "s=Hello?" string in the url. Queries are determined after the "?" in the url. We use the split() method to split the query with the "=" parameter passed in it. This returns a string array with "s" and "Hello?" (the word we need to append). We use the equals() method to compare if 2 strings are equal, comparing if the url path is only "/" as a parameter (default page url) which it is not. We also use it to see if the first part of the query is "s", which indicates that we need to append the word after the "=" to our StringBuilder (which is now already split and contained in a string array). We use the contains() method to see if getPath() contains the "/add-message" string parameter inside, indicating the program to check for a query. We also use the append() method to append the string "Hello?" and newline "\n" in the parameter to our StringBuilder. We also use String.format() and toString() to format and print the StringBuilder.

2. Screenshot with "Hey" added\
<img width="585" alt="Screen Shot 2023-01-29 at 11 09 48 PM" src="https://user-images.githubusercontent.com/42948407/215411052-ccf33811-d0de-4aec-83f2-b4d50a12ba7e.png">\
The url variable is now "http://ieng6-201.ucsd.edu:4444/add-message?s=Hey". All of the methods from the previous screenshot are used, however, the values of relevant fields were altered. Although the getPath() method still returns a string containing "/add-message", the getQuery() method is different. This is because getQuery() returns "s=Hey", and therefore the parameters string array is split with "s" and "Hey". The first element of parameters is the same. However, the second new element in the array is appended to the StringBuilder, making the values of relevent fields different from the first screenshot and the StringBuilder now includes another word.

3. Screenshot with "Hi" added\
<img width="578" alt="Screen Shot 2023-01-29 at 11 10 00 PM" src="https://user-images.githubusercontent.com/42948407/215411116-b1c7a187-fe74-45eb-9ded-db7449bf5d53.png">\
The url variable is now "http://ieng6-201.ucsd.edu:4444/add-message?s=Hi". Similar to the second screenshot, the path is the same however the query is different. A new, different word is added to the StringBuilder as our query is different. The word "Hi" is added to our StringBuilder.

5. Screenshot on defaul web server URL\
<img width="441" alt="Screen Shot 2023-01-29 at 11 10 13 PM" src="https://user-images.githubusercontent.com/42948407/215411137-45f95c67-cf97-48d2-aa0c-c58d87c90171.png">\
The handleRequest method is called and the parameter, URI url, is the value of "http://ieng6-201.ucsd.edu:4444/", or the default url with no query. Therefore, only the first if statement is run, as getPath(), which is just "/", is different from the first 3 screenshots. StringBuilder is not updated, however, it is still printed using the methods String.format() and toString().

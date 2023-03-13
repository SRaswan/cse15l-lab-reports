# Lab Report 5
by Shaurya Raswan
## Lab Report 2: Creating my own web server
## Part 1: What I learned
Learning how to create my own web server was extremely interesting and made a lot of different ideas click into place with me. I never exactly knew how websites function behind the scenes and understanding the basic core of remotely connecting to a server and running the web server with Java was a whole new revelation for me. I was even able to connect to other people's web servers with the right port number and URI. Adding a microservice, backend SQL server, and some CSS/HTML/Java would really allow for a massive website that anyone in the world can access. 
By interacting with their website and incrementing their number, I came to a better understanding of the backend and how data like integers or ArrayLists are stored on the web server. Our programs evolved from just being local files to now something that more people can remotely interact with. SearchEngine.java was my favorite problem to solve in lab Week 2 because I was able to apply my Java skills to a real application by compiling my code and running it on a web server. Other people are able to connect and add or search for their own words. Here is my code for SearchEngine.java below:
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

class SearchEngine {
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

## Part 2: Explanation of SearchEnginge.java in the format of Lab Report 2
Questions:\
Which methods in your code are called?\
What are the relevant arguments to those methods, and the values of any relevant fields of the class?\
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

1. Inital Screen\
<img width="407" alt="Screen Shot 2023-03-13 at 12 22 03 AM" src="https://user-images.githubusercontent.com/42948407/224634240-01e01f31-46b7-4df5-9dc8-80470bbef766.png">\
The arraylist word is initated and created. Arraylist found is created too.
2. Adding "Hello!!!"\
<img width="401" alt="Screen Shot 2023-03-13 at 12 24 18 AM" src="https://user-images.githubusercontent.com/42948407/224634297-cf51054b-c03d-4583-b502-220ba679a571.png">\
The query of ?add is checked and the split of s= is found, therefore we are able to add Hello!!! to the arraylist words. Arraylist found is refreshed.
3. Entire List so Far\
<img width="414" alt="Screen Shot 2023-03-13 at 12 22 29 AM" src="https://user-images.githubusercontent.com/42948407/224634433-5405fe1e-b34a-4d91-95ef-7f77877f8c83.png">\
Now we can see the entire list so far when we go to the home directory URL.
4. Fast forward after adding multiple words\
<img width="413" alt="Screen Shot 2023-03-13 at 12 23 15 AM" src="https://user-images.githubusercontent.com/42948407/224634345-87be753e-23e4-41cb-8b92-6a8c24ab84c8.png">\
This adds multiple words to showcase the search engine in the next part.
5. Search for "bo"\
<img width="393" alt="Screen Shot 2023-03-13 at 12 24 31 AM" src="https://user-images.githubusercontent.com/42948407/224634493-54c4973e-1169-413e-89e9-adf5b0cdb87e.png">\
The query of ?search is found and the split of s= is found, therefore we can search for "bo" out of all of the words in the arraylist. We do this by seing all of the words that contain the letters "bo". One word of "boat" is found.
6. Search for "a"\
<img width="377" alt="Screen Shot 2023-03-13 at 12 24 38 AM" src="https://user-images.githubusercontent.com/42948407/224634521-9df1110d-547b-414a-b68d-533c1f91f35d.png">\
The query of ?search is found and the split of s= is found, therefore we can search for "a" out of all of the words in the arraylist. We do this by seing all of the words that contain the letter "a". 4 words found with the letter, showing that this program works for multiple matches, too. This works by using a for loop to iterate through every word is ArrayList words, then it uses the .contains() method to check if each word contains "a", then it adds matching words to ArrayList found.
Multiple words come up in this example.
7. Search for "t"\
<img width="386" alt="Screen Shot 2023-03-13 at 12 24 46 AM" src="https://user-images.githubusercontent.com/42948407/224634546-468beba1-1c68-497b-8bcf-55c2d6e681ea.png">\
The query of ?search is found and the split of s= is found, therefore we can search for "t" out of all of the words in the arraylist. We do this by seing all of the words that contain the letter "t". 4 words found with the letter, showing that this program works for multiple matches, too. This works by using a for loop to iterate through every word is ArrayList words, then it uses the .contains() method to check if each word contains "t", then it adds matching words to ArrayList found.
8. Search for "ee"\
<img width="372" alt="Screen Shot 2023-03-13 at 12 24 54 AM" src="https://user-images.githubusercontent.com/42948407/224634558-aff2563f-0e9d-42db-a881-7bd7d799b02d.png">\
The query of ?search is found and the split of s= is found, therefore we can search for "ee" out of all of the words in the arraylist. We do this by seing all of the words that contain the letters "ee". 1 word "tree" was found, showing that this program works with a different search query from last time. This works by using a for loop to iterate through every word is ArrayList words, then it uses the .contains() method to check if each word contains "a", then it adds matching words to ArrayList found. Notice that the words are different from when we checked for "t". This is because the ArrayList found is refreshed every single call to a new URL, so none of the searches we made before will collide with the new searches.

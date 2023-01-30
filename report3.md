# Week 3 Lab Report
by Shaurya Raswan

## Part 1
My StringServer.java is below:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    StringBuilder words = new StringBuilder();


    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(words.toString());
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    words.append(parameters[1]+"\n");
                    return String.format(words.toString());
                }
            }

            return "404 Not Found!";
        }
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
Which methods in your code are called?\
What are the relevant arguments to those methods, and the values of any relevant fields of the class?\
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.\
1. Screenshot with "Hello?" added\
<img width="641" alt="Screen Shot 2023-01-29 at 11 09 34 PM" src="https://user-images.githubusercontent.com/42948407/215411022-d3df586c-16c7-4a52-8ce8-04ed2d60a782.png">\
The handleRequest method is called with the parameter, URI url. The parameter passed contains the path to add-message and the query that has the data of the message we need. To see the data that the URI url object has for us, 2 main methods are called. One method is getPath(), which gets the path "/add-message" as a string in this request. Then the next method is getQuery(), which returns the "s=Hello?" string in the url. Queries are determined after the "?" in the url. We use the split() method to split the query with the "=" parameter passed in it. This returns a string array that lets us contain the word string that is to be added. We use the equals() method to compare if 2 strings are equal, comparing if the url path is only "/" as a parameter (default page url) which it is not. We also use it to see if the first part of the query is "s", which indicates that we need to add the word after the "=" to our StringBuilder. We use the contains() method to see if a string contains another string inside, passing in "/add-message" as a parameter to check if "/add-message" is part of the url to indicate to the program that we need to add a new word. We also use the append() method to append the string (and newline) in the parameter to our StringBuilder. We also use String.format() and toString() to format and print the StringBuilder.

2. Screenshot with "Hey" added\
<img width="585" alt="Screen Shot 2023-01-29 at 11 09 48 PM" src="https://user-images.githubusercontent.com/42948407/215411052-ccf33811-d0de-4aec-83f2-b4d50a12ba7e.png">\
All of the methods from the previous screenshot are used, however, the values of relavant fields were altered. Although the getPath() method still returns a string containing "/add-message", the getQuery() method is different. This is because getQuery() returns "s=Hey", and therefore the parameters string array is split with "s" and "Hey". The first element of parameters is the same. However, the second element in the array is actually appended to the StringBuilder, making the values of relavent fields different from the first screenshot and the StringBuilder now includes another different word.

3. Screenshot with "Hi" added\
<img width="578" alt="Screen Shot 2023-01-29 at 11 10 00 PM" src="https://user-images.githubusercontent.com/42948407/215411116-b1c7a187-fe74-45eb-9ded-db7449bf5d53.png">\
Similar to the second screenshot, the path is the same however the query is different. A new, different word is added to the StringBuilder as our query is different. The word "Hi" is added to our StringBuilder.

5. Screenshot on defaul web server URL\
<img width="441" alt="Screen Shot 2023-01-29 at 11 10 13 PM" src="https://user-images.githubusercontent.com/42948407/215411137-45f95c67-cf97-48d2-aa0c-c58d87c90171.png">\
The handleRequest method is called and the parameter, URI url, is the value of the path "/", or the default url with no query. Therefore, only the first if statement is run, as getPath() is different from the first 3 screenshots. StringBuilder is not updated, however, it is still printed using the methods String.format() and toString().


## Part 2
In ArrayExamples.java, the averageWithoutLowest method has a bug. Here is the code for averageWithoutLowest (not fixed yet):
```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
```
To show where the bug is, I will show:
1. A failure-inducing input for the buggy program, as a JUnit test and any associated code
```
@Test
public void testAverageWithoutLowest1() {
    double[] input1 = { 1, 2, 3, 3, 1, 1};
    assertEquals(2, (int) ArrayExamples.averageWithoutLowest(input1));
}
```
2. An input that doesn’t induce a failure, as a JUnit test and any associated code
```
@Test
public void testAverageWithoutLowest2() {
    double[] input1 = { 1, 2, 3, 3, 5, 7};
    assertEquals(4, (int) ArrayExamples.averageWithoutLowest(input1));
}
```
3. The symptom, as the output of running the tests
<br/>
Here the code did not work for this test, which has multiple duplicate numbers, one group which is the lowest number of 1s:
<img width="1179" alt="Didn't work" src="https://user-images.githubusercontent.com/42948407/215369252-46ced67d-e6b4-4f52-8819-4ec5063d1937.png">
But it worked for this test, which also has duplicate numbers but it is not the lowest:
<img width="533" alt="Worked" src="https://user-images.githubusercontent.com/42948407/215369246-02c46489-c243-471b-a8e8-90ce9035e9aa.png">
5. The bug, as the before-and-after code change required to fix it
<br/>
Above the original code is shown. This is the new code below to fix the bug:

```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
        if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
        sum += num; 
    }
    sum = sum - lowest;
    return sum / (arr.length - 1);
}
```

This fixes the bug because it first adds all numbers in the array, even the lowest one, and then subtracts it at the end once. This ensures that all duplicates of the lowest value arent included in the sum, and only one instance of the lowest value is not included. The JUnit tests work as shown below.\
<img width="511" alt="Fixed" src="https://user-images.githubusercontent.com/42948407/215370623-fdcea930-5f07-4ba4-81af-8b6122e9c049.png">

## Part 3
Learning how to create my own web server was extremely interesting and made a lot of different ideas click into place with me. I never exactly knew how websites function behind the scenes and understanding the basic core of remotely connecting to a server and running the web server with Java was a whole new revelation for me. I was even able to connect to other people's web servers with the right port number and URI, as seen below.\
<img width="414" alt="Connect" src="https://user-images.githubusercontent.com/42948407/215371207-ea68bfce-8c0f-4b9f-a9a5-0a59e391afc5.png">\
By interacting with their website and increment their number, I came to a better understanding of the backend and how data like variables are stored on the web server. SearchEngine.java was my favorite problem to solve in lab Week 2 because I was able to apply my Java skills to a real application by compiling my code and running it on a web server. Other people are able to connect and add or search for their own words. Here is my code below:
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
Lerning how data can seamlessly display on different systems was super engaging, and I hope to learn more about web development in the future.

# Week 3 Lab Report
by Shaurya Raswan

## Part 1
Here is my code for StringServer.java

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

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
Learning how to create my own webserver was extremley intresting and made a lot of different ideas click into place with me. I never exactly knew how websites function behind the scenes, and understanding the basic core of remotely connecting to a server and running the webserver with Java was a whole new revelation for me. I was even able to connect to other people's webservers with the right port number and URI, as seen below.\
<img width="414" alt="Connect" src="https://user-images.githubusercontent.com/42948407/215371207-ea68bfce-8c0f-4b9f-a9a5-0a59e391afc5.png">\
I was even able to interact with their website and increment their number. Understanding the backend, where the variables are stored, and how data is able to seamlessly display on different systems was super engaging, and I hope to learn more about web development in the future.

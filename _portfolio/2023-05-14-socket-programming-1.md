---
caption: #what displays in the portfolio grid:
  title: JAVA 네트워크 소켓 프로그래밍 -1-
  subtitle: 소켓을 통한 아스키 코드 변환값과 수식 계산값 수신하기
  thumbnail: https://velog.velcdn.com/images/dongchyeon/post/e258b9da-59f8-48c9-8841-30de0b21aeea/image.png
  
#what displays when the item is clicked:
title: JAVA 네트워크 소켓 프로그래밍 -1-
subtitle: 소켓을 통한 아스키 코드 변환값과 수식 계산값 수신하기
image: https://velog.velcdn.com/images/dongchyeon/post/e258b9da-59f8-48c9-8841-30de0b21aeea/image.png #main image, can be a link or a file in assets/img/portfolio
---

## 소켓 통신이란?

`소켓`은 TCP/IP 기반 네트워크 통신에서 데이터 송수신의 마지막 end point를 말한다. `소켓 통신`은 이러한 소켓을 통해 서버-클라이언트간 데이터를 주고받는 양방향 연결 지향성 통신이다. 

클라이언트는 소켓을 사용하여 서버에 연결하고 데이터를 전송하며, 서버는 클라이언트의 연결을 수락하고 클라이언트로부터 데이터를 수신한다.

따라서 소켓 통신을 구현하기 위해서는 `서버 소켓`과 `클라이언트 소켓`을 구현해야 한다.

## 서버 소켓 구현하기

```java
// 1. 서버 소켓 생성
ServerSocket serverSocket = new ServerSocket(3000);

// 2. 클라이언트 접속 대기
Socket clientSocket = serverSocket.accept();

// 3. 데이터 수신을 위한 Input Stream 생성 / 데이터 송신을 위한 Output Stream 생성
BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

// 4. Input Stream을 통한 데이터 수신
String receivedMessage = in.readLine();

// 5. Output Stream을 통한 데이터 송신
String sentMessage = "보낼 메시지";
out.println(sentMessage);
out.flush();

// 6. 통신 종료
clientSocket.close();
serverSocket.close();
```

## 클라이언트 소켓 구현하기

```java
// 1. 클라이언트 소켓 생성을 위해 서버 접속
Socket socket = new Socket("localhost", 3000);

// 2. 데이터 송신을 위한 Input Stream 생성 / 데이터 수신을 위한 Output Stream 생성
PrintWriter out = new PrintWriter(new OutputStreamWriter(socket.getOutputStream()));
BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

// 4. Output Stream을 통한 데이터 송신
out.println(message);
out.flush();

// 5. Input Stream을 통한 데이터 수신
String response = in.readLine();
System.out.println("Received message: " + response);

// 6. 통신 종료
socket.close();
```

## 응용 예제

### 1. 보낸 문자열을 아스키 코드로 반환받기

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {
    public static String strToASCII(String str) {
        StringBuilder ascii = new StringBuilder();

        for (int i = 0; i < str.length(); i++) {
            ascii.append((int) str.charAt(i));
        }

        return ascii.toString();
    }

    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(3000);

            Socket clientSocket = serverSocket.accept();
            System.out.println("Client connected: " + clientSocket.getInetAddress().getHostAddress());

            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

            while (true) {
                String message = in.readLine();
                System.out.println("Received message: " + message);

                if (message.equals("close")) break;

                out.println(strToASCII(message));
                out.flush();
            }

            clientSocket.close();
            serverSocket.close();
            System.out.println("Client disconnected.");
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

`서버 측 코드`
 
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.Scanner;

public class Client {
    public static void main(String[] args) {
        try {
            Scanner scanner = new Scanner(System.in);

            Socket socket = new Socket("localhost", 3000);

            PrintWriter out = new PrintWriter(new OutputStreamWriter(socket.getOutputStream()));
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            while (true) {
                String message = scanner.nextLine();

                out.println(message);
                out.flush();
                System.out.println("Sent message: " + message);

                if (message.equals("close")) break;

                String response = in.readLine();
                System.out.println("Received message: " + response);
            }

            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

`클라이언트 측 코드`

```java
public static String strToASCII(String str) {
    StringBuilder ascii = new StringBuilder();

    for (int i = 0; i < str.length(); i++) {
        ascii.append((int) str.charAt(i));
    }

    return ascii.toString();
}

String message = in.readLine();
System.out.println("Received message: " + message);

if (message.equals("close")) break;

out.println(strToASCII(message));
out.flush();
```

서버가 클라이언트로부터 문자열을 받으면 strToASCII 메소드를 통해 아스키 코드로 변환 후 다시 클라이언트로 반환하는 구조이다.

![](https://velog.velcdn.com/images/dongchyeon/post/e258b9da-59f8-48c9-8841-30de0b21aeea/image.png)

실행 결과는 다음과 같다.

### 2. 보낸 수식의 계산값 반환 받기

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

public class Server {

    public static List<String> tokenizeExpression(String expression) {
        List<String> tokens = new ArrayList<>();
        StringBuilder currentNumber = new StringBuilder();

        for (char c : expression.toCharArray()) {
            if (Character.isDigit(c) || c == '.') {
                currentNumber.append(c);
            } else if (isOperator(c)) {
                if (currentNumber.length() > 0) {
                    tokens.add(currentNumber.toString());
                    currentNumber.setLength(0);
                }
                tokens.add(Character.toString(c));
            }
        }

        if (currentNumber.length() > 0) {
            tokens.add(currentNumber.toString());
        }

        return tokens;
    }

    private static boolean isOperator(char c) {
        return c == '+' || c == '-' || c == '*' || c == '/';
    }

    public static int priority(String oper) {
        if (oper.equals("*") || oper.equals("/")) return 2;
        else if (oper.equals("+") || oper.equals("-")) return 1;
        else return 0;
    }

    public static ArrayList<String> infixToPostFix(List<String> infixExp) {
        ArrayList<String> postfixExp = new ArrayList<>();

        Stack<String> operator = new Stack<>();

        for (String elem : infixExp) {
            switch (elem) {
                case "(":
                    operator.push(elem);
                    break;
                case ")":
                    while (true) {
                        String temp = operator.pop();
                        if (temp.equals("(")) break;
                        postfixExp.add(temp);
                    }
                    break;
                case "*":
                case "/":
                case "+":
                case "-":
                    if (!operator.isEmpty() && priority(operator.peek()) >= priority(elem)) {
                        postfixExp.add(operator.pop());
                    }
                    operator.push(elem);
                    break;
                default:
                    postfixExp.add(elem);
                    break;
            }
        }

        while (!operator.isEmpty()) {
            postfixExp.add(operator.pop());
        }

        return postfixExp;
    }

    public static double calculate(List<String> postfixExp) {
        double a, b, result;
        Stack<String> operand = new Stack();

        for (String elem : postfixExp) {
            switch (elem) {
                case "*":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a * b;
                    operand.push(result + "");
                    break;
                case "/":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a / b;
                    operand.push(result + "");
                    break;
                case "+":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a + b;
                    operand.push(result + "");
                    break;
                case "-":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a - b;
                    operand.push(result + "");
                    break;
                default:
                    operand.push(elem);
                    break;
            }
        }

        return Double.parseDouble(operand.pop());
    }

    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(3000);

            Socket clientSocket = serverSocket.accept();
            System.out.println("Client connected: " + clientSocket.getInetAddress().getHostAddress());

            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

            while (true) {
                String message = in.readLine();
                System.out.println("Received message: " + message);

                if (message.equals("close")) break;

                List<String> postfixExp = infixToPostFix(tokenizeExpression(message));

                out.println(calculate(postfixExp));
                out.flush();
            }

            clientSocket.close();
            serverSocket.close();
            System.out.println("Client disconnected.");
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}

```

`서버 측 코드`

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.Scanner;

public class Client {
    public static void main(String[] args) {
        try {
            Scanner scanner = new Scanner(System.in);

            Socket socket = new Socket("localhost", 3000);

            PrintWriter out = new PrintWriter(new OutputStreamWriter(socket.getOutputStream()));
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            while (true) {
                String message = scanner.nextLine();

                out.println(message);
                out.flush();
                System.out.println("Sent message: " + message);

                if (message.equals("close")) break;

                String response = in.readLine();
                System.out.println("Received message: " + response);
            }

            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

`클라이언트 측 코드`

```java
public static List<String> tokenizeExpression(String expression) {
        List<String> tokens = new ArrayList<>();
        StringBuilder currentNumber = new StringBuilder();

        for (char c : expression.toCharArray()) {
            if (Character.isDigit(c) || c == '.') {
                currentNumber.append(c);
            } else if (isOperator(c)) {
                if (currentNumber.length() > 0) {
                    tokens.add(currentNumber.toString());
                    currentNumber.setLength(0);
                }
                tokens.add(Character.toString(c));
            }
        }

        if (currentNumber.length() > 0) {
            tokens.add(currentNumber.toString());
        }

        return tokens;
    }

    private static boolean isOperator(char c) {
        return c == '+' || c == '-' || c == '*' || c == '/';
    }

    public static int priority(String oper) {
        if (oper.equals("*") || oper.equals("/")) return 2;
        else if (oper.equals("+") || oper.equals("-")) return 1;
        else return 0;
    }

    public static ArrayList<String> infixToPostFix(List<String> infixExp) {
        ArrayList<String> postfixExp = new ArrayList<>();

        Stack<String> operator = new Stack<>();

        for (String elem : infixExp) {
            switch (elem) {
                case "(":
                    operator.push(elem);
                    break;
                case ")":
                    while (true) {
                        String temp = operator.pop();
                        if (temp.equals("(")) break;
                        postfixExp.add(temp);
                    }
                    break;
                case "*":
                case "/":
                case "+":
                case "-":
                    if (!operator.isEmpty() && priority(operator.peek()) >= priority(elem)) {
                        postfixExp.add(operator.pop());
                    }
                    operator.push(elem);
                    break;
                default:
                    postfixExp.add(elem);
                    break;
            }
        }

        while (!operator.isEmpty()) {
            postfixExp.add(operator.pop());
        }

        return postfixExp;
    }

    public static double calculate(List<String> postfixExp) {
        double a, b, result;
        Stack<String> operand = new Stack();

        for (String elem : postfixExp) {
            switch (elem) {
                case "*":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a * b;
                    operand.push(result + "");
                    break;
                case "/":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a / b;
                    operand.push(result + "");
                    break;
                case "+":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a + b;
                    operand.push(result + "");
                    break;
                case "-":
                    a = Double.parseDouble(operand.pop());
                    b = Double.parseDouble(operand.pop());
                    result = a - b;
                    operand.push(result + "");
                    break;
                default:
                    operand.push(elem);
                    break;
            }
        }

        return Double.parseDouble(operand.pop());
    }
```

수식을 계산하는 것은 다음 절차를 따른다.

* 입력받은 수식을 연산자와 숫자마다 나누어 리스트에 담는다.
* 리스트를 토대로 후위 표기식을 만든다.
* 후위 표기식을 다음 절차에 따라 계산한다.
  1. 피연산자가 들어오면 스택에 담는다.
  2. 연산자를 만나면 스택에서 두 개의 연산자를 꺼내서 연산한 뒤에 그 결과를 스택에 담는다.
  3. 연산을 마친 뒤에 스택에 남아있는 하나의 피연산자가 연산 수행 결과이다.

해당 연산 결과를 다시 클라이언트 측에 송신하면 된다,

![](https://velog.velcdn.com/images/dongchyeon/post/651b0696-cddc-4bd2-9f7f-4c91ce25d5f5/image.png)

실행 결과는 다음과 같다.
---
caption: #what displays in the portfolio grid:
  title: JAVA 네트워크 소켓 프로그래밍 -2-
  subtitle: 소켓을 통한 DNS 서버 흉내내기
  thumbnail: https://velog.velcdn.com/images/dongchyeon/post/0449c815-3ab8-40bb-a636-2bf5a77f5a8c/image.png
  
#what displays when the item is clicked:
title: JAVA 네트워크 소켓 프로그래밍 -2-
subtitle: 소켓을 통한 DNS 서버 흉내내기
image: https://velog.velcdn.com/images/dongchyeon/post/0449c815-3ab8-40bb-a636-2bf5a77f5a8c/image.png #main image, can be a link or a file in assets/img/portfolio
---

우선 소켓 통신에 대한 대략적인 내용은 이전 포스트를 참고하자.

구현 요구 사항은 다음과 같다.

1. 기본적인 정보로 도메인 주소와 아이피 주소를 가지고 있다.
2. 도메인 네임을 보내면 IP 주소를 준다.
3. IP 주소를 보내면 도메인 네임을 준다.
4. w: 도메인 네임, IP 주소를 하면 테이블에 해당 아이템을 추가한다.


## 1. 데이터베이스 설계

DNS 아이템을 담기 위해서 h2 데이터베이스를 연동하였다.

![](https://velog.velcdn.com/images/dongchyeon/post/5ccca148-60e7-46f8-8915-70b945aa5899/image.png)

테이블의 구조는 다음과 같다.

## 2. jdbc로 데이터베이스 연동하기

### 2-1. JDBCUtil 클래스 작성

데이터베이스의 연결과 연결 종료를 쉽게 하기 위해 JDBCUtil 클래스를 작성했다.

```java
import java.sql.*;

public class JDBCUtil {

    public static Connection getConnection() {
        Connection conn = null;

        try {
            DriverManager.registerDriver(new org.h2.Driver());
            conn = DriverManager.getConnection("jdbc:h2:tcp://localhost/~/test", "sa", "");
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }

        return conn;
    }

    public static void close(PreparedStatement pstmt, Connection conn) {
        try {
            pstmt.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }

        try {
            conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public static void close(Connection conn, PreparedStatement pstmt, ResultSet rs) {
        try {
            rs.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }

        try {
            pstmt.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }

        try {
            conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

}
```

### 2-2. Repository 작성

실질적인 SQL 쿼리의 실행이 이루어지는 Repository 클래스를 작성했다.

필요한 쿼리는 DNS 아이템 삽입, IP 주소로 도메인 네임 조회, 도메인 네임으로 IP 주소 조회가 있다.

```java
public Dns save(Dns dns) {
        findByDomainName(dns.getDomainName()).ifPresent(d -> {
            throw new RuntimeException("Domain name already exists");
        });

        String sql = "INSERT INTO DNS(domainname, ipaddress) values(?, ?)";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);
            pstmt.setString(1, dns.getDomainName());
            pstmt.setString(2, dns.getIpAddress());
            pstmt.executeUpdate();
            rs = pstmt.getGeneratedKeys();
            if (rs.next()) {
                dns.setId(rs.getLong(1));
            } else {
                throw new SQLException("No item found.");
            }
            return dns;
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
```

`DNS 아이템 삽입`

```java
public Optional<Dns> findByIpAddress(String ipAddress) {
        String sql = "SELECT * FROM DNS WHERE IPADDRESS = ?";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1, ipAddress);
            rs = pstmt.executeQuery();
            if(rs.next()) {
                Dns dns = new Dns();
                dns.setId(rs.getLong("id"));
                dns.setDomainName(rs.getString("domainname"));
                dns.setIpAddress(rs.getString("ipaddress"));
                return Optional.of(dns);
            } else {
                return Optional.empty();
            }
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
```

`IP 주소로 도메인 네임 조회`

```java
public Optional<Dns> findByDomainName(String domainName) {
        String sql = "SELECT * FROM DNS WHERE DOMAINNAME = ?";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1, domainName);
            rs = pstmt.executeQuery();
            if(rs.next()) {
                Dns dns = new Dns();
                dns.setId(rs.getLong("id"));
                dns.setDomainName(rs.getString("domainname"));
                dns.setIpAddress(rs.getString("ipaddress"));
                return Optional.of(dns);
            } else {
                return Optional.empty();
            }
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
```

`도메인 네임으로 IP 주소 조회`

<hr>


```java
import java.sql.*;
import java.util.Optional;

import static org.example.socket.dns.JDBCUtil.close;
import static org.example.socket.dns.JDBCUtil.getConnection;

public class DnsRepository {
    public Dns save(Dns dns) {
        findByDomainName(dns.getDomainName()).ifPresent(d -> {
            throw new RuntimeException("Domain name already exists");
        });

        String sql = "INSERT INTO DNS(domainname, ipaddress) values(?, ?)";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);
            pstmt.setString(1, dns.getDomainName());
            pstmt.setString(2, dns.getIpAddress());
            pstmt.executeUpdate();
            rs = pstmt.getGeneratedKeys();
            if (rs.next()) {
                dns.setId(rs.getLong(1));
            } else {
                throw new SQLException("No item found.");
            }
            return dns;
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }

    public Optional<Dns> findByIpAddress(String ipAddress) {
        String sql = "SELECT * FROM DNS WHERE IPADDRESS = ?";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1, ipAddress);
            rs = pstmt.executeQuery();
            if(rs.next()) {
                Dns dns = new Dns();
                dns.setId(rs.getLong("id"));
                dns.setDomainName(rs.getString("domainname"));
                dns.setIpAddress(rs.getString("ipaddress"));
                return Optional.of(dns);
            } else {
                return Optional.empty();
            }
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }

    public Optional<Dns> findByDomainName(String domainName) {
        String sql = "SELECT * FROM DNS WHERE DOMAINNAME = ?";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1, domainName);
            rs = pstmt.executeQuery();
            if(rs.next()) {
                Dns dns = new Dns();
                dns.setId(rs.getLong("id"));
                dns.setDomainName(rs.getString("domainname"));
                dns.setIpAddress(rs.getString("ipaddress"));
                return Optional.of(dns);
            } else {
                return Optional.empty();
            }
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
}
```

전체 클래스 내용은 다음과 같다.

## 3. 서버 클래스에 Repository 연동

클라이언트에 날라오는 메시지는 3가지로 나뉜다.

* `DNS 아이템 삽입` : w: 로 시작하는지 걸러야 한다.
* `IP 주소를 통한 도메인 네임 조회` : 숫자와 .으로 시작하는지 걸러야 한다.
* `도메인 네임을 통한 IP 주소 조회` : 위의 두 경우가 아닐 경우 도메인 네임이 날라온 걸로 가정한다.

```java
// DNS 아이템 삽입
if (message.startsWith("w: ")) {
    String[] commands = message.split(" ");
    String domainName = commands[1];
    String ipAddress = commands[2];

    if (repository.findByDomainName(commands[1]).isEmpty()) {
        Dns dns = new Dns();
        dns.setDomainName(domainName);
        dns.setIpAddress(ipAddress);
        repository.save(dns);
        out.println("DNS insertion completed: " + dns);
    } else {
        out.println("Domain name already exists.");
    }
// IP 주소로 검색
} else if (Pattern.matches("^[0-9.]+$", message)) {
    Optional<Dns> dns = repository.findByIpAddress(message);
    dns.ifPresent(value -> out.println("Domain Name: " + value.getDomainName()));
    if (dns.isEmpty()) out.println("No item found.");
// 도메인 네임으로 검색
} else {
    Optional<Dns> dns = repository.findByDomainName(message);
    dns.ifPresent(value -> out.println("IP Address: " + value.getIpAddress()));
    if (dns.isEmpty()) out.println("No item found.");
}
```

코드로 구현하면 다음과 같다.

<hr>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Optional;
import java.util.regex.Pattern;

public class Server {

    public static final DnsRepository repository = new DnsRepository();

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

                // DNS 아이템 삽입
                if (message.startsWith("w: ")) {
                    String[] commands = message.split(" ");
                    String domainName = commands[1];
                    String ipAddress = commands[2];

                    if (repository.findByDomainName(commands[1]).isEmpty()) {
                        Dns dns = new Dns();
                        dns.setDomainName(domainName);
                        dns.setIpAddress(ipAddress);
                        repository.save(dns);
                        out.println("DNS insertion completed: " + dns);
                    } else {
                        out.println("Domain name already exists.");
                    }
                // IP 주소로 검색
                } else if (Pattern.matches("^[0-9.]+$", message)) {
                    Optional<Dns> dns = repository.findByIpAddress(message);
                    dns.ifPresent(value -> out.println("Domain Name: " + value.getDomainName()));
                    if (dns.isEmpty()) out.println("No item found.");
                // 도메인 네임으로 검색
                } else {
                    Optional<Dns> dns = repository.findByDomainName(message);
                    dns.ifPresent(value -> out.println("IP Address: " + value.getIpAddress()));
                    if (dns.isEmpty()) out.println("No item found.");
                }
            }

            clientSocket.close();
            System.out.println("Client disconnected.");
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

전체 클래스 내용은 다음과 같다.

Client에 대한 내용은 이전 포스트의 내용과 같으므로 생략하겠다.

## + 방화벽 설정하기

같은 컴퓨터에서 서버와 클라이언트를 둘 다 실행했을 때와는 달리, 각각 다른 컴퓨터에서 실행하면 `java.net.socketexception connection timed out` 에러가 날 수도 있다.

이때, 방화벽을 통해 소켓 통신을 하는 포트에 대한 접근을 허용해야 한다.

![](https://velog.velcdn.com/images/dongchyeon/post/1262bfdb-903f-4fca-b989-e73676cbce40/image.png)

방화벽의 고급 설정에 들어가 인바운드 규칙과 아웃바운드 규칙에 소켓을 연 포트에 대한 접근을 허용시키면 된다.
해당 코드에서는 3000 포트를 사용하고 있으므로 3000 포트에 대한 접근을 허용했다.

<img src = "https://velog.velcdn.com/images/dongchyeon/post/0449c815-3ab8-40bb-a636-2bf5a77f5a8c/image.png" width="100%">

서로 다른 컴퓨터에서도 무사히 돌아가는 것을 확인할 수 있다.

## 실행 결과

<img src = "https://velog.velcdn.com/images/dongchyeon/post/3f576129-0283-4072-9edc-f8c9e68710bf/image.png" width="100%">

`w: 도메인 네임 IP 주소`를 통한 DNS 아이템 삽입, 도메인 네임을 통한 IP 주소 조회, IP 주소를 통한 도메인 네임 조회 모두 정상적으로 이루어지는 것을 확인할 수 있다.
# :book: 디자인 패턴

## :pushpin: Facade pattern

### :seedling: facade pattern
- Facade는 건물의 앞쪽 정면이라는 뜻을 가진다. 여러 개의 객체와 실제 사용하는 서브 객체의 사이에 복잡한 의존관계가 있을 때,
중간에 facade 라는 객체를 두고, 여기서 제공하는 interface만을 활용하여 기능을 사용하는 방식이다.
- facade는 자신이 가지고 있는 각 클래스의 기능을 명확히 알아야 한다.

![](./images/facade.png)

### :seedling: Facade 패턴 적용 이전

#### Ftp Class
```java
public class Ftp {

    private String host;
    private int port;
    private String path;

    public Ftp(String host, int port, String path) {
        this.host = host;
        this.port = port;
        this.path = path;
    }

    public void connect() {
        System.out.println("FTP Host : "+host+" Port : " +port+" 로 연결 합니다.");

    }

    public void moveDirectory() {
        System.out.println("FTP path : "+path+" 로 이동 합니다.");
    }

    public void disconnect() {
        System.out.println("FTP 연결을 종료 합니다.");
    }
}
```

#### Reader Class
````java
public class Reader {

    private String fileName;

    public Reader(String fileName) {
        this.fileName = fileName;
    }

    public void fileConnect() {
        String msg = String.format("Reader %s 로 연결 합니다.", fileName);
        System.out.println(msg);
    }

    public void fileRead() {
        String msg = String.format("Reader %s 의 내용을 읽어 옵니다.", fileName);
        System.out.println(msg);
    }

    public void fileDisconnect(){
        String msg = String.format("Reader %s 로 연결 종료 합니다.", fileName);
        System.out.println(msg);
    }

}
````

#### Writer Class
````java
public class Writer {

    private String fileName;

    public Writer(String fileName) {
        this.fileName = fileName;
    }

    public void fileConnect() {
        String msg = String.format("Writer %s 로 연결 합니다.", fileName);
        System.out.println(msg);
    }

    public void fileDisconnect() {
        String msg = String.format("Writer %s 로 연결 종료 합니다.", fileName);
        System.out.println(msg);
    }

    public void write() {
        String msg = String.format("Writer %s 로 파일쓰기를 합니다.", fileName);
        System.out.println(msg);
    }
}
````

#### Main Class
```java
public class Main {

    public static void main(String[] args) {
        Ftp ftpClient = new Ftp("www.foo.co.kr", 22, "/home/etc");
        ftpClient.connect();
        ftpClient.moveDirectory();

        Writer writer = new Writer("text.tmp");
        writer.fileConnect();
        writer.write();

        Reader reader = new Reader("text.tmp");
        reader.fileConnect();
        reader.fileRead();

        reader.fileDisconnect();
        writer.fileDisconnect();
        ftpClient.disconnect();
    }
}
```

### :seedling: Facade 패턴 적용한 후

#### SftpClient Class
```java
public class SftpClient {

    private Ftp ftp;
    private Reader reader;
    private Writer writer;

    public SftpClient(Ftp ftp, Reader reader, Writer writer) {
        this.ftp = ftp;
        this.reader = reader;
        this.writer = writer;
    }

    public SftpClient(String host, int port, String path, String fileName) {
        this.ftp = new Ftp(host, port, path);
        this.reader = new Reader(fileName);
        this.writer = new Writer(fileName);
    }
    
    public void connect() {
        ftp.connect();
        ftp.moveDirectory();
        writer.fileConnect();
        reader.fileConnect();
    }
    
    public void disConnect() {
        writer.fileDisconnect();
        reader.fileDisconnect();
        ftp.disconnect();
    }
    
    public void read() {
        reader.fileRead();
    }
    
    public void write() {
        writer.write();
    }
}
```

#### Main Class
````java
public class Main {

    public static void main(String[] args) {
        SftpClient sftpClient = new SftpClient("www.foo.co.kr", 22, "/home/ect", "text.tmp");
        sftpClient.connect();
        sftpClient.write();
        sftpClient.read();
        sftpClient.disConnect();
    }
}
````
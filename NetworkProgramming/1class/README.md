# 바이트스트림
## 스트림이란?
* 입출력
  * 프로그램이 외부 매체와 자료를 주고 받는 것
* 스트림이란 입출력 메소드를 체계적으로 모아 놓은 클래스
  * 입력 스트림은 데이터를 읽는 read 메소드 중심
  * 출력 스트림은 데이터를 기록하는 write 메소드 중심
* 스트림 클래스가 들어 있는 패키지 이름은 java.io 이고 거의 모든 입출력 스트림의 메소드는 IOException을 발생시킨다.

## 바이트 스트림
자바 바이트 스트림의 메소드는 8비트의 정수를 읽거나 기록한다.
* 따라서 한번에 0~255 범위의 값을 가진 데이터를 취급한다.

## OutputStream
자바에서 제공하는 출력용 바이트 스트림의 기본 클래스
* void write(int b)
  * 매개변수는 int형이지만 실제로는 8개 비트(부호 없는 바이트)를 인자로 받아 출력한다.
    * 따라서 하위 1바이트만 인식하고 상위 3바이트는 무시하며 0~255 범위의 정수를 출력하게 된다.
    * 즉 데이터가 b가라면 b%256 또는 b&0xff가 출력된다.
## FileOutputStream
실제로 데이터를 출력할 때는 OutputStream 같은 추상클래스가 아닌 구체적인 스트림을 사용해야 한다. FileOutputStream을 파일에 출력할 때 사용한다.
```import java.io.*;
public class Example_01 {
	public static void main(String[] arguments) throws Exception{
		FileOutputStream fos = new FileOutputStream("file01.dat");
		for (int i = 65; i < 65+26; i++) 
			fos.write(i);
		fos.close();
	}
}
```
출력결과
* ABCDEFGHUJKLMNOPQRSTUVWXYZ

바이트 배열을 출력하는 메소드
* void write(byte[] b)
* void write(byte[] b, int s, int b)
  * s: 시작 인덱스
  * n: 출력을 원하는 바이트 수
1회의 write 메소드 호출로 여러 바이트의 데이터를 한꺼번에 출력할 수 있다.  

write(byte[]) 예
``` import java.io.*;
public class Example_06 {
	public static void main(String[] args) throws Exception{
		byte[] b = new byte[26];
		// 다음 라인은 배열을 65, 66, …, 91로 채운다
		for (int i = 0; i < 26; i++) b[i] = (byte)(i+65);
		// 파일에 배열을 출력한다
		FileOutputStream fos = new FileOutputStream("file03.dat");
		fos.write(b); // write 메소드 한 번 호출
		fos.close();
	}
}
```
출력결과
* ABCDEFGHUJKLMNOPQRSTUVWXYZ

파일 스트림과 파일과의 관계
* 파일 스트림 객체를 생성할 때 파일이 오픈된다.
* 출력의 경우 이미 있던 내용은 전부 지워지고 새로이 생성 된다.
* 오픈후 write() 메소드를 호출하지 않으면 내용이 없이 빈파일이 생성된다.
* 오픈후 read() 메소드를 호출하면 맨 앞 바이트부터 읽음
* 프로그램이 종료되면 파일은 저절로 닫힘

## InputStream
1바이트 자료 입력을 위한 기본 추상 클래스
* int read() 메소드는 1바이트의 자료를 읽는다. 따라서 반환하는 결과는 0~255 범위의 수이다.
* 반환값이 -1이면 파일 내의 모든 데이터가 다 읽혀져서 스트림의 끝(End-Of-Stream)에 도달했다는 표시이다.

## FileInputStream
실제로 데이터를 출력할 때는 InputStream 같은 추상클래스가 아닌 구체적인 스트림을 사용해야 한다. FileInputStream을 파일로부터 읽어 들일때 사용한다.
```import java.io.*;
class Example_08 {
	public static void main(String[] args) throws IOException {
		FileInputStream fis = new FileInputStream ("my.dat");
		int total = 0;
		int j = fis.read();
		while (j != -1) {
			total++;
			j = fis.read();
		}
		System.out.println(total + " bytes");
	}
}
```
* read()문의 배치(1)
  * 일반적인 방법
```FileInputStream fis = new FileInputStream("myFile.txt");
int k;
while((k = fis.read()) != -1) {
		System.out.print(k);
}
```
  * 무한 루프 속에 포함시키는 방법
```FileInputStream fis = new FileInputStream("myFile.txt");
while (true) {
		int k = fis.read();
		if (k == -1) break;
		System.out.print(k);
}
```
  * read()문을 2개 사용
```FileInputStream fis = new FileInputStream("myFile.txt");
int k= fis.read();
while(k != -1){
		System.out.print(k);
		k= fis.read();
}
```

바이트 배열에 읽어 들이기
* 하나의 read()문으로 여러 바이트 읽기
  * int read(byte[] buf) // 바이트 배열 채우기
  * int read(byte[] buf, int s, int n) // 바이트 배열 일부분 채우기
* 반환값은 읽은 바이트 수이다. 

바이트 배열에 읽어 들일 때 주의(1)
* int read()는 읽을 데이터가 없으면 기다린다.
  * 블록(block)된다. 즉 Synchronous 방식으로 동작한다.
* int read(byte[])는 블록이 되지 않는다(즉 기다리지 않는다.)

바이트 배열에 읽어 들일 때 주의(2)
* read(byte[]), read(byte[], int, int)는 0 ~ 255 범위의 데이터를 읽어 들이므로 -128 ~ 127 범위인 byte형 배열에 저장되는 과정에서 형변환되어 음수로 변할 수 있다.
* 따라서 읽어들인 원래의 수를 알기 위해서는 부호 있는 byte를 부호 없는 byte로 변환해야함 
  * int original = input[k] >= 0? input[k] : 256+input [k]; 
  * int original = input [k] & 0xff;

available()
* 이 메소드를 통해 현재 얼마만큼의 바이트를 읽어 들일 수 있는가 알 수 있다.

skip()
* 데이터를 읽지 않고 그냥 지나치고 싶을 때 사용

Marking과 Restting
* mark()로 현재의 위치를 표시해 놓고 후에 reset()을 이용하여 표시된 위치로 되돌아 와서 이미 읽은 스트림을 다시 읽음
* 모든 스트림이 Mark and Reset을 허용하는 것은 아니므로 markSupported()로 확인을 해 본 후에 사용하는 것이 좋다
* Mark & Reset을 지원하는 대표적인 입력 스트림
  * BufferedInputStream
  * ByteArrayInputStream
```import java.io.*;
class Example_17 {
public static void main(String[] args) throws IOException {
FileInputStream fis = new FileInputStream ("char");
BufferedInputStream bis = new BufferedInputStream (fis);

int j;
for(int i = 0; i < 3; i++){
j = bis.read();
System.out.println(j);
}
System.out.println("Mark here!");
bis.mark(3);

for(int i = 0; i < 5; i++){
j = bis.read();
System.out.println(j);
}
System.out.println("Reset");
bis.reset();

for(int i = 0; i < 10; i++){
j = bis.read();
System.out.println(j);
}
        }
}
```
## 스트림과 다형성
* OutputStream
  * 자료를 어느 곳에 출력할 것인가??
  * FileOutputSteam
  * ByteArrayOutputStream
  * TelnetOutputStream
* InputStream
  * 자료를 어느곳에 입력할 것인가?
  * FileInputSteam
  * ByteArrayInputStream
  * TelnetInputStream

다형성을 활용한 예제
```import java.io.*;
public class Example_18 { 
	public static void main(String[] args) {
		try {
			InputStream is = new FileInputStream("javalogo.gif");
			int input;
			int count = 0;
			input = is.read();
			while (input != -1) {
				System.out.print(input + " ");
				if(count%8==7) System.out.print('\n');
				else System.out.print('\t');
				count++;
				input = is.read();
			}
			is.close();
			System.out.println("\nBytes read: " + count);
		}catch (IOException e) {
			System.out.println("Error -- " + e.toString());
		}
	}
}
```





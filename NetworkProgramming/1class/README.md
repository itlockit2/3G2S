# ����Ʈ��Ʈ��
## ��Ʈ���̶�?
* �����
  * ���α׷��� �ܺ� ��ü�� �ڷḦ �ְ� �޴� ��
* ��Ʈ���̶� ����� �޼ҵ带 ü�������� ��� ���� Ŭ����
  * �Է� ��Ʈ���� �����͸� �д� read �޼ҵ� �߽�
  * ��� ��Ʈ���� �����͸� ����ϴ� write �޼ҵ� �߽�
* ��Ʈ�� Ŭ������ ��� �ִ� ��Ű�� �̸��� java.io �̰� ���� ��� ����� ��Ʈ���� �޼ҵ�� IOException�� �߻���Ų��.

## ����Ʈ ��Ʈ��
�ڹ� ����Ʈ ��Ʈ���� �޼ҵ�� 8��Ʈ�� ������ �аų� ����Ѵ�.
* ���� �ѹ��� 0~255 ������ ���� ���� �����͸� ����Ѵ�.

## OutputStream
�ڹٿ��� �����ϴ� ��¿� ����Ʈ ��Ʈ���� �⺻ Ŭ����
* void write(int b)
  * �Ű������� int�������� �����δ� 8�� ��Ʈ(��ȣ ���� ����Ʈ)�� ���ڷ� �޾� ����Ѵ�.
    * ���� ���� 1����Ʈ�� �ν��ϰ� ���� 3����Ʈ�� �����ϸ� 0~255 ������ ������ ����ϰ� �ȴ�.
    * �� �����Ͱ� b����� b%256 �Ǵ� b&0xff�� ��µȴ�.
## FileOutputStream
������ �����͸� ����� ���� OutputStream ���� �߻�Ŭ������ �ƴ� ��ü���� ��Ʈ���� ����ؾ� �Ѵ�. FileOutputStream�� ���Ͽ� ����� �� ����Ѵ�.
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
��°��
* ABCDEFGHUJKLMNOPQRSTUVWXYZ

����Ʈ �迭�� ����ϴ� �޼ҵ�
* void write(byte[] b)
* void write(byte[] b, int s, int b)
  * s: ���� �ε���
  * n: ����� ���ϴ� ����Ʈ ��
1ȸ�� write �޼ҵ� ȣ��� ���� ����Ʈ�� �����͸� �Ѳ����� ����� �� �ִ�.  

write(byte[]) ��
``` import java.io.*;
public class Example_06 {
	public static void main(String[] args) throws Exception{
		byte[] b = new byte[26];
		// ���� ������ �迭�� 65, 66, ��, 91�� ä���
		for (int i = 0; i < 26; i++) b[i] = (byte)(i+65);
		// ���Ͽ� �迭�� ����Ѵ�
		FileOutputStream fos = new FileOutputStream("file03.dat");
		fos.write(b); // write �޼ҵ� �� �� ȣ��
		fos.close();
	}
}
```
��°��
* ABCDEFGHUJKLMNOPQRSTUVWXYZ

���� ��Ʈ���� ���ϰ��� ����
* ���� ��Ʈ�� ��ü�� ������ �� ������ ���µȴ�.
* ����� ��� �̹� �ִ� ������ ���� �������� ������ ���� �ȴ�.
* ������ write() �޼ҵ带 ȣ������ ������ ������ ���� �������� �����ȴ�.
* ������ read() �޼ҵ带 ȣ���ϸ� �� �� ����Ʈ���� ����
* ���α׷��� ����Ǹ� ������ ������ ����

## InputStream
1����Ʈ �ڷ� �Է��� ���� �⺻ �߻� Ŭ����
* int read() �޼ҵ�� 1����Ʈ�� �ڷḦ �д´�. ���� ��ȯ�ϴ� ����� 0~255 ������ ���̴�.
* ��ȯ���� -1�̸� ���� ���� ��� �����Ͱ� �� �������� ��Ʈ���� ��(End-Of-Stream)�� �����ߴٴ� ǥ���̴�.

## FileInputStream
������ �����͸� ����� ���� InputStream ���� �߻�Ŭ������ �ƴ� ��ü���� ��Ʈ���� ����ؾ� �Ѵ�. FileInputStream�� ���Ϸκ��� �о� ���϶� ����Ѵ�.
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
* read()���� ��ġ(1)
  * �Ϲ����� ���
```FileInputStream fis = new FileInputStream("myFile.txt");
int k;
while((k = fis.read()) != -1) {
		System.out.print(k);
}
```
  * ���� ���� �ӿ� ���Խ�Ű�� ���
```FileInputStream fis = new FileInputStream("myFile.txt");
while (true) {
		int k = fis.read();
		if (k == -1) break;
		System.out.print(k);
}
```
  * read()���� 2�� ���
```FileInputStream fis = new FileInputStream("myFile.txt");
int k= fis.read();
while(k != -1){
		System.out.print(k);
		k= fis.read();
}
```

����Ʈ �迭�� �о� ���̱�
* �ϳ��� read()������ ���� ����Ʈ �б�
  * int read(byte[] buf) // ����Ʈ �迭 ä���
  * int read(byte[] buf, int s, int n) // ����Ʈ �迭 �Ϻκ� ä���
* ��ȯ���� ���� ����Ʈ ���̴�. 

����Ʈ �迭�� �о� ���� �� ����(1)
* int read()�� ���� �����Ͱ� ������ ��ٸ���.
  * ���(block)�ȴ�. �� Synchronous ������� �����Ѵ�.
* int read(byte[])�� ����� ���� �ʴ´�(�� ��ٸ��� �ʴ´�.)

����Ʈ �迭�� �о� ���� �� ����(2)
* read(byte[]), read(byte[], int, int)�� 0 ~ 255 ������ �����͸� �о� ���̹Ƿ� -128 ~ 127 ������ byte�� �迭�� ����Ǵ� �������� ����ȯ�Ǿ� ������ ���� �� �ִ�.
* ���� �о���� ������ ���� �˱� ���ؼ��� ��ȣ �ִ� byte�� ��ȣ ���� byte�� ��ȯ�ؾ��� 
  * int original = input[k] >= 0? input[k] : 256+input [k]; 
  * int original = input [k] & 0xff;

available()
* �� �޼ҵ带 ���� ���� �󸶸�ŭ�� ����Ʈ�� �о� ���� �� �ִ°� �� �� �ִ�.

skip()
* �����͸� ���� �ʰ� �׳� ����ġ�� ���� �� ���

Marking�� Restting
* mark()�� ������ ��ġ�� ǥ���� ���� �Ŀ� reset()�� �̿��Ͽ� ǥ�õ� ��ġ�� �ǵ��� �ͼ� �̹� ���� ��Ʈ���� �ٽ� ����
* ��� ��Ʈ���� Mark and Reset�� ����ϴ� ���� �ƴϹǷ� markSupported()�� Ȯ���� �� �� �Ŀ� ����ϴ� ���� ����
* Mark & Reset�� �����ϴ� ��ǥ���� �Է� ��Ʈ��
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
## ��Ʈ���� ������
* OutputStream
  * �ڷḦ ��� ���� ����� ���ΰ�??
  * FileOutputSteam
  * ByteArrayOutputStream
  * TelnetOutputStream
* InputStream
  * �ڷḦ ������� �Է��� ���ΰ�?
  * FileInputSteam
  * ByteArrayInputStream
  * TelnetInputStream

�������� Ȱ���� ����
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





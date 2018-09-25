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

### 인접 레이어 상호작용(Adjacent-Layer Interaction)
* OSI 모델에서는 데이터가 맨 위의 계층 응용 프로그램 계층(Application Layer)에서 만들어지고 밑의 레이어로 전송한다.  
![](1.jpg)  
* 이때 일어나는 레이어들 끼리의 상호작용을 인접 레이어 상호작용(Adjacent-Layer Interaction)이라고 한다.  
![](3.jpg)  
* 각 레이어에서는 데이터를 전송할때 각 레이어에 맞는 Header를 데이터앞에 붙이는데 이 헤더에는 각 레이어별 기능을 수행하기 위한 정보(Control Information)가 들어있다.  
이러한 과정을 캡슐화(Capsulation)이라고 한다.  
![](4.jpg)  
* 이렇게 헤더와 데이터를 통틀어서 Protocol Data Unit(PDU)라고 한다.  즉 각 계층에서 전송되는 데이터 단위이다.  각각의 계층별 PDU를 따로부르는 이름이 있는데, 5~7계층은 메세지(Message), 4계층은 세그먼트 혹은 데이터 그램, 3계층의 PDU는 데이터그램 혹은 패킷, 2계층은 프레임 1계층은 신호라고 부른다.
![](6.jpg)  
* 데이터는 계층을 통과하면 할 수록 앞에 계속 Header가 붙는다 하지만 Data Link 계층에서는 헤더뿐만 아니라 특이하게 뒤에 트레일러를 추가한다.  
![](8.jpg)  
* PC1 에서 PC2로 데이터를 전송할때 Application Layer에서부터 Physical Layer 까지 내려가면서 데이터를 Capsulation하고 PC2에서는 Physical Layer에서부터 Application Layer까지 Decapsulation과정을 거쳐 즉 헤더를 하나씩 없애가면서 Data를 얻는다. 즉 PC1에 있는 Presentation Layer에서 캡슐화 하기 위한 Header를 PC2 Presentation Layer에서 그 정보를 처리하므로 Same-Layer Interaction 이라고 한다.
![](9.jpg)  
### OSI 7계층 각 계층별 역할
* 7계층 Application
  * 응용 계층으로 사용자에게 가장 가까운 계층이다. 7층에서 작동하는 응용프로그램은 사용자와 직접 상호작용 하는데 구글 크롬, 스카이프, 오피스 등의 응용프로그램이 대표적이고 HTTP나 FTP와 같은 서비스들을 제공한다.
* 6계층 Presentation
  * 데이터를 하나의 표현형태로 변환한다. 즉 응용프로그램 형식을 네트워크 형식으로 변환하거나 네트워크 형식을 응용프로그램 형식으로 변환한다. 그래픽 등의 확장자(JPEG, MPEG)가 여기에 해당한다.
* 5계층 Session
  * 컴퓨터와 서버간의 대화를 위해 세션을 만들어 준다. 즉 Port를 연결해준다고 생각하면 된다. 사용자같의 포트연결(세션)이 유효한지 확인하고 설정한다. 대표적인 프로토콜 로는 SSH,TLS가 있다.
* 4계층 Transport
  * 전체 메시지를 발신지 대 목적지(End to End)간 제어와 에러를 관리한다. 패킷들의 전송이 유효한지 확인하고 실패한 패킷은 다시보내는 등 신뢰성 있는 통신을 오류컴출 코드로를 이용하여 보장한다. 4계층 PDU를 세그먼트라고 하는데 여기에는 보낼 데이터의 용량과 속도 발신지 포트 목적지 포트 등이 저장되어 있다. 대표적인 프로토콜이 TCP(Transport Control Protocol)이다.
* 3계층 Network
  * 패킷을 발신지로부터 목적지로 전달할때 성공적이고 효과적으로 전달되도록 한다. 보스턴에 있는 컴퓨터가 캘리포니아에 있는 서버에 연결하려고 할 때 그 경로는 수백만 가지인데 이 계층에서 이 작업을 라우터가 효율적으로 처리한다. 따라서 패킷에는 패킷의 발신자 주소와 패킷의 수신자 주소 그리고 서비스 요청 정보가 들어있다. 대표적인 프로토콜은 IP(Internet Protocol)이다.
* 2계층 Data Link
  *  3계층에서 정보를 받아 주소와 제어정보를 Header와 Tail에 추가하고 스위치같은 장비를 통해 MAC주소를 이용하여 한 장치에서 다른 장치로 Frame을 전달한다. 즉 노드 대 노드 전달을 감독한다.
* 1계층 Physical
  * 케이블이나 연결 장치 등과 같은 기본적인 물리적 연결을 이용하여 두 노드를 물리적으로 연결하는 단계이다. 시스템의 전기적, 물리적 표현을 나타낸다.

## TCP/IP 모델
### TCP/IP 모델에서의 캡슐화
* 4계층 Application 
  * 응용 계층으로 L7H가 붙는게 아니라 HTTP나 FTP같은 헤더가 붙는다. 
  * OSI 7계층 모델에서 7~5 계층에 해당하는 일을 한다.

* 3계층 Transport 
  * 헤더에 TCP나 UDP가 붙으며 이와 같은 데이터를 세그먼트라고 한다.
  * OSI 7계층 모델에서 4계층에 해당한다.  

![](10.jpg)

* 2계층 Internet
  * 헤더에 IP가 붙으며 이와 같은 데이터를 패킷이라고 한다.
  * OSI 7계층 모델에서 3계층에 해당한다.

![](11.jpg)

* 1계층 Newtwork
  * 데이터에 Header와 Trailer가 붙으며 이와 같은 데이터를 Frame 이라고 한다.
  * OSI 7계층 모델에서 2~1계층에 해당한다.

![](14.jpg)


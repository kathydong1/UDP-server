package UDP;

import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

public class Udp {
  //数据结构--集合--队列
  //流
  //服务端的启动方法
	public static void main(String[] args) {
		Udp server=new Udp();
		 server.start();
		 

	}
	public void start(){
		try{
			/**
			 * 接收包的步骤；
			 * 1.创建socket一次
			 * 2.创建一个合适大小的包
			 * 3.通过socket接收数据到包中
			 * 4.拆包取数据
			 */
			//服务端必须指定端口，否者客户端发送的端口不能接收
			DatagramSocket socket=new DatagramSocket(8088);
			//创建一个字节长度位100的字节数组
			byte[] data=new byte[100];
			//创建一个包
			DatagramPacket recive=new DatagramPacket(data,data.length);
			//receive是阻塞方法，只有接收到数据后才会解除阻塞,接收数据到包中
			socket.receive(recive);
			//拆包取数据，getData方法取数据
			byte[] d=recive.getData();
			//getLength方法获取有效字节的长度
			int dlen=recive.getLength();
			//String(byte[],int offset,int len,Strubg charseName)
			//将给定的字符数组，从offset位置处，取len个长度，按照指定的字符集取出
			String info=new String(d,0,dlen,"UTF-8");
			System.out.println("客户端说:"+info);
			
			//回复客户端
			//获取字符串
	    	String strs="你好客户端";
	    	//将字符串转成字节
	    	 data=strs.getBytes("UTF-8");
	    	//打包：准备包裹，填写地址，装入数据,getAddress
	    	InetAddress address=recive.getAddress();
	    	int port=recive.getPort();
	    	//DatagramPacket接收四个参数，数组，要发送的长度，地址，端口，打包
	    	DatagramPacket sendpacket=new DatagramPacket(data,data.length,address,port);
	    	//发送方法，send(包)
	    	socket.send(sendpacket);
			
			
			
			
			
			
			
		}catch(Exception e){
		  e.printStackTrace();
			
		}
	}

}

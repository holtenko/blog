---
title: Java利用Rxtx进行串口通讯
date: 2015-12-05 16:04:02
categories: [Java]
tags: [Java,Library,Rxtx]
---

最近在做传感器数据采集的工作，底层是基于Zigbee的无线传感网络，所有数据采集到Zigbee协调器上然后通知上位机数据采集完成，上位机通过USB转串口去读取数据就可以了。那么问题来了，如何进行串口通讯呢？老板说你用Java写个程序好了嘛，用Java写串口程序也是醉了。实验室也没别人写了，所以就让我写了。当我听到要让我用Java写串口通讯程序的时候我本来是拒绝的，然后。。。就没有然后了。。就只能写了。

网上看了一下，最后用了一个开源的Java串口通讯库RXTX做串口通讯，下面记录一下RXTX的使用方法。

<!-- more -->

#### 环境配置

RXTX做串口通讯，有一个jar包(RXTXcomm.jar)和一个rxtxSerial.dll(Windows环境下)或者librxtxSerial.so（Linux环境下），因为开发是在Windows上，但是工作是在Linux上，所以两个都用到了。



**Windows环境下**

文档里是这么写的

> Copy rxtxSerial.dll ---> <JAVA_HOME>\jre\bin



但是这个做了之后并不能用，会有一些很奇怪的问题，不知道是不是我的Java环境配置有问题还是怎么了，我是把dll文件copy到了C:\Windows\System32，然后一切正常，一直很奇怪，为什么要cp到<JAVA_HOME>\jre\bin呢？求解答！



**Linux环境下**

> Copy librxtxSerial.so ---> <JAVA_HOME>/jre/lib/i386/

> or

> Copy librxtxSerial.so ---> <JAVA_HOME>/jre/lib/x86_64/



这个按照文档没问题。

    

    

**小问题**

我用的是rxtx-2.2pre2版本的，文档里有写运行时会报版本不匹配的WARNING，实际使用中的确也是这样的，不过目前还没有别的问题，不影响使用。

<br/>

#### 常用方法

1.查找端口



```java

/**

     * 查找所有可用端口

     *

     * @return 所有端口列表

     */

    public static final ArrayList<String> findPort() {

        Enumeration<CommPortIdentifier> portList = CommPortIdentifier.getPortIdentifiers();//获得所有串口

        ArrayList<String> portNameList = new ArrayList<>();

        //串口名字添加到List并返回

        while (portList.hasMoreElements()) {

            String portName = portList.nextElement().getName();

            portNameList.add(portName);

        }

        return portNameList;

    }

```

2.打开端口



```java

    /**

     * 打开串口

     *

     * @param portName 端口名称

     * @param baudrate 波特率

     * @return 串口对象

     */

    public static final SerialPort openPort(String portName, int baudrate) {

        try {

            //通过端口名识别端口

            CommPortIdentifier portIdentifier = CommPortIdentifier.getPortIdentifier(portName);

            //打开端口，并给端口名字和一个timeout

            CommPort commPort = portIdentifier.open(portName, 2000);

            //判断是不是串口

            if (commPort instanceof SerialPort) {

                SerialPort serialPort = (SerialPort) commPort;

                try {

                    //设置一下串口的波特率等参数

                    serialPort.setSerialPortParams(baudrate, SerialPort.DATABITS_8, SerialPort.STOPBITS_1, SerialPort.PARITY_NONE);

                } catch (UnsupportedCommOperationException e) {

                    LOGGER.error("Set Serialport Parameters failure", e);

                }

                System.out.println("Open " + portName + " sucessfully !");

                return serialPort;

            } else {

                LOGGER.error("This port is not a serialport");

                return null;

            }

        } catch (NoSuchPortException | PortInUseException e) {

            LOGGER.error("There is no " + portName + "or it's occupied!", e);

            return null;

        }

    }

```

3.发送数据

```java

    /**

     * 发送数据

     *

     * @param serialPort 串口对象

     * @param order      命令字节

     */

    public void sendToPort(SerialPort serialPort, byte[] order) {

        try {

            OutputStream out = serialPort.getOutputStream();

            out.write(order);

            out.flush();

            out.close();

        } catch (IOException e) {

            LOGGER.error("Send to SerialPort failure", e);

        }

    }

```

4.读取数据



```java

    /**

     * 读取数据

     *

     * @return 字节ArrayList

     */

    public byte[] readFromPort(InputStream inStream) {

        byte[] bytes = null;

        try {

            while (true) {

                //获取buffer里的数据长度

                int bufflenth = inStream.available();

                if (0 == bufflenth) {

                    break;

                }

                bytes = new byte[bufflenth];

                inStream.read(bytes);

            }

        } catch (IOException e) {

            LOGGER.error("Read Data Failure", e);

        }

        return bytes;

    }

```

<br/>  

#### 监听器

1.实现监听器

继承SerialPortEventListener然后重写serialEvent,然后再各个对应case里面写代码就好啦。

```java

public class TestExample implements SerialPortEventListener {

    @Override

    public void serialEvent(SerialPortEvent serialPortEvent) {

        switch (serialPortEvent.getEventType()) {

            case SerialPortEvent.BI: // 10通讯中断

            case SerialPortEvent.OE: // 7溢位错误

            case SerialPortEvent.FE: // 9帧错误

            case SerialPortEvent.PE: // 8奇偶校验错

            case SerialPortEvent.CD: // 6载波检测

            case SerialPortEvent.CTS: // 3清除发送

            case SerialPortEvent.DSR: // 4数据设备准备好

            case SerialPortEvent.RI: // 5振铃指示

            case SerialPortEvent.OUTPUT_BUFFER_EMPTY: // 2输出缓冲区已清空

            case SerialPortEvent.DATA_AVAILABLE: // 1读到可用数据时激活

        }

    }

}

```

2.给串口添加监听器



```java

    /**

     * 添加监听器

     *

     * @param port     串口对象

     * @param listener 串口监听器

     */

    public static void addListener(SerialPort port, SerialPortEventListener listener) {

        try {

            // 给串口添加监听器

            port.addEventListener(listener);

            // 设置当有数据到达时唤醒监听接收线程

            port.notifyOnDataAvailable(true);

            port.notifyOnBreakInterrupt(true);

            System.out.println("Add listeners to " + port.getName() + " sucessfully !");

        } catch (TooManyListenersException e) {

            LOGGER.error("There is too many listeners !", e);

        }

    }

```



#### TIP

** 一定记得从串口发指令取数据之后加一个延时，等待底层数据传输完成再去buffer里面取，不然很大可能数据包不完整。 **
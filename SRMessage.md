# Mind-
My Homework

/*!
 * MindPlus
 * mpython
 *
 */
 
#include <MPython.h>

#include <DFRobot_Iot.h>

// 函数声明

void obloqMqttEventT0(String& message);

// 静态常量

const String topics[5] = {"9PhuhMFMR","9boX2GKMg","","",""};

const MsgHandleCb msgHandles[5] = {obloqMqttEventT0,NULL,NULL,NULL,NULL};

// 创建对象

DFRobot_Iot myIot;



// 主程序开始

void setup() {

	mPython.begin();
	
	myIot.setMqttCallback(msgHandles);
	
	myIot.wifiConnect("Snoopy", "s20000113");
	
	while (!myIot.wifiStatus()) {yield();}
	
	display.setCursorLine(1);
	
	display.printLine("wifi连接成功");
	
	myIot.init("iot.dfrobot.com.cn","gD2uhGKMR","","gDhXhMFGgz",topics,1883);
	
	myIot.connect();
	
	while (!myIot.connected()) {yield();}
	
	display.setCursorLine(2);
	
	display.printLine("MQTt连接成功");
	
}

void loop() {

	if ((buttonA.isPressed())) {
	
		myIot.publish(topic_1, "2018764239史佩莹");
		
	}
	
}



// 事件回调函数

void obloqMqttEventT0(String& message) {

	display.setCursorLine(3);
	
	display.printLine(message);
	
}


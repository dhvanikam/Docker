# Execution modes

* **Standalone**
* **Hub and Nodes**
  * Docker networking : https://github.com/SeleniumHQ/docker-selenium?tab=readme-ov-file#docker-networking
  * Using different machines/VMs : https://github.com/SeleniumHQ/docker-selenium?tab=readme-ov-file#using-different-machinesvms
  * Docker Compose : https://github.com/SeleniumHQ/docker-selenium?tab=readme-ov-file#docker-compose

We are going to focus mainly on Docker-Compose, But before that lets see how to run in Standalone mode.

## Docker - Standalone mode on macOS


![docker drawio](https://github.com/dhvanikam/Docker/assets/73573915/7ab78eb0-ff18-4f2b-998d-d509051d1d8a)




As I am using macOS, I am following https://github.com/seleniumhq-community/docker-seleniarm specific to my system which is ARM.

For other System Make sure to visit : https://github.com/SeleniumHQ/docker-selenium 

Lets get Started,

## Start the Containers in Standalone mode 
**Step 1**: Make sure Docker Engine is Running

<img width="1338" alt="Step5" src="https://github.com/dhvanikam/Docker/assets/73573915/cec59d2c-a9e8-4c47-a443-23e55f19ce0d">


**Step 2**: Open Terminal to run commands to start containers

Start Chrome standalone:

```
docker run --rm -it -p 4444:4444 -p 5900:5900 -p 7900:7900 --shm-size 2g seleniarm/standalone-chromium:latest
```

* Point your WebDriver tests to http://localhost:4444
* Use your traditional VNC client via port 5900, and noVNC in the browser via port 7900.
* When executing docker run for an image that contains a browser please use the flag --shm-size=2g to use the host's shared memory.
  
Start Firefox standalone:

```
docker run --rm -it -p 4445:4444 -p 5901:5900 -p 7901:7900 --shm-size 2g seleniarm/standalone-firefox:latest

```

* Point your WebDriver tests to http://localhost:4445
* Use your traditional VNC client via port 5901, and noVNC in the browser via port 7901.
* **No need to pull image in advance as Docker will pull that image if it was not existed locally**



**Step 3**: Check Docker Desktop for running chrome and firefox containers in standalone mode.

<img width="1747" alt="Step7" src="https://github.com/dhvanikam/Docker/assets/73573915/56c4dcef-8b18-4335-9eec-10f927fe6eb3">

**Step 4**: Navigate to URLs http://localhost:4444 & http://localhost:4445

<img width="2240" alt="Step8" src="https://github.com/dhvanikam/Docker/assets/73573915/4e98d896-cb5e-4d69-a890-c46b7aab1988">


## Update your selenium tests to point to the respective urls:
**DriverFactory.java**

```java
		if (browser.equalsIgnoreCase("firefox")) {
			Loggerload.info("Testing on firefox");
			WebDriverManager.firefoxdriver().setup();
			DesiredCapabilities capability = new DesiredCapabilities();
			capability.setPlatform(Platform.LINUX);
			capability.setBrowserName(browser);
			driver = new RemoteWebDriver(new URL("http://localhost:4445/"), capability);

		} else if (browser.equalsIgnoreCase("chrome")) {
			Loggerload.info("Testing on chrome");
			DesiredCapabilities capability = new DesiredCapabilities();
			capability.setPlatform(Platform.LINUX);
			capability.setBrowserName(browser);
			WebDriverManager.chromedriver().setup();
			driver = new RemoteWebDriver(new URL("http://localhost:4444/"), capability);

```
**TestNG.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="Suite"  thread-count="3">
	<test name="Chrome Test">
		<parameter name="browser" value="chrome"></parameter>
		<classes>
			<class name="runner.TestRunner" />
		</classes>
	</test> <!-- Test -->

	<test name="Firefox Test">
		<parameter name="browser" value="firefox"></parameter>
		<classes>
			<class name="runner.TestRunner" />
		</classes>
	</test> <!-- Test -->
</suite> <!-- Suite -->
```
 So, Chrome container will run test on Chrome browser, Firefox container will run test on Firefox

Navigate to : 
* For chrome noVNC : http://localhost:7900/?autoconnect=1&resize=scale&password=secret
* For firefox noVNC : http://localhost:7901/?autoconnect=1&resize=scale&password=secret

Now lets run the project

https://github.com/dhvanikam/Docker/assets/73573915/fa5f3012-18c6-4a94-a280-51502d12738e


Chrome: While test is running
<img width="1884" alt="Chrome" src="https://github.com/dhvanikam/Docker/assets/73573915/45cc093e-ea13-4410-b20f-7871e87a3d5b">

Firefox :While test is running
<img width="1884" alt="firefox" src="https://github.com/dhvanikam/Docker/assets/73573915/b8ae91e8-6a62-46c5-b87b-e7749cb7f5d8">


So that was it for stand alone mode. 

**The major downside of performing tests in a below execution modes, is low scalability and starting containers separately**. 
* Standalone container
* Hub and Nodes
  * Docker networking 
  * Using different machines/VMs 
 

We can overcome this issue with Docker Compose. 

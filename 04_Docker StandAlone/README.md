# Execution modes

* **Standalone**
* **Hub and Nodes**
  * Docker networking : https://github.com/SeleniumHQ/docker-selenium?tab=readme-ov-file#docker-networking
  * Using different machines/VMs : https://github.com/SeleniumHQ/docker-selenium?tab=readme-ov-file#using-different-machinesvms
  * Docker Compose : https://github.com/SeleniumHQ/docker-selenium?tab=readme-ov-file#docker-compose

We are going to focus mainly on Docker-Compose, But before that lets see how to run in Standalone mode.

## Docker - Standalone mode on macOS


![docker2 drawio](https://github.com/dhvanikam/Docker/assets/73573915/95bf8bfb-ea60-4aa0-a88d-a49f4337c7d5)


## Start the Containers in Standalone mode 

### Step 1: Find the correct images and docker run command from Docker Hub.
Lets check that image that we want to start container for is availble in Docker hub, Go to : https://hub.docker.com and Search "Selenium"

#### For Windows and Linux:

Here we are looking for 
* Chrome image : selenium/standalone-chrome (https://hub.docker.com/r/selenium/standalone-chrome) 
* Firefox image : selenium/standalone-firefox (https://hub.docker.com/r/selenium/standalone-firefox)

<img width="1421" alt="DockerHub" src="https://github.com/dhvanikam/Docker/assets/73573915/21be887f-a624-4893-bf90-90b71b593552">

Make sure to filter images according to your system requirement.

Now, Click on image one by one and copy the commands,

<img width="1175" alt="chromecommand" src="https://github.com/dhvanikam/Docker/assets/73573915/aeda2cd0-f4bb-424b-9096-0f1a50cbeb01">

<img width="1175" alt="firefoxcommand" src="https://github.com/dhvanikam/Docker/assets/73573915/f9406610-0f50-4795-9492-d40f089bad94">


More details on : https://github.com/SeleniumHQ/docker-selenium 

#### For macOS - ARM, ARM64:
As I am using macOS - ARM64 which has spefic system requirment for that visit : https://hub.docker.com/u/seleniarm

Here we are looking for 
* Chrome image : seleniarm/standalone-chromium (https://hub.docker.com/r/seleniarm/standalone-chromium)
* Firefox image : seleniarm/standalone-firefox (https://hub.docker.com/r/seleniarm/standalone-firefox)

More details on : https://github.com/seleniumhq-community/docker-seleniarm

Now we know the images Lets get Started,


### Step 2: Make sure Docker Engine is Running,

<img width="1277" alt="DockerDesktop" src="https://github.com/dhvanikam/Docker/assets/73573915/328b110a-8d41-455b-9343-7d595c418251">


### Step 3: Open Terminal to run commands to start containers

Start Chrome standalone:

* **For Windows and Linux**:
```
docker run -d -p 4444:4444 -p 7900:7900 --shm-size="2g" selenium/standalone-chrome:latest
```

* **macOS - ARM64 System**
```
docker run --rm -it -p 4444:4444 -p 5900:5900 -p 7900:7900 --shm-size 2g seleniarm/standalone-chromium:latest
```

* Point your WebDriver tests to http://localhost:4444
* Use your traditional VNC client via port 5900, and noVNC in the browser via port 7900.
* When executing docker run for an image that contains a browser please use the flag --shm-size=2g to use the host's shared memory.
  
Start Firefox standalone:

* **For Windows and Linux**:
```
docker run -d -p 4444:4444 -p 7900:7900 --shm-size="2g" selenium/standalone-firefox:latest
```
* **macOS - ARM64 System**
```
docker run --rm -it -p 4445:4444 -p 5901:5900 -p 7901:7900 --shm-size 2g seleniarm/standalone-firefox:latest

```

* Point your WebDriver tests to http://localhost:4445
* Use your traditional VNC client via port 5901, and noVNC in the browser via port 7901.
* **No need to pull image in advance as Docker will pull that image if it was not existed locally**



### Step 4: Check Docker Desktop for running chrome and firefox containers in standalone mode.

<img width="1747" alt="Step7" src="https://github.com/dhvanikam/Docker/assets/73573915/56c4dcef-8b18-4335-9eec-10f927fe6eb3">

### Step 5: Navigate to URLs http://localhost:4444 & http://localhost:4445

<img width="2240" alt="Step8" src="https://github.com/dhvanikam/Docker/assets/73573915/4e98d896-cb5e-4d69-a890-c46b7aab1988">


### Step 6: Update your selenium tests to point to the respective urls:
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

**The major downside of performing tests in a below execution modes, is and starting containers separately**. 
* Standalone container - low scalability 
* Hub and Nodes
  * Docker networking 
  * Using different machines/VMs 
 

We can overcome this issue with Docker Compose.

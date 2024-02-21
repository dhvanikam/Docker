# Docker Compose Example

Find sample Project on : https://github.com/dhvanikam/DockerSampleProject 

**Step 1**: Point RemoteWebDriver in your test to http://localhost:4444 

Update your selenium tests to point to the respective urls:
**DriverFactory.java**

```java
		if (browser.equalsIgnoreCase("firefox")) {
			Loggerload.info("Testing on firefox");
			WebDriverManager.firefoxdriver().setup();
			DesiredCapabilities capability = new DesiredCapabilities();
			capability.setPlatform(Platform.LINUX);
			capability.setBrowserName(browser);
			driver = new RemoteWebDriver(new URL("http://localhost:4444/"), capability);

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

**Step 2**: Make sure Docker Engine is running

**Step 3**: Go to your project directory where "docker-compose-v2.yml" is residing

<img width="561" alt="Step8" src="https://github.com/dhvanikam/Docker/assets/73573915/08afc2c3-fbfc-4a64-8f2e-2a0b89f5f53f">


Run the docker compose file

To execute this docker-compose yml file use
```
docker-compose -f docker-compose-v2.yml up
```
Add the -d flag at the end for detached execution

```
docker-compose -f docker-compose-v2.yml up -d
```
<img width="873" alt="Step9" src="https://github.com/dhvanikam/Docker/assets/73573915/6e6d8820-ed9c-4714-b39b-c897c20eda02">


**Step 4**: Check the Docker Desktop

<img width="1747" alt="Step10" src="https://github.com/dhvanikam/Docker/assets/73573915/edb4665a-2f3b-4853-a5c0-a2de0175a0f5">

**Step 5**: http://localhost:4444 

<img width="1480" alt="Step11" src="https://github.com/dhvanikam/Docker/assets/73573915/f585e56a-be66-49ff-a9c9-30b9e59c683e">

**Step 6**: Now Run the test

https://github.com/dhvanikam/Docker/assets/73573915/046f7132-5621-4210-ac97-f6b36bf301f5


**Step 7**: Now all test are done so lets stop the containers

```
docker-compose -f docker-compose-v2.yml down
```

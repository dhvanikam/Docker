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

**Step 2**: Go to your project directory where "docker-compose-v2.yml" is residing

Run the docker compose file

To execute this docker-compose yml file use
```
docker-compose -f docker-compose-v2.yml up
```
Add the -d flag at the end for detached execution

```
docker-compose -f docker-compose-v2.yml up -d
```

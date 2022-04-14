# Project Structure

The recommended project structure is as follows :
```
├── pom.xml
└── src
    ├── main
    │   └── java
    │       └── pages
    │           ├── WebsiteHomePage.java
    │           └── WebsiteLoginPage.java
    └── test
        ├── java
        │   └── TetikusCoreRunner.java
        └── resources
            ├── driverconfig.json
            ├── tetikus.properties
```

### pages/*Page.java
`WebsiteHomePage` and other classes inside the `pages` folder contains objects that model actions that you do to a website / application under test (AUT), such as clicking button or typing into a field. These classes need to extend Tetikus' `PageObject` class.

Example :
```java
@BaseURL("https://www.medium.com")
public class WebsitePage extends PageObject {
    @Locator(webXPath = "//a[text()='Sign In']",
            mobileID = "com.medium.reader:id/sign_in_prompt")
    private Element signInButton;

    @Locator(webXPath = "//div[text()='Sign in with Twitter']",
            mobileID = "com.medium.reader:id/sign_in_twitter_button")
    private Element signInWithTwitterButton;

    public void goToTwitterLoginPage() {
        signInButton.waitUntilClickable().click();
        signInWithTwitterButton.waitUntilClickable().click();
    }
}
```

You may also want to read more about Page Object design pattern here.
https://www.selenium.dev/documentation/test_practices/encouraged/page_object_models/


### TetikusCoreRunner.java
`TetikusCoreRunner` acts as a runner that will provide driver configuration to each of tests you create. This class needs to extend Tetikus' `TetikusBaseRunner` class. 

Example :
```java
public class TetikusCoreRunner extends TetikusBaseRunner {
    private HomePage homePage;
    private LoginPage loginPage;

    @Test
    public void login() {
        homePage.openPage();
        homePage.goToTwitterLoginPage();

        loginPage.fillTwitterLoginCredentials("username", "password");
    }
}
```
  
### driverconfig.json
`driverconfig.json` is where you put the configuration of your driver. You can specify the configuration for mobile and web, and also for web you can also specify whether you want to run it locally (driver would be setup by WebDriverManager library) or remotely.

Example :
```json
[
  {
    "platform": "MOBILE",
    "url": "http://127.0.0.1:4723/wd/hub",
    "desiredCapabilities": {
      "automationName": "UiAutomator2",
      "platformName": "Android",
      "udid": "emulator-5554",
      "appPackage": "com.medium.reader",
      "appActivity": "com.medium.android.donkey.start.SplashActivity"
    }
  },
  {
    "platform": "WEB",
    "location": "LOCAL",
    "browser": "CHROME"
  }
]
```

### tetikus.properties
You can use `tetikus.properties` to change configuration that's provided by Tetikus. Currently, behaviour that you can configure are :
- Where you want to store driver configuration (`driverconfig.json`)
- Whether you want to keep browser / application session such as login session, and where you want to store the session
- Whether you want to generate report after running tests

Example :
```properties
driver.configuration.path=driver-config
driver.keep.session=true
driver.session.folder.path=browser-session/chrome-cache-dir
report.enabled=true
```

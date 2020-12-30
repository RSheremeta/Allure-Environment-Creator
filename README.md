# Allure-Environment-Creator
This tiny Library helps you to serve and store environment data for Allure easily.

## Installation
1 Since it's not pushed to the MVN central repository yet, there are two installation options:

a) Download already compiled and packaged **.jar** file [here]("https://") and proceed to the 2nd step
b) Pull this repo to your local machine, make a jar by running **`mvn package`** in the repo directory and proceed to the 2nd step

2 Put a **.jar** file into your project directory (for instance – create root dir `~/libs/` and paste there)

3 Add this dependency to your `pom.xml` (**systemPath** value is for instance)
````
    <dependency>
      <groupId>com.github.rsheremeta</groupId>
      <artifactId>Allure-Environment-Creator</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${basedir}/libs/Allure-Environment-Creator-1.0.jar</systemPath>
    </dependency>
````

## Usage
1. In your ``@BeforeSuite`` or ``@AfterSuite`` method (or ``@BeforeClass`` or ``@AfterClass`` for **JUnit**):
````
  @BeforeSuite(alwaysRun = true)
  public void beforeSuiteSetUp() {
    // Instantiate a map with your needed Environment values
    Map<String, String> envData = new HashMap<>();
    envData.put("Base URL", "https://google.com/");
    envData.put("User", "Admin");
    envData.put("OS", System.getProperty("os.name"));
    
    /*
    If your /allure-results is in /target – just pass instantiated map as a parameter
    */ 
    AllureEnv.createAllureEnvironmentFile(envData);
    
    /*
    If your /allure-results is in custom directory – just pass one more parameter with customPath to your /allure-results directory
    */ 
    AllureEnv.createAllureEnvironmentFile(envData, "/");
    
    // some your other code
  }
````

2. Now you're all set to run your suite.

3. Once suite is finished, generate allure report and take a look on the **Environment** section:
![Allure Report Results](https://ibb.co/3djVmcp)

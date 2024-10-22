package rahulshettyacademy.TestComponents;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.time.Duration;
import java.util.HashMap;
import java.util.List;
import java.util.Properties;

import org.apache.commons.io.FileUtils;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.edge.EdgeDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;

import com.fasterxml.jackson.core.type.TypeReference;
import com.fasterxml.jackson.databind.ObjectMapper;

import io.github.bonigarcia.wdm.WebDriverManager;
import rahulshettyacademy.PageObjects.LandingPage;

public class BaseTest {
	public WebDriver driver;
	public LandingPage landingPage;

	public WebDriver initializeDriver() throws IOException {

		Properties prop = new Properties();

		FileInputStream fis = new FileInputStream(
				System.getProperty("user.dir") + "/src/main/java/rahulshettyacademy/resources/GlobalData.properties");

		prop.load(fis);

		String browserName = prop.getProperty("browser");

		// if (browserName.contains("chrome")) check for substring contains

		if (browserName.equalsIgnoreCase("chrome"))
		// check for exact match
		{
			WebDriverManager.chromedriver().setup();
			driver = new ChromeDriver();

		} else if (browserName.equalsIgnoreCase("firefox")) {

		} else if (browserName.equalsIgnoreCase("edge")) {
			
			System.setProperty("webdriver.chrome.driver",
					"C:/Users/sivaj/OneDrive/Desktop/Selenium/Software/edgedriver_win64/msedgedriver.exe");

			driver = new EdgeDriver();

		}
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(5));
		return driver;
	}
	
	public List<HashMap<String, String>> getJsonDataToMap(String filePath) throws IOException {
		String jsonContent=	FileUtils.readFileToString(new File(filePath), StandardCharsets.UTF_8);

		ObjectMapper mapper= new ObjectMapper();
		List<HashMap<String,String>> data = mapper.readValue(jsonContent,new TypeReference<List<HashMap<String,String>>>() {});
		return data;
		//map, map1
			
		}

public String getScreenShot(String testCaseName, WebDriver driver) throws IOException {
	File screenshotFile = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
	File file=new File(System.getProperty("user.dir")+"//reports//"+testCaseName+".png");
	FileUtils.copyFile(screenshotFile, file);	
	return System.getProperty("user.dir")+"//reports//"+testCaseName+".png";
}	



	@BeforeMethod
	public LandingPage launchApplication() throws IOException {

		driver = initializeDriver();
		landingPage = new LandingPage(driver);
		landingPage.goTo();
		return landingPage;

	}

	@AfterMethod
	public void closeDriver() {
		driver.close();
	}
}

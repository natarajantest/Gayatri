package package1;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;

public class TestOpenEMR {

	public static void main(String[] args) throws InterruptedException {
		
		WebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
		driver.get("https://demo.openemr.io/d/openemr");
		
		driver.findElement(By.id("authUser")).click();
		driver.findElement(By.id("authUser")).sendKeys("admin");
		driver.findElement(By.id("clearPass")).click();
		driver.findElement(By.id("clearPass")).sendKeys("pass");
		driver.findElement(By.xpath("//i[@class='fa fa-sign-in']")).click();
		
		Actions act=new Actions(driver);
		act.moveToElement(driver.findElement(By.xpath("//div[text()='Patient/Client']"))).build().perform();
		driver.findElement(By.xpath("//div[text()='New/Search']")).click();
		
		
		driver.switchTo().frame(driver.findElement(By.xpath("//iframe[@name='pat']")));
	    driver.findElement(By.xpath("//input[@name='form_fname']")).click();
		driver.findElement(By.xpath("//input[@name='form_fname']")).clear();
		driver.findElement(By.xpath("//input[@name='form_fname']")).sendKeys("Gayatri");
		driver.findElement(By.name("form_lname")).click();
		driver.findElement(By.name("form_lname")).clear();
		driver.findElement(By.name("form_lname")).sendKeys("Bhosale");
		
		driver.findElement(By.xpath("//input[@id='form_DOB']")).click();
		driver.findElement(By.xpath("//div[text()='17']")).click();
		
	
		Select sel1=new Select(driver.findElement(By.name("form_sex")));
	    sel1.selectByVisibleText("Female");
	  
	    
	    driver.findElement(By.name("create")).click();
	    driver.switchTo().defaultContent();
	   
	    driver.switchTo().frame(driver.findElement(By.xpath("//iframe[@class='embed-responsive-item modalIframe']")));
	    driver.findElement(By.xpath("//input[@value='Confirm Create New Patient']")).click();
	    Thread.sleep(3000);
	    driver.switchTo().alert().accept();
	   
	    driver.findElement(By.className("closeDlgIframe")).click();
	    
	    driver.switchTo().defaultContent();
	    act.moveToElement(driver.findElement(By.xpath("//div[@class='menuSection userSection']"))).build().perform();
	    driver.findElement(By.xpath("//ul//li[text()='Logout']")).click();

	}

}

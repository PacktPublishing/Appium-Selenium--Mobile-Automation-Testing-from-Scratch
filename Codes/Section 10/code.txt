import io.appium.java_client.android.AndroidDriver;

import io.appium.java_client.remote.MobileCapabilityType;

import io.appium.java_client.remote.MobilePlatform;

import java.io.File;

import java.net.MalformedURLException;

import java.net.URL;

import java.util.Set;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;

import org.openqa.selenium.remote.DesiredCapabilities;

public class Hybridapps {

public static void main(String[] args) throws MalformedURLException {

// TODO Auto-generated method stub

File appDir = new File("src");

File app = new File(appDir, "testApp.apk");

DesiredCapabilities cap=new DesiredCapabilities();

cap.setCapability(MobileCapabilityType.PLATFORM_NAME,MobilePlatform.ANDROID);

cap.setCapability(MobileCapabilityType.DEVICE_NAME, "Android device");

cap.setCapability(MobileCapabilityType.NEW_COMMAND_TIMEOUT, "100");

cap.setCapability(MobileCapabilityType.APP, app.getAbsolutePath());

AndroidDriver driver=new AndroidDriver(new URL("http://127.0.0.1:4723/wd/hub"),cap );

driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);

System.out.println(driver.getContext());

driver.findElement(By.id("com.example.testapp:id/urlField")).sendKeys("http://google.com");

driver.findElement(By.id("com.example.testapp:id/goButton")).click();

Set<String> s=driver.getContextHandles();

for(String handle : s)

{

System.out.println(handle);

}

driver.context("WEBVIEW_com.example.testapp");

//To enable WebView debugging, call the static method setWebContentsDebuggingEnabled on the WebView class.

driver.findElement(By.name("q")).sendKeys("Handling hybrid app");

//

driver.context("NATIVE_APP");

//

//1 native 1 Web

//driver.context(name)

}

}
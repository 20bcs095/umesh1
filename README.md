WiFi.begin(ssid, password);
  while ( WiFi.status() != WL_CONNECTED ) {
    delay ( 500 );
    Serial.print ( "." );
  }
    timeClient.begin();
  mlx.begin(); 
  display.begin(SSD1306_SWITCHCAPVCC, 0x3C); //Start the OLED display
  display.clearDisplay();
  display.display();
  
 secured_client.setCACert(TELEGRAM_CERTIFICATE_ROOT);
   bot.sendMessage(CHAT_ID, "pillbox connected", "");

}

void loop() {
   timeClient.update();
   int h = timeClient.getHours();
    int s = timeClient.getMinutes();
   String sh = String(h);
   String ss = String(s);
   String t = sh + ":" +ss;

    String time = "2:15";
   //delay(5000);
   if (time == t){
  buzzer();
   }
   Serial.println(t);
  display.clearDisplay();
  
  display.setTextSize(1.5);                    
  display.setTextColor(WHITE);             
  display.setCursor(0,4);                
  display.println("Smart Pillbox"); 
   display.display();
   delay(5000);
    display.clearDisplay();
  
  display.setTextSize(1);                    
  display.setTextColor(WHITE);             
  display.setCursor(0,20);                
  display.println("Alert AT"); 
  
  display.setTextSize(2);
  display.setCursor(50,17);
  display.println(time);
  

  
  display.display();
  
  
  delay(5000);

}

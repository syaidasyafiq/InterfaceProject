# InterfaceProject
Interface for Radio Tester (Ramsey COM3010 )
#include <SoftwareSerial.h>
#include <SPI.h>
#include <UIPEthernet.h>

//DEKLARASI
SoftwareSerial Serial1 (5,6); // INISIALISASI RS232
byte mac [] = {0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED};
IPAddress ip(192, 168, 169, 177);// IP ADRESS YANG DIDAPAT BERGANTUNG PADA JARINGAN YANG TERKONEKSI
EthernetServer server(80);// PORT DEFAULT UNTUK HTTP
String inString = ""; // INISIALISASI UNTUK TIPE DATA YANG DIGUNAKAN


void setup() 
{
Ethernet.begin(mac, ip); // MEMULAI KONEKSI ETHERNET
server.begin();
Serial1.begin(9600); // KEC.TRANSMISI DATA MENYESUAIKAN DEFAULT RAMSEY COM3010
}

void loop() 
{
   EthernetClient client = server.available();
   if (client.available()>0) // MENYATAKAN DATA YANG SIAP DIBACA DARI SERIAL PORT 
                            // YANG TELAH DITERIMA DAN DISIMPAN PADA RECEIVE BUFFER
  {
      char thisChar = client.read();
      inString = client.readString();
      
      if (thisChar == 'a')
      {
        Serial1.println("SYS OPEN 555");
        inString = Serial1.findUntil("Welcome from unit 555","\r\n");
        inString = Serial1.readStringUntil("\r");
        client.print(inString); 
      }
      
      if (thisChar == 'x')
      {
        Serial1.println("SYS CLOSE"); 
        inString = Serial1.findUntil("Disconnecting, bye.","\r\n");
        inString = Serial1.readStringUntil("\r");
        client.print(inString);
      }
      
      if (thisChar=='b') 
      {
        Serial1.println("SET GAM");
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }
      }
      
      if (thisChar=='q') 
      {
        Serial1.println("SET GFM");
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }
      }
      
      if (thisChar=='i') 
      {
        Serial1.println("SET MINT ON");
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }
      }
      
      if (thisChar=='j') 
      {
        Serial1.println("SET MEXT ON");
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }
      }
      
      if (thisChar=='o') 
      {
        Serial1.println("SET GEN ON");
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }
      }
      
      if (thisChar == 'c')
      {
        Serial1.print("SET GF ");   
        Serial1.println(inString);
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }            
      }
      
      if (thisChar == 'd')
      {
        Serial1.print("SET RF ");
        Serial1.println(inString);
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }            
      }
      
      if (thisChar == 'e')
      {
        Serial1.print("SET INT% ");
        Serial1.println(inString);
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }            
      }
      
      if (thisChar == 'p')
      {
        Serial1.print("SET EXT% ");
        Serial1.println(inString);
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }            
      }
      
      if (thisChar == 'l')
      {
        Serial1.print("SET INTDEV ");
        Serial1.println(inString);
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }            
      }
      
      if (thisChar == 'n')
      {
        Serial1.print("SET EXTDEV ");
        Serial1.println(inString);
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }            
      }
      
      if (thisChar == 'k')
      {
        Serial1.print("SET LEVEL ");
        Serial1.println(inString);
        inString = Serial1.findUntil("OK" ,"\r\n");
        inString = Serial1.readStringUntil("\r"); 
        if(inString)
        {
          client.print(inString);
        }
        else
        {
          client.print("BAD");
        }            
      }
      
      if (thisChar == 'f')
      {
        Serial1.print("GET LEVEL\r");
        inString = Serial1.findUntil("dBm","\r\n");
        inString = Serial1.readStringUntil("\r");
        client.println(inString);
      }
      
      if (thisChar == 'g')
      {
        Serial1.print("GET POWER\r");
        inString = Serial1.findUntil("W", "\r\n");
        inString = Serial1.readStringUntil("\r");
        client.println(inString);
      }
    }
}


void Logout(EthernetClient client )
{ 
  client.print('x');
  client.stop(); 
}

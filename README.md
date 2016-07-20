# cryo-genix
In this era of life people are becoming more lazy, they just want everything by their side without any efforts. They just like to sit on a couch watch TV for whole day.
If the light is switched ON they don't care about that because they don't want to move from the comfortness. To overcome this here is a small and simple mini project that anyone can make.
A home automation device controlled by using TV remote and IR receiver with help of Arduino. By which you can turn ON and turn OFF your electric devices using your TV remote.
lets get started:
Things needed: Arduino UNO,  IR receiver, TV remote, 4 channel relay switch, few jumper wire.
To connect the 4 channel relay you need to be more carefull, as it has connections with the main AC source. A seprate connection will be given to the relay.
Connect +5v and ground to relay board and for IR receiver connect pin 11 to signal pin and 5v and ground to respective pins.
The realy 4 pins to be connected to pin 2,3,4,5 respectively, and note down that what device is connected to which pin number.
The device two terminals(main and ground) are connected as main to NO and ground to COMMON of the relay board, as it has to work as a switch.
The relay consist of a magnetic coil connected to the pin which recives the signal from arduino that whan to make HIGH and LOW, and the coil acts like a switch.
THE CODE:
Here is the example code in which the devices are named as led, so don't get confused.
And please do add the IR library before compiling the program else it will dispaly an error.


 #include <IRremote.h>
 int RECV_PIN = 11; 
 int led1 = 2;
 int led2 = 3;
 int led3 = 4;
 int led4 = 5;



 int itsONled[] = {0,0,0,0,0,};
 #define code1   20655
 #define code2   55335 
 #define code3   63495 
 #define code4   12495 

 IRrecv irrecv(RECV_PIN);
 
 decode_results results;
 
 void setup()
 {
   Serial.begin(9600);   
   irrecv.enableIRIn();  
   pinMode(led1, OUTPUT);
   pinMode(led2, OUTPUT);
   pinMode(led3, OUTPUT);
   pinMode(led4, OUTPUT);
    
   
   }
 
void loop() {
     if (irrecv.decode(&results)) {
     unsigned int value = results.value;
     switch(value) {
       case code1:
         if(itsONled[1] == 1) {       
            digitalWrite(led1, LOW);   
            itsONled[1] = 0;           
         } else {                      
             digitalWrite(led1, HIGH); 
             itsONled[1] = 1;          
         }
          break; 
            case code2:
         if(itsONled[2] == 1) {
            digitalWrite(led2, LOW);
            itsONled[2] = 0;
         } else {
             digitalWrite(led2, HIGH);
             itsONled[2] = 1;
         }
          break;
            case code3:
         if(itsONled[3] == 1) {
            digitalWrite(led3, LOW);
            itsONled[3] = 0;
         } else
         {
             digitalWrite(led3, HIGH);
             itsONled[3] = 1;
         }
          break;
            case code4:
         if(itsONled[4] == 1) {
            digitalWrite(led4, LOW);
            itsONled[4] = 0;
         } else
         {
             digitalWrite(led4, HIGH);
             itsONled[4] = 1;
         }
          break;
         
  }
    Serial.println(value);
    irrecv.resume();
  }
}

The code1, code2,...... are the value in HEX recived by the remote it changes with different remote, so just check the code for your remote using serial moniter.
Then change the code value with yours value, and upload the program again.


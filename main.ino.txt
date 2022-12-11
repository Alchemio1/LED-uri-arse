#include <string.h>

#include <SoftwareSerial.h>

//SoftwareSerial myserial(A1, A2);      // rx , tx

const byte numChars = 32;
char receivedChars[numChars]; // an array to store the received data
boolean newData = false;

int i;
int in1=2;
int in2=4;
int enA=3;
int in3=5;
int in4=7;
int enB=6;
int m1=A3, m2=A4, m3=A5;
int in1b=8;
int in2b=13;
int enAb=10;
int in3b=12 ;
int in4b=11;
int enBb=9;

int vrx=A5; int mapx=0;
int vry=A4; int mapy=0;
int pozx=0; int pozy=0;
void setup()
{
  pinMode(A0, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(enA, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
  pinMode(enB, OUTPUT);
  pinMode(in1b, OUTPUT);
  pinMode(in2b, OUTPUT);
  pinMode(enAb, OUTPUT);
  pinMode(in3b, OUTPUT);
  pinMode(in4b, OUTPUT);
  pinMode(enBb, OUTPUT);
  pinMode(m1, OUTPUT);
  pinMode(m2, OUTPUT);
  pinMode(m3, OUTPUT);
  pinMode (vrx,INPUT);
  pinMode (vry,INPUT);
  Serial.begin(9600);
}

void recv()
{

    // the byte we are currently on
    static byte ndx;
    char endMark = '\n';
    // character currently reading
    char ch;


    // we read data until we have enough
    while(Serial.available() > 0)// && newData==false)
    {
      // read character from bluetooth device
      ch = Serial.read();

      if(ch != endMark)
      {
        // store the read character
        receivedChars[ndx] = ch;
        // increse the character counter
        ndx++;

        // see if we exceed the buffer
        if(ndx >= numChars)
          ndx = numChars - 1;
      }
      else
      { // we have reached the end of the message
         receivedChars[ndx] = '\0';
         ndx = 0;
         //newData = true;  
      }
    }
}

void loop()
  
{
  digitalWrite(A0, HIGH);

  recv();

  if(!strcmp(receivedChars, "1"))
  {

    digitalWrite(enA, HIGH);
    digitalWrite(enB, HIGH);

    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);

    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);

    delay(1000);

    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);

    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);
    //strcpy(receivedChars, "");

    for(int j = 0; j < numChars; j++)
      receivedChars[j] = '\n';
  }

  newData = false;

  /*

 digitalWrite (in1,LOW);
 digitalWrite (in2,HIGH);
  // low - high merge inainte
  // high - low merge inapoi

 digitalWrite (in3,HIGH);
 digitalWrite (in4,LOW);

 digitalWrite(enAb, HIGH);
 digitalWrite(enBb, HIGH);

 digitalWrite (in1b,LOW);
 digitalWrite (in2b,HIGH);
 digitalWrite (in3b,HIGH);
 digitalWrite (in4b,LOW);
 delay(1000);
 
 digitalWrite (in1,HIGH);
 digitalWrite (in2,LOW);
 digitalWrite (in3,LOW);
 digitalWrite (in4,HIGH);
 
 digitalWrite (in1b,LOW);
 digitalWrite (in2b,HIGH);
 digitalWrite (in3b,HIGH);
 digitalWrite (in4b,LOW);
 delay(1000);
 */
 
  
}
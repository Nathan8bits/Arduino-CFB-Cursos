*ideia de formatação*: adicione um sumário com os conteúdos usados no código 

## Circuito com potenciômetro, botão e ledRGB
![[circuitoComLedRBGPotenciometro.jpg]]

## Código
```cpp
// C++ code
//
int ledPino[4] = {11, 7, 2, 4};

#define pot A5
#define red 6
#define blue 5
#define green 3

#define ledR 8
#define ledG 9
#define ledB 10
#define btn 12

int ciclo = 0;  
int cor[3] = {0, 0, 0};

void verificarPotencia(int x) {  
  
  for(int i = 0; i < x; i++) {
    digitalWrite(ledPino[i], HIGH);
  }
  
  for(int i = x; i < 4; i++){
    digitalWrite(ledPino[i], LOW);
  }
}

void verificarBtn() {
  //HIGH == 1
  if(digitalRead(btn) == HIGH) {
    cor[ciclo] = analogRead(pot);
    ciclo++;
    
    Serial.println("###################");
  	Serial.println(ciclo);
  	Serial.println("####################");
  }
  
  if(ciclo > 2) {
   ciclo = 0; 
  }
  //delay(5000);
  
}

void verificarCiclo() {
  switch (ciclo)  {
    case 0:
     digitalWrite(ledR, HIGH);
     digitalWrite(ledG, LOW);
     digitalWrite(ledB, LOW);
     break;
    case 1:
     digitalWrite(ledR, LOW);
     digitalWrite(ledG, HIGH);
     digitalWrite(ledB, LOW);
     break;
    case 2:
     digitalWrite(ledR, LOW);
     digitalWrite(ledG, LOW);
     digitalWrite(ledB, HIGH);
     break;
  }
}

void corLed() {
  analogWrite(red, cor[0]);
  analogWrite(green, cor[1]);
  analogWrite(blue, cor[2]);  
}

void setup()
{
  pinMode(red, OUTPUT);
  pinMode(green, OUTPUT);
  pinMode(blue, OUTPUT);
  
  pinMode(btn, INPUT);
  pinMode(pot, INPUT);
  
  pinMode(ledR, OUTPUT);
  pinMode(ledG, OUTPUT);
  pinMode(ledB, OUTPUT);
  
  for(int i =0; i<4; i++){
    pinMode(ledPino[i], OUTPUT);
  }
  Serial.begin(20000);
  
}

void loop()
{  
  Serial.println(analogRead(pot));
   
  verificarBtn();
  verificarCiclo();
  verificarPotencia(map(analogRead(pot), 0, 1023, 0, 4));
  
  Serial.println(cor[0]);
  Serial.println(cor[1]);
  Serial.println(cor[2]);
  Serial.println("-----------------");
  
  corLed();
  //delay(5000);
}
```



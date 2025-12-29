
## Circuito:

![[ledRGBComClasses.jpg]]

## Código:

```cpp
/* SEM CLASSE

//led com catodo em comum, catodo ligado no ground
#define red 3
#define blue 5
#define green 6
#define btn 8
#define maximo 3


int btnClicado = 0;
int btnLiberado = 0;
int ciclo = 0;

void vermelho(){
 digitalWrite(red, HIGH); //HIGH == 1, LOW == 0
 digitalWrite(green, LOW);
 digitalWrite(blue, LOW);
}

void verde(){
 digitalWrite(red, LOW); //HIGH == 1, LOW == 0
 digitalWrite(green, HIGH);
 digitalWrite(blue, LOW);
}

void azul(){
 digitalWrite(red, LOW); //HIGH == 1, LOW == 0
 digitalWrite(green, LOW);
 digitalWrite(blue, HIGH);
}

void trocaLed() {
  switch (ciclo) {
   case 0:
    vermelho();
    break;
    
   case 1:
    verde();
    break;
    
   case 2:
    azul();
    break;
  }
  
  ciclo++;
  if(ciclo > maximo - 1) {
   ciclo = 0; 
  }
}

void verificaBtn() {
  if(digitalRead(btn) == HIGH) {
    btnClicado = 1;
    btnLiberado = 0;
  } else {
   btnLiberado = 1; 
  }
  
  if((btnClicado == 1) and (btnLiberado ==1)) {
    btnClicado = 0;
    btnLiberado = 0;
    trocaLed();
  }
}

void setup()
{
  pinMode(red, OUTPUT);
  pinMode(green, OUTPUT);
  pinMode(blue, OUTPUT);
  pinMode(btn, INPUT);
}

void loop()
{
  verificaBtn();
}
*/



// COM CLASSE

#define red 3
#define blue 5
#define green 6
#define btn 8

class Btn {
  public: 
  	int btnClicado, btnLiberado, pino;
  	
    Btn(int p){
     pino = p;
     btnClicado = btnLiberado = 0;
    }
    
    bool press() {
     if(digitalRead(pino) == HIGH) {
       btnClicado = 1;
       btnLiberado = 0;
     } else { 
       btnLiberado = 1;
     }
    
     if ((btnClicado == 1) and (btnLiberado == 1)) {
       btnClicado = 0;
       btnLiberado = 0;
      
       return true;
     } else {
       return false;
     } 
   }
};

class Cor {
 public:
  int pinoRed, pinoGreen, pinoBlue, ciclo, maximo;
  
  //lista de inicialização
  Cor (int r, int g, int b): pinoRed(r), pinoGreen(g), pinoBlue(b) {
    ciclo = 0;
    maximo = 3;
  }
  
  void trocaLed() {
    switch (ciclo) {
   	 case 0:
      corLed(1, 0, 0); //red
      break;
    
     case 1:
      corLed(0, 1, 0);//verde
      break;
    
     case 2:
      corLed(0, 0, 1);
      break;
    }
  
    ciclo++;
    if(ciclo > maximo - 1) {
     ciclo = 0; 
    }
  }
  
private: 
  void corLed(int r, int g, int b) {
   digitalWrite(red, r); //HIGH == 1
   digitalWrite(green, g);
   digitalWrite(blue, b);
  }
  
};

Btn botao(btn); //instanciando btn
Cor cor(red, green, blue);

void setup() {
  pinMode(red, OUTPUT);
  pinMode(green, OUTPUT);
  pinMode(blue, OUTPUT);
  pinMode(btn, INPUT);
}

void loop() {
  if(botao.press()) {
    cor.trocaLed();
  }
}
```

**Obs**: A função *'verificarBtn'* usa as variáveis *'btnClicado'* e *'btnLiberado'* para determinar se o botão foi clicado ou pressionado, podendo chamar funções diferentes para cada evento. Recomendo o uso de uma função semelhante para lidar com botões.
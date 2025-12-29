# Aula 1: Introdução

![[arduino2.jpg]]

site Tinkercad para desenvolvimento web.

programa Arduino para desenvolver e mover códigos para a placa arduino.

# Aula 2: Primeiros Comandos do Arduino

**obs:** A porta 13 tem um led próprio.

* **setup()**: é executado a primeira vez que o programa inicia. Configurações, iniciar variáveis e definir portas para entrada e saída;
* **loop()**: roda em loop enquanto o Arduino estiver ligado. O botão Reset executa o método setup() novamente;
* **Sinal Digital**: 1 ou 0, uma onda quadrada; (HIGH/ LOW)

## primeiros comandos
* **pinMode()**: define se um pino será de saída ou entrada;
* **digitalWrite()**: valor de saída para determinado pino;
* **delay()**: espera em milisegundos;

```cpp title:primeirosPassos.cpp
void setup() {
  pinMode(13, OUTPUT); //numero da porta e se é entrada ou saida(INPUT/OUTPUT)
}

void loop() {
  digitalWrite(13, HIGH); //porta e o estado (HIGH, LOW)
  delay(2000); //dá uma espera em milisegundos
  digitalWrite(13, LOW);
  delay(2000);
}

```

# Aula 3: Declaração de variáveis

* declaração e atribuição de valores para variáveis globais fora do escopo das funções:
```cpp
int led=10; //declaracao global

void setup() {
  pinMode(led, OUTPUT);
}

void loop() {
  digitalWrite(led, HIGH);
  delay(2000);
  digitalWrite(led, LOW);
  delay(2000);
}
```

## Leds

* <mark style="background: #BBFABBA6;">Leds têm polaridade</mark>, ânodo (positivo, maior) e catodo(negativo, menor):
![[led.jpg]]



### Montagem do circuito com led:

![[montagemLed.jpg]]

**obs**: resistores não têm polaridade, podendo ser conectado em qualquer polo do led.

### Assuntos Relacionados:
* [[Lei de ohm]]


# Aula 4: define e funcões

* **'#Define':** é diretiva de compilação. Substitui o nome da variável pelo valor após a compilação, na geração do executável. Vantagem do uso de memória. Para <mark style="background: #CACFD9A6;">número de portas dê preferência ao uso do '#define'</mark>

* **Funções:** são trechos reutilizaveis de código.
## Semáforo
``` cpp
/*
int ledGreen = 10;
int ledYellow = 9;
int ledRed = 8;
*/
//utilize define ao inves de variaveis, pois ocupa muito espaço
//o define, durante a compilação, substitui o nome pelo valor
//dessa forma não ocupa espaço na memória pra armazenar os valores
#define ledGreen 8
#define ledYellow 9
#define ledRed 10

void ligarLed(int led);

void setup()
{
  pinMode(ledGreen, OUTPUT);
  pinMode(ledYellow, OUTPUT);
  pinMode(ledRed, OUTPUT);
}

void loop()
{
 ligarLed(ledRed);
  delay(1000);
 ligarLed(ledYellow);
  delay(1000);
 ligarLed(ledGreen);
  delay(1000);
}

void ligarLed(int led){
  switch (led) {
   case 10:
    digitalWrite(8, LOW);
    digitalWrite(led, HIGH);
    break;
   case 9:
    digitalWrite(10, LOW);
    digitalWrite(led, HIGH);
    break;
   case 8:
    digitalWrite(9, LOW);
    digitalWrite(led, HIGH);
    break;
  }
}
```


# Aula 5: portas PWM, método analogWrite, loop FOR

  *Portas PWM são entradas digitais que simulam portas analógicas alterando o comprimento da onda quadrada*. Podendo ler valores entre o HIGH (5v) e o LOW (0v), <mark style="background: #CACFD9A6;">no intervalo entre 0 e 255.</mark>

``` cpp
#define led 9
#define maximo 255
#define minimo 0

void setup()
{
  pinMode(led, OUTPUT);
}

void loop()
{
  for(int i=minimo; i<maximo; i++) {
    analogWrite(led, i);
    //digitalWrite(led, HIGH);
    delay(100);
  }
  
   for(int i=maximo; i>minimo; i--) {
    analogWrite(led, i);
    delay(100);
  }
  
}
```


# Aula 6: Lendo portas digitais, digitalRead, pushButtom

## PushButtom
![[pushbuttom.jpg]]


### Circuitos com o pushButtom

![[circuitoPushButtom.jpg]]

![[circuitoLedWithPushButtom.jpg]]
obs: esse buttom está com resistor em pull down

# Aula 7: Resistor Pull Down, Resistor Pull Up

## Resistor em Pull Down
![[resistorPullDown.jpg]]
    Enquanto estiver pressionado manda 5V para a entrada do Arduino.
Sem um resistor conectado ao negativo não será possível saber quando o botão for liberado, pois ele não estará recebendo 0V, na verdade estará recebendo um valor nulo.

## Resistor em Pull Up
![[pullDownEPullUp.jpg]]
    Em Pull Up ocorre o contrário, enquanto estiver pressionado envia 0v.

# Aula 8: Led RGB, Módulo Led RGB

## Conteúdos Anexos:
*  [[Circuito com Potenciômetro e led RGB]]

## Led RGB

![[ledRGB.jpg]]
     O led RGB tem um pino para cada cor e um para o GND (negativo).

Defina cada pino de cor como OUTPUT e use o analogWrite ou digitalWrite para passar o valor da intensidade.  A combinação desses valores gera as demais cores.

# Aula 9: Led RGB Com Classes

## Conteúdos Anexos:
*  [[Leds RGB com  Classes]]

## Classes em c++

Utilize a estrutura padrão de uma classe

```cpp
class Btn {
	public: 
		int btnCLicado, btnLiberado, pino;
		
	Btn(int p) {
		pino = p;
		btnClicado = btnLiberado = 0;
	}
	
	bool press() {
		//...
	}
};
```

```cpp
class Cor{
	public:
		int pinoRed, pinoGreen, pinoBlue, ciclo, maximo;
		
	//lista de inicialização
	Cor (int r, int g, int b): pinoRed(r), pinoGreen(g), pinoBlue(b) {

		ciclo = 0;
		maximo = 3;
	}
	
	void trocarLed() {
		//...
	}
	
	private:
		void corLed(int r, int g, int b){
			//...
		}
};
```

# Aula 10: Portas analógicas

  O arduino possui portas de entrada analógicas.

![[ondasAnalogicasEDigitais.jpg]]

* **Onda analógica**: varia entre 0V e 5v, entre 0 e 1023. Seguindo a seguinte conversão:
*![[conversaoPraVoltsEntradaAnalogica.jpg]]
* **Onda Digital**: 0 ou 1, 0V ou 5V;

**Obs**: *Portas PWM são entradas digitais que simulam portas analógicas alterando o comprimento da onda quadrada*. Variam entre 0 e 255 (0V a 5V).

Exemplo com leitura de potenciômetro:
![[lendoUmPotenciometro.jpg]]

```cpp
#define an5 A5
void setup() {
	pinMode(an5, INPUT); //portas analogicas são de entrada
	Serial.begin(9600); //definir a saida serial do arduino, o parâmetro é a velocidade
}

void loop() {
    //Serial.println para exibir
    //analogRead para ler uma entrada analogica
	Serial.println( 
		analogRead(an5));
	delay(100);
}


```

# Aula 11: função Map

A função *Map()* fornece o valor y contido em um intervalo determinado, correspondente a um valor x determinado e contido em outro intervalo também determinado.

Seus parâmetros:
* map(valor, min_entrada, max_entrada, min_saida, max_saida)

## Exemplo 1: led e potenciômetro
![[aula11circuito1.jpg]]

```cpp
#define led 3
#define pot A0

void setup() {
	pinMode(let, OUTPUT);
	pinMode(pot, INPUT);
}

void loop(){
	//analigico => 0 a 1023
	//PWM => 0 a 255
	//analogWrite(led,analogRead(pot)/4);
	analogWrite(led, map(analogRead(pot), 0, 1023,0, 255))
	/*Sintaxe: map(leitura, 
		min_val_entrada, max_val_entrada, 
		min_val_saida, max_val_saida)
	*/
}
```

Veja também o segundo exemplo de uso da função map: [[Aula 11 exemplo 2]]

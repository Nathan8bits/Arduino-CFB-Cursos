## Circuito 1
![[aula11exem2FuncaoMap.jpg]]

## Circuito 2:
![[aula11exem2FuncaoMapCircuito2.jpg]]

Os dois circuitos estão corretos, com a diferença sendo apenas a quantidade de jumpers e resistores.

Código:

```cpp
int leds[] = {3, 4, 5, 6, 7, 8};
#define pot A0
int val;

void setup()
{
  for(int i = 0; i < 6; i++) {
    pinMode(leds[i], OUTPUT);
  }
  pinMode(pot, INPUT);
}

void acender(int x) {
  for(int i = 0; i < x; i++) {
    digitalWrite(leds[i], HIGH);
  }
  
  for(int i = x; i < 6; i++) {
    digitalWrite(leds[i], LOW);
  }
}

void loop()
{	
	acender(map(analogRead(pot), 0, 1023, 0, 6));
}
```
#define msjluz "Luz: "
#define msjtemp "Temp: "
#define grados "°C"

const int pin_tpm = A0;
const int pin_ldr = A1;
  
const int led_rojo = 2;
const int led_azul = 3;
const int led_verde = 4;

void setup() {
  pinMode(pin_tpm, INPUT);
  pinMode(pin_ldr, INPUT);
  
  pinMode(led_rojo, OUTPUT);
  pinMode(led_azul, OUTPUT);
  pinMode(led_verde, OUTPUT);
  
  Serial.begin(9600);
}

void loop() {
  int valorluz = analogRead(pin_ldr);
  int valortemp = analogRead(pin_tpm);
  
 
  int porcentajeluz = map(valorluz, 0, 1023, 0, 100);
  
  float voltaje = valortemp * 5.0 / 1023.0;
  float temperatura = (voltaje - 0.5) * 100;
  
  Serial.print(msjluz);
  Serial.print(porcentajeluz);
  Serial.println("%");

  Serial.print(msjtemp);
  Serial.print(temperatura);
  Serial.println(grados);
  
  
  digitalWrite(led_rojo, LOW);
  digitalWrite(led_azul, LOW);
  digitalWrite(led_verde, LOW);
  
 
  if (porcentajeluz >= 30 && porcentajeluz <= 70) {
    if (temperatura > 90) {
      digitalWrite(led_rojo, HIGH);
    } else if (temperatura < 18) {
      digitalWrite(led_azul, HIGH);
    } else {
      digitalWrite(led_verde, HIGH);
    }
  }
  
  delay(100);
}

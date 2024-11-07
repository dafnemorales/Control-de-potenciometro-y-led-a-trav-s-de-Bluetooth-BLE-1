# Control-de-potenciometro-y-led-a-trav-s-de-Bluetooth-BLE-1 
Para conocer el funcionamiento de Bluetooth BLE, se hizo uso del ESP32 y otros componentes electronicos para leer valores analógicos y convertirlos a digitales a través de una aplicacion. Para esto, se realizaron varios objetivos, los cuales implementan funciones para comprobar el funcionamiento del sistema completo.

Parte 1: Monitoreo de Voltaje a través del Monitor Serial
Configurando el pin de señal como entrada analógica (INPUT) y realizando la lectura de voltaje utilizando el ADC interno del ESP32. Los valores de lectura estarán en el rango de 0 a 4095, los cuales deben ser convertidos a un rango de 0 a 3.3V para visualizar correctamente el voltaje. Este proceso de conversión permitirá detectar los valores de voltaje y graficar la variación en tiempo real en el monitor serial.

Código - parte 1:

const int Pot=35;
int Signal = 0;
float voltaje = 0.0;

void setup() {
  Serial.begin(115200);
} 

void loop(){
  Signal=analogRead(Pot);
  voltaje = Signal*3.3/4095;

  Serial.printIn(voltaje);  //Imprime el valor leído y el voltaje calculado
  
delay(500); 


Código - parte 2:


const int ledPin= 4; //definición del pin del led

void setup() {
  pinMode(ledPin, OUTPUT); //pin de LED como salida
  Serial.begin(9600);  //
  Serial.printIn("Escribe s para encender el LED o n para apagarlo")

}

void loop() {
  if (Serial.aviable() > 0) {
    char dato = Serial.read ();  //leer dato del puerto serial

    if (dato == 'S'){
      digitalWrite(ledPin, HIGH); // enciende led
      Serial.printIn(" Led encendido ");
    }
    
    else if (dato == 'N'){
      digitalWrite(ledPin, LOW); // apaga led 
    }
  }
}

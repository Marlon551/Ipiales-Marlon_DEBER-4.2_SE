# Ipiales-Marlon_DEBER-4.2_SE
Ipiales Marlon_DEBER 4.2_SE
/*
*CAPITULO V: PERIFERICOS ESPECIALES
*CODIGO 16: MCAD y SERVO
*OBJETIVO: Activar juego de leds por medio de la interrupcion 0 y la seleccion del numero de veces a jugar se realizara con la otra interrupcion 1 
*NOMBRE: Marlon Ipiales 
*FUNCIONES: interrup 0: Inicio del sistema e ingreso de veces del juego
*                  Inicio de juego
*                  Fin de juego
*           interrup 1: Contador
*           attachInterrupt(interrump,rutina, modo)
*NOTA: Para que el codigo compile debe estar seleccionado con Arduino Uno WiFi caso contrario si no funcionara seleccionar Arduino Uno, en caso de que no compile el codigo debe guardarlo y luego compilarlo verias veces
*/
const int leds[6]={13,12,11,10,9,8};
int on=0;      //int0
int cont;     //int1
int i;        //Variable de conteo 
int j=0;     //Variable de conteo  

void setup() {
  for(i=0;i<6;i++){          //Configuracion de los leds
    pinMode(leds[i],OUTPUT); //
  }
  i=0;
  Serial.begin(9600);           //Activacion de la comunicacion serial 
  attachInterrupt(0,activacion,LOW);    //Interrupt 0 habilitada
  attachInterrupt(1,contador,LOW);      //Interrump 1 habilitada
}

void loop() {
  if(on==2){
    for(;i<cont;i++){
      for(j=0;j<6;j++){
        digitalWrite(leds[j],HIGH);
        delay(200);
        digitalWrite(leds[j],LOW);
        delay(200);
      }
    }
  }

}

void activacion(){
  switch(on){        //Opciones de los botones a definor
  case 0:
   Serial.println("Inicio del sistema");
   Serial.println("Ingrese el numero de veces que desee jugar");
   //on++;
  break;
  case 1:
    Serial.println("Inicio de juego");
    on++;
  break;
  case 2:
    Serial.println("Fin de juego");
    cont=0; 
    on=0;
    i=0;
  break;
  }
}

void contador(){
  if(on=1){
    cont++;
    Serial.println(String("Juega ")+String(cont)+String(" Veces"));
  }
}

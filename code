// Sensor ultrassônico
#define TRIG_PIN 2  
#define ECHO_PIN 3  

// Buzzer
#define BUZZER_PIN 4  

// Chaves de controle
#define CHAVE1_LED 5
#define CHAVE1_PIN 6  
#define CHAVE2_PIN 7  
#define CHAVE2_LED 8

// LEDs de indicação de distância
#define LED_DIST1_PIN 9   
#define LED_DIST2_PIN 10  
#define LED_DIST3_PIN 11  
#define LED_DIST4_PIN 12  
#define LED_DIST5_PIN 13  

void setup() {
  Serial.begin(9600);

  // HC-SR04
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);

  // Buzzer
  pinMode(BUZZER_PIN, OUTPUT);

  // Chaves (pull-up interno)
  pinMode(CHAVE1_PIN, INPUT);
  pinMode(CHAVE1_LED, OUTPUT);
  pinMode(CHAVE2_PIN, INPUT);
  pinMode(CHAVE2_LED, OUTPUT);

  // LEDs de distância
  pinMode(LED_DIST1_PIN, OUTPUT);
  pinMode(LED_DIST2_PIN, OUTPUT);
  pinMode(LED_DIST3_PIN, OUTPUT);
  pinMode(LED_DIST4_PIN, OUTPUT);
  pinMode(LED_DIST5_PIN, OUTPUT);
}

float lerDistanciaCM() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  long duracao = pulseIn(ECHO_PIN, HIGH);
  float distancia = duracao * 0.034 / 2.0;
  return (distancia < 0) ? 0 : distancia;
}

void desligarSistema() {
  digitalWrite(LED_DIST1_PIN, LOW);
  digitalWrite(LED_DIST2_PIN, LOW);
  digitalWrite(LED_DIST3_PIN, LOW);
  digitalWrite(LED_DIST4_PIN, LOW);
  digitalWrite(LED_DIST5_PIN, LOW);
  noTone(BUZZER_PIN);
}

void desligarTodosLeds() {
  digitalWrite(LED_DIST1_PIN, LOW);
  digitalWrite(LED_DIST2_PIN, LOW);
  digitalWrite(LED_DIST3_PIN, LOW);
  digitalWrite(LED_DIST4_PIN, LOW);
  digitalWrite(LED_DIST5_PIN, LOW);
}

void ligarLeds123() {
  digitalWrite(LED_DIST1_PIN, HIGH);
  digitalWrite(LED_DIST2_PIN, HIGH);
  digitalWrite(LED_DIST3_PIN, HIGH);
  digitalWrite(LED_DIST4_PIN, LOW);
  digitalWrite(LED_DIST5_PIN, LOW);
}

void ligarLeds1234() {
  digitalWrite(LED_DIST1_PIN, HIGH);
  digitalWrite(LED_DIST2_PIN, HIGH);
  digitalWrite(LED_DIST3_PIN, HIGH);
  digitalWrite(LED_DIST4_PIN, HIGH);
  digitalWrite(LED_DIST5_PIN, LOW);
}

void ligarLeds12345() {
  digitalWrite(LED_DIST1_PIN, HIGH);
  digitalWrite(LED_DIST2_PIN, HIGH);
  digitalWrite(LED_DIST3_PIN, HIGH);
  digitalWrite(LED_DIST4_PIN, HIGH);
  digitalWrite(LED_DIST5_PIN, HIGH);
}

void loop() {
  // 1) Leitura das chaves (fechada→LOW, aberta→HIGH)
  int chave1 = digitalRead(CHAVE1_PIN);
  int chave2 = digitalRead(CHAVE2_PIN);

  float distancia = lerDistanciaCM();
  Serial.print("Distancia: ");
  Serial.print(distancia);
  Serial.println(" cm");

  // Ambas chaves desligadas → desliga tudo
  if (chave1 == LOW && chave2 == LOW) {
    desligarSistema();
    digitalWrite(CHAVE1_LED, LOW);
    digitalWrite(CHAVE2_LED, LOW);
    return;
  }

  // Ambas chaves ligadas → indica ambas e controla buzzer + LEDs de distância
  if (chave1 == HIGH && chave2 == HIGH) {
    digitalWrite(CHAVE1_LED, HIGH);
    digitalWrite(CHAVE2_LED, HIGH);

    // garanta que o buzzer comece desligado
    noTone(BUZZER_PIN);

    if (distancia >= 400.0) {
      desligarTodosLeds();
      noTone(BUZZER_PIN);
    }
    else if (distancia >= 200.0) {
      ligarLeds123();
      tone(BUZZER_PIN, 440);   // 440 Hz para frequência mais baixa
      delay(900);
      noTone(BUZZER_PIN);
      desligarTodosLeds();
    }
    else if (distancia >= 100.0) {
      ligarLeds1234();
      tone(BUZZER_PIN, 880);   // 880 Hz para frequência mais alta
      delay(600);
      noTone(BUZZER_PIN);
      desligarTodosLeds();
    }
    else {
      ligarLeds12345();
      tone(BUZZER_PIN, 880);   // tom contínuo
    }
  }


if ((chave1 == HIGH && chave2 == LOW) || (chave1 == LOW && chave2 == HIGH)) {
  // reflete estado das chaves nos LEDs
  digitalWrite(CHAVE1_LED, chave1);
  digitalWrite(CHAVE2_LED, chave2);

  // desliga o buzzer corretamente
  noTone(BUZZER_PIN);

  if (distancia >= 400.0) {
    desligarTodosLeds();
  }
  else if (distancia >= 200.0) {
    ligarLeds123();
    delay(900);
    desligarTodosLeds();
  }
  else if (distancia >= 100.0) {
    ligarLeds1234();
    delay(600);
    desligarTodosLeds();
  }
  else {
    ligarLeds12345();
  }
}
  // Aguarda 200ms antes da próxima leitura
  delay(200);
}

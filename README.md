Este projeto implementa um sistema de monitoramento e controle utilizando Arduino e sensor ultrassônico HC-SR04 para detectar a presença de objetos em diferentes faixas de distância, acionando alertas visuais (LEDs) e sonoros (buzzer) conforme especificado no enunciado da disciplina de Arquitetura de Computadores (Prof. Clayton J A Silva).

Funcionalidades:

Detecção de distância exibida em tempo real via Monitor Serial


Alertas visuais e sonoros configurados para quatro faixas de distância:

4 m: sem alerta

2–4 m: três LEDs piscando com buzzer intermitente a 440 Hz

1–2 m: quatro LEDs piscando com buzzer intermitente a 880 Hz

< 1 m: cinco LEDs acesos continuamente com buzzer contínuo


Configuração via jumpers:

00: sistema desligado

01 / 10: alerta somente visual (som desativado)

11: operação normal
  

Materiais:

Arduino (Uno, Nano etc.)

Sensor ultrassônico HC-SR04

Buzzer piezoelétrico

Oito LEDs (cinco para indicação de distância, dois para jumpers e um opcional)

Jumpers e protoboard com fios de conexão


Conexões de Pinos:

TRIG (HC-SR04) — pino 2

ECHO (HC-SR04) — pino 3

Buzzer — pino 4

LED dos jumpers (CHAVE1_LED) — pino 5

Jumper 1 (CHAVE1) — pino 6

Jumper 2 (CHAVE2) — pino 7

LED dos jumpers (CHAVE2_LED) — pino 8

LED de distância 1 (2–4 m) — pino 9

LED de distância 2 (2–4 m) — pino 10

LED de distância 3 (2–4 m) — pino 11

LED de distância 4 (1–2 m) — pino 12

LED de distância 5 (<1 m) — pino 13


Estrutura do Código:

setup(): configura pinos e inicializa comunicação serial

lerDistanciaCM(): dispara o sensor e calcula a distância em cm

Funções de controle de LEDs:

desligarSistema()

desligarTodosLeds()

ligarLeds123()

ligarLeds1234()

ligarLeds12345()

loop(): lê o estado dos jumpers, obtém a distância e aplica a lógica de alertas



Disciplina: Arquitetura de Computadores – Prof. Clayton J A Silva

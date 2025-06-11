# RETROWAVE

## Table of Contents
1. About
2. Getting Started
   2.1 Prerequisites
   2.2. Installation
   2.3 Usage
3. 
4. Contributors


## 1. About

O projeto RetroWave consiste na criação de dois objetos distintos, com a intenção de serem inseridos numa instalação artística interativa. 
Estes são uma reinterpretação de duas peças tecnológicas já existentes: Um leitor de cassetes e um  lava lamp.

## 2. Getting Started
# 2.1 Prerequisites
Software:
- Arduino IDE (com suporte ESP32)
- Processing IDE
- MQTT Broker (ex: HiveMQ público)

Lava lamp:
- Arduino IDE: v2.2.1 ou superior

- Biblioteca Adafruit NeoPixel: v1.11.0

Lista de Materiais:
1x	            Placa Arduino Uno
1x	            Sensor Ultrassônico HC-SR04
1x	            Fita de LED WS2812B (30 LEDs)
1x	            Fonte de alimentação 5V 2A
Vários	      Cabos Jumper
1x	            Breadboard

Leitor de cassetes:
- Hardware ESP32 DevKit Leitor NFC MFRC522 2 ou mais tags NFC com UIDs únicos Botão físico Jumpers, protoboard Acesso à rede WiFi

- Software Arduino IDE (com suporte ESP32) Processing IDE MQTT Broker (ex: HiveMQ público)

- Bibliotecas Arduino MFRC522 WiFi (nativa no ESP32) PubSubClient

- Bibliotecas Processing MQTT Sound

Lista de Materiais:
1x   ESP32 DevKit
1x   Leitor NFC MFRC522
Várias tags NFC com UIDs únicos
1x   Botão físico
Vários  Jumpers, protoboard



# 2.2 Installation
Instale via Arduino IDE → Ferramentas → Gerenciar Bibliotecas

Lava lamp:
Construa o circuito conforme presente no repositório
Instale a biblioteca Adafruit NeoPixel v1.11.0
Copie o código-fonte para o Arduino IDE
Compile e faça o upload para o Arduino Uno
Abra o Monitor Serial para visualizar a leitura da distância

Leitor de cassetes:
Parte 1 — ESP32
- Instale as bibliotecas no Arduino IDE:
   MFRC522
   PubSubClient

- Faça o upload do código para o ESP32.

- Substitua as credenciais WiFi no código (SSID e password).

- Abra o Monitor Serial e aproxime tags NFC para testar os UIDs e publicações MQTT.

Parte 2 — Processing
- Crie uma pasta (ex: LeitorCasseteProcessing/) com:

LeitorCasseteProcessing/
├── leitor_processing.pde
├── toxic.mp3
├── babe.mp3

- Instale as bibliotecas via Sketch > Import Library > Add Library...:
   Sound
   MQTT

- No código .pde, edite os UIDs reais das suas tags:
   String n = "4EB79AD6A2681";
   String n2 = "4C279AD6A2681";




# 2.3 Usage
Lava Lamp:
- Ligações do Circuito

<img width="850" src="https://github.com/ClaraAriGomes/TI-Retrowave/blob/main/circuito_lamp.png">

> A fonte externa de 5V precisa fornecer pelo menos 2A. O GND da fonte deve estar ligado ao GND do Arduino.

- Como Funciona
    - Inicialização
        Define os pinos e inicia a comunicação Serial
    - Leitura do Sensor
        Mede distância via pulso de ultrassom

    - Processamento de Dados
        Distância entre 25cm e 200cm afeta LEDs
        Cor calculada em HSV → convertida para RGB

    - Saída Visual
        Mais perto: mais LEDs + mistura de cor
        Mais longe: menos LEDs + cor pura

- Environment Variables
    Este projeto não utiliza variáveis de ambiente. Porém, o código pode ser adaptado para aceitar parâmetros externos futuramente.

    Código de Exemplo:

digitalWrite(trigPin, LOW);
delayMicroseconds(3);
digitalWrite(trigPin, HIGH);
delayMicroseconds(12);
digitalWrite(trigPin, LOW);

duration = pulseIn(echoPin, HIGH);
distance = (duration * 0.034) / 2;

int activeLEDs = map(distance, 200, 25, 0, numPixels);
int mixAmount = map(distance, 200, 25, 0, 255);

Leitor de cassetes:
- Ligações do Circuito

<img width="850" src="https://github.com/ClaraAriGomes/TI-Retrowave/blob/main/circuito.png">

## Nunca conecte o MFRC522 ao 5V
Conexão do Botão
Um pino: GPIO 14
Outro: GND

# Teste Completo
Construa o circuito conforme presente no repositório
Execute o sketch no Processing
Ligue o ESP32 e abra o Monitor Serial
Aproxime uma tag NFC → toca uma música específica e inicia visualização
Troque de tag → muda a música
Pressione o botão → a música para



# Dicas de Depuração
Verifique arquivos .mp3 na pasta correta
Confira SSID e senha WiFi
Use println(code) no Processing para ver se o UID está sendo recebido
Use ferramentas como MQTT Explorer para monitorar tópicos e mensagens

# Broker MQTT
Broker: broker.hivemq.com
Porta: 1883
Tópico: leitor

## 3.Credits
- Desenvolvido no âmbito da unidade curricular do Mestrado em Design e Multimédia da Universidade de Coimbra

- Biblioteca: Adafruit NeoPixel

- Biblioteca MFRC522 por Miguel Balboa
- Biblioteca PubSubClient por Nick O’Leary
- Broker público: HiveMQ
- Bibliotecas Processing: Sound, MQTT (StudioSAVSoft)





---

## 4. Contributors
Carolina Travanca, Clara Gomes, Flávia Simões - MDM

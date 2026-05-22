# 🌡️ Sistema IoT — Monitoramento de Temperatura e Umidade

> Projeto Integrador | ESP32 + DHT22 + MicroPython + Wokwi

-----

## 📋 Descrição

Sistema de Internet das Coisas (IoT) para monitoramento ambiental em tempo real. O sensor DHT22, conectado ao microcontrolador ESP32 e programado em MicroPython, realiza leituras periódicas de temperatura e umidade. Os dados são exibidos no terminal serial e armazenados em um arquivo CSV para análise histórica.

O projeto foi desenvolvido e simulado no ambiente **Wokwi**, sem necessidade de hardware físico.

-----

## 🛠️ Tecnologias Utilizadas

|Tecnologia |Função                                           |
|-----------|-------------------------------------------------|
|ESP32      |Microcontrolador principal — processa os dados   |
|DHT22      |Sensor de temperatura (-40°C a 80°C) e umidade   |
|MicroPython|Linguagem de programação para o ESP32            |
|Wokwi      |Simulador online de circuitos eletrônicos        |
|CSV        |Formato de armazenamento do histórico de leituras|
|GitHub     |Versionamento e documentação do projeto          |

-----

## ✅ Funcionalidades

- [x] Leitura de temperatura em graus Celsius (°C)
- [x] Leitura de umidade relativa (%)
- [x] Exibição dos dados no terminal serial a cada 10 segundos
- [x] Armazenamento automático em arquivo `dados.csv` com data e hora
- [x] Simulação completa no Wokwi sem hardware físico

-----

## 📁 Estrutura do Projeto

```
iot-temperatura-umidade/
│
├── main.py          # Código principal — loop de leitura e exibição
├── csv_logger.py    # Módulo de armazenamento em CSV
├── diagram.json     # Circuito do Wokwi (ESP32 + DHT22)
├── dados.csv        # Exemplo de dados coletados
├── docs/
│   ├── Relatorio_Academico_IoT.md
│   └── Apresentacao_IoT_DHT22_ESP32.pptx
└── README.md
```

-----

## ⚡ Como Executar no Wokwi

1. Acesse <https://wokwi.com>
1. Crie um novo projeto ESP32 com MicroPython
1. Copie o conteúdo de `diagram.json` para o circuito
1. Copie os arquivos `main.py` e `csv_logger.py` para o editor
1. Clique em **▶ Run** e observe o terminal serial

-----

## 🔌 Circuito — Conexões

|Pino DHT22|Pino ESP32|
|----------|----------|
|VCC       |3.3V      |
|GND       |GND       |
|DATA      |GPIO 4    |


> ⚠️ Adicione um resistor pull-up de **10kΩ** entre DATA e VCC.

-----

## 🐍 Código Principal

```python
import dht
import machine
import utime
import csv_logger

sensor = dht.DHT22(machine.Pin(4))

print("Sistema IoT iniciado!")

while True:
    sensor.measure()
    temperatura = sensor.temperature()
    umidade = sensor.humidity()
    
    print(f"Temperatura: {temperatura}°C | Umidade: {umidade}%")
    csv_logger.salvar(temperatura, umidade)
    
    utime.sleep(10)
```

-----

## 📊 Exemplo de Saída — Terminal Serial

```
Sistema IoT iniciado!
Monitorando temperatura e umidade...

Temperatura: 24.3°C | Umidade: 62.1%
Temperatura: 24.7°C | Umidade: 61.5%
Temperatura: 25.1°C | Umidade: 60.8%
```

-----

## 📄 Exemplo de Saída — Arquivo CSV (`dados.csv`)

```
2026-20-04 09:00:00,24.3,62.1
2026-14-04 06:00:10,24.7,61.5
2026-06-04 07:00:20,25.1,60.8
2026-05-05 13:10:30,25.4,60.2
```

> O arquivo CSV pode ser aberto diretamente no Excel ou Google Sheets para geração de gráficos e análises.

-----

## 👥 Integrantes

|Nome          |Função no Projeto                     |
|--------------|--------------------------------------|
|Luan          |Desenvolvimento do código MicroPython |
|Lauan         |Montagem e teste do circuito no Wokwi |
|Maria Fernanda|Documentação, relatório e apresentação|
|Simplicio     |Armazenamento CSV e análise dos dados |

-----

## 📚 Referências

- [Documentação MicroPython](https://docs.micropython.org)
- [ESP32 Datasheet — Espressif](https://www.espressif.com/en/products/socs/esp32)
- [DHT22 Datasheet — Aosong](https://aosong.com)
- [Wokwi Simulador](https://wokwi.com)

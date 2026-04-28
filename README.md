# 💡 Monitor de Luminosidade com Alerta Sonoro

<div align="center">

![Arduino](https://img.shields.io/badge/-Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![Status](https://img.shields.io/badge/Status-Finalizado-success?style=for-the-badge)

</div>

Este projeto utiliza um **Arduino Uno** para monitorar a luz ambiente através de um sensor LDR. O sistema categoriza a luminosidade em três estados (**OK, Alerta e Problema**), fornecendo feedback visual via LEDs coloridos e um alerta sonoro via Buzzer quando a luz atinge níveis críticos.

---

## 👥 Alunos / RMs
* **Kaick Lima Silva** - 574060
* **Gustavo Basso** - 572623
* **Guilherme Sales** - 572933
* **Pedro Feltrin Geraldes** - 569038
* **Guilherme Kozikoski Failla** - 571611

---

## 🛠️ Dependências e Componentes Hardware

| Qtd | Componente | Observação |
| :--- | :--- | :--- |
| 1 | Arduino Uno | Ou placa compatível |
| 1 | Sensor de Luz (LDR) | Sensor de entrada |
| 1 | Buzzer | Ativo ou Passivo |
| 3 | LEDs | Verde, Amarelo e Vermelho |
| 3 | Resistores 220 $\Omega$ | Para proteção dos LEDs |
| 1 | Resistor 10k $\Omega$ | Para o divisor de tensão do LDR |
| - | Protoboard e Jumpers | Para conexões físicas |

---

## 🔌 Esquema de Ligação (Pinagem)

* **LDR**: Pino **A0** (Conectado em divisor de tensão com resistor de 10k)
* **LED Verde**: Pino **13** (Indica estado OK)
* **LED Amarelo**: Pino **11** (Indica estado de ALERTA)
* **LED Vermelho**: Pino **10** (Indica estado de PROBLEMA)
* **Buzzer**: Pino **7** (Ativado no estado de PROBLEMA)

---

## 🚀 Como Reproduzir

### 1. Montagem do Hardware
1. **Conexão dos LEDs**: Conecte 3 jumpers nas pinagens **13** (Verde), **11** (Amarelo) e **10** (Vermelho). Leve-os até a protoboard.
2. **Polaridade**: Conecte os jumpers ao **Anodo** (lado positivo/maior) de cada LED.
3. **Resistência**: No **Cátodo** (lado negativo/menor), conecte os resistores de **220 $\Omega$** para limitar a corrente.
4. **GND**: A ponta restante do resistor deve ser conectada ao barramento negativo da protoboard, que por sua vez deve ser conectado a um pino **GND** do Arduino.
5. **Sensor LDR**: Conecte uma ponta do LDR ao **5V**. A outra ponta deve ser conectada a um resistor de **10k $\Omega$** (que vai ao GND). Na linha entre o LDR e o Resistor, conecte um jumper ao pino **A0**.
6. **Buzzer**: Conecte o terminal positivo ao pino **7** e o negativo ao barramento **GND**.

### 2. Montagem do Código
Abaixo está a estrutura lógica utilizada no projeto:

```cpp
// 1. Declaro as Variáveis para utilização em código: 
const int pinoLDR = A0;
const int ledVerde = 13;
const int ledAmarelo = 11;
const int ledVermelho = 10;
const int buzzer = 7;

// 2. Defino um valor para a Varíavel Luminosidade:
int luminosidade = 0;

// 3. Dentro do void setup, defino as Váriaveis e o buzzer como OUTPUT:
void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
  pinMode(buzzer, OUTPUT);
  Serial.begin(9600); 
}

// 4. Dentro do void loop, leio a luminosidade e printo no Serial:
void loop() {
  luminosidade = analogRead(A0);
  Serial.print("Valor da Luminosidade: ");
  Serial.println(luminosidade);

  // 5. Se a luminosidade estiver acima dos parâmetros (>830):
  if (luminosidade > 830) {
    // Estado: PROBLEMA
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarelo, LOW);
    digitalWrite(ledVermelho, HIGH);
    tone(buzzer, 3000); 
    delay(3000);
  } 
  // 6. Se estiver em estado de ALERTA (entre 400 e 830):
  else if (luminosidade >= 400 && luminosidade <= 830) {
    // Estado: ALERTA
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarelo, HIGH);
    digitalWrite(ledVermelho, LOW);
    noTone(buzzer);
  } 
  // 7. Caso contrário, estado OK:
  else {
    // Estado: OK
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledAmarelo, LOW);
    digitalWrite(ledVermelho, LOW);
    noTone(buzzer);
  }

  // Delay de 100 milissegundos para execução do código:
  delay(100);
}

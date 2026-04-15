Monitor de Luminosidade com Alerta Sonoro 💡📝 
---------------------------------------------------------------------------------------------------------------

Alunos / Rms
Kaick Lima Silva - 574060
Gustavo Basso - 572623
Guilherme Sales - 572933
Pedro Feltrin Geraldes - 569038
Guilherme Kozikoski Failla - 571611

---------------------------------------------------------------------------------------------------------------
Descrição:
---------------------------------------------------------------------------------------------------------------

Este projeto utiliza um Arduino Uno para monitorar a luz ambiente através de um sensor LDR. O sistema categoriza a luminosidade em três estados (OK, Alerta e Problema), fornecendo feedback visual via LEDs coloridos e um alerta sonoro via Buzzer quando a luz atinge níveis críticos.
É ideal para sistemas de automação residencial simples ou estudos de sensores analógicos.

---------------------------------------------------------------------------------------------------------------
🛠️ Dependências e Componentes Hardware
---------------------------------------------------------------------------------------------------------------

1x Arduino Uno (ou compatível)

1x Sensor de Luz (LDR)

1x Buzzer Ativo/Passivo

1x LED Verde

1x Amarelo

1x Vermelho

3x Resistores de 220 $\Omega$ (para os LEDs)

1x Resistor de 10k $\Omega$ (para o divisor de tensão do LDR)

Protoboard e Jumpers

SoftwareArduino IDE (para carregar o código).

Não são necessárias bibliotecas externas para este projeto (utiliza apenas funções nativas como analogRead e tone).

---------------------------------------------------------------------------------------------------------------
🔌 Esquema de Ligação (Pinagem)
---------------------------------------------------------------------------------------------------------------

Componente --- Pino --- Função/Observação

LDR  ---  A0 (Conectado em divisor de tensão com resistor de 10kLED)

LED Verde  ---  13 (Indica estado OK)

LED Amarelo --- 11 (indica estado de ALERTA)

LED Vermelho  ---  10 (Indica estado de PROBLEMA)

Buzzer  --  7 (Ativado no estado de PROBLEMA)

---------------------------------------------------------------------------------------------------------------
🚀 Como Reproduzir
---------------------------------------------------------------------------------------------------------------

Montagem do Hardware:

1. Deve-se conectar 3 jumpers nas pinagens 13(para o Verde), 11(para o Amarelo) e 10(para o Vermelho) do Arduino, e Puxá-las até o meio do protoboard, parte onde será feito o projeto.

2. conecta-se as pinagens anteriores aos seus respectivos Leds, onde deve-se atentar que a conecção é feita no Anodo(Lado positivo e Maior), e sempre na mesma linha onde tem a Escrita.

3. na mesma linha do Cátodo (Lado negativo e Menor), conecta-se resistores de 220 $\Omega$, para aguentar a corrente que irá passar pelo protoboard.

4.Na ponta que sobrar do Resistor, na mesma linha, irá puxar para o lado negativo do protoboard (Representado por -), do lado contrário ao Arduino.

5. Irá fazer a Conecção de um Jumper na mesma linha do lado negativo do protoboard (Em uma de suas Extremidades) e conecta-los a um GND (Fonte de Retorno da Corrente elétrica.)

6. Irá conectar uma das pontas do LDR a voltagem de 5V, e a outra a um resistor de 10k $\Omega$,(no qual na outra ponta do Resistor, deverá ser conectado a um GND). E na mesma linha que a conecção do LDR ao Resistor for feita, coloca-se uma conecção ao pino A0 utilizando um jumper.

7.Encaixa-se um jumper no Pino A7 do arduino, e faz a conecção ao Buzzer em seu sentido positivo. No sentido negativo, irá puxar-se um jumper para a mesma linha do lado negativo do protoboard, que fizerá a conecção do GND.

---------------------------------------------------------------------------------------------------------------
Montagem do Código:
---------------------------------------------------------------------------------------------------------------

## Declaro as Variáveis para utilização em código: 

° const int pinoLDR = A0;
° const int ledVerde = 13;
° const int ledAmarelo = 11;
° const int ledVermelho = 10;
° const int buzzer = 7;

## Defino um valor para a Varíavel Luminosidade, que será utilizado em conjunto ao LDR para ascender os leds e o buzzer:

int luminosidade = 0;

## Dentro do void setup, defino as Váriaveis e o buzzer como OUTPUT, sem contar o pinoldr:

void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
  pinMode(buzzer, OUTPUT);
  Serial.begin(9600); 
}

## Dentro do void loop, leio a luminosidade declarada no pino A0, e printo uma mensagem na tela com o valor atual de luminosidade:

void loop() {
  luminosidade = analogRead(A0);
  Serial.print("Valor da Luminosidade: ");
  Serial.println(luminosidade);

## Começo um If (Se) a luminosidade estiver acima dos paramêtros permitidos, onde irá ativar apenas o LedVermelho, e ativar o Buzzer por 3 segundos e esperar 3 segundos.

  if (luminosidade > 830) {
    // Estado: PROBLEMA
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarelo, LOW);
    digitalWrite(ledVermelho, HIGH);

    tone(buzzer, 3000); 
    delay(3000);

## Se a luminosidade estiver dentro dos paramêtros permitidos, mas acima do ideal, ativará o LedAmarelo numa função else if e não tocará o buzzer.
    
  } 
  else if (luminosidade >= 400 && luminosidade <= 830) {
    // Estado: ALERTA
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarelo, HIGH);
    digitalWrite(ledVermelho, LOW);
    noTone(buzzer);
  } 

## Mas caso nenhuma das opções sejam verdadeiras, o LedVerde vai ser ativado, indicando que tudo está dentro dos parâmetros desejados e o buzzer não irá tocar.

  else {
    // Estado: OK
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledAmarelo, LOW);
    digitalWrite(ledVermelho, LOW);
    noTone(buzzer);

  }

## Delay de 100 milissegundos para executar o código:

  delay(100);

---------------------------------------------------------------------------------------------------------------
Cuidados:
---------------------------------------------------------------------------------------------------------------

Cuidado com os LEDs:
1. Sempre conecte o resistor em série com o LED para evitar sobrecarga (ou erro de Parâmetros acima do limite permitido (em mA)), lembrando-se de evitar colocar finais de resistores no mesmo lugar onde se tem um caminho de um cátodo, pois isso permitira á passagem da corrente elétrica pelo circuito sem a resistência adequada, podendo queimar componentes e até mesmo o Arduino.

2. Montagem do LDR: Conecte o 5V em uma perna, o pino A0 na outra, e um resistor de 10k entre o A0 e o GND 
(configuração Pull-Down).Buzzer: Conecte o terminal positivo no pino 7 e o negativo no GND.

---------------------------------------------------------------------------------------------------------------
Link para Exércicio Completo:
---------------------------------------------------------------------------------------------------------------

Link para dôminio do Template digital via Tinkercard:

https://www.tinkercad.com/things/aSazIqzX2dE-swanky-waasa-curcan/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=NSCtLN8UP-vfwpvHQbAytcM7703HTVuPjnbkB33sQwg

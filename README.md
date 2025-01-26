# Conversor DC-DC com SIC437A

Este projeto implementa um conversor buck baseado no controlador SIC437A da Vishay, projetado para converter uma entrada de 25,2V em uma saída regulada de 5V com capacidade de fornecer até 12A. 

## Objetivo
O objetivo deste projeto é apresentar o design de um circuito de conversor DC-DC de alta eficiência, considerando os cálculos necessários para os componentes como resistores, capacitores e indutores, garantindo confiabilidade e desempenho.

---

## Cálculos dos Componentes

### 1. **Capacitores de Saída (COUT_Cer)**
- **Quantidade:** 3 capacitores de 47µF (cerâmicos, X7R, 16V).
- **Capacitância Total:** 
  \[ C_{total} = 3 \times 47\,\mu F = 141\,\mu F \]
- **Ripple de Corrente Necessário:**
  \[ I_{ripple} = \frac{\Delta I_L}{2} \times \sqrt{3} = \frac{5,5\,A}{2} \times \sqrt{3} \approx 4,76\,A \]  
  Cada capacitor deve suportar pelo menos \( 4,76\,A \).
- **Tensão de Operação:** Deve ser maior que o VOUT, ou seja, **16V** é suficiente.

### 2. **Capacitores de Entrada (CIN_B)**
- **Capacitância Necessária:**
  \[ C_{IN} = \frac{I_{out}}{f \times \Delta V_{IN}} \approx \frac{12}{500\,kHz \times 0,1} = 240\,\mu F \]
  Utilizou-se um capacitor de 150µF + capacitores cerâmicos para suportar o ripple de corrente.
- **Ripple de Corrente Necessário:** Aproximadamente **6A**.
- **Tensão de Operação:** Deve suportar o VIN máx de **25,2V**, então escolheu-se capacitores de **30V**.

### 3. **Indutor (L1)**
- **Indutância Calculada:**
  \[ L = \frac{(V_{in} - V_{out}) \times D}{\Delta I_L \times f} \approx \frac{(25,2 - 5) \times 0,8}{5,5 \times 500\,kHz} \approx 2,91\,\mu H \]  
  Escolheu-se um indutor de **2,2µH** considerando margens de segurança.
- **Corrente Máxima:** Deve suportar a corrente média de saída (12A) + \( \Delta I_L / 2 \), ou seja, pelo menos **14A**.

### 4. **Resistores do Divisor de Tensão (RFB1 e RFB2)**
- **Relação de Resistores:**
  \[ \frac{R_{FB1}}{R_{FB2}} = \frac{V_{out}}{V_{ref}} - 1 \approx \frac{5}{0,6} - 1 = 7,33 \]
  Selecionados:
  - \( R_{FB1} = 73,2k\,\Omega \)
  - \( R_{FB2} = 10k\,\Omega \)
- **Potência Dissipada:**
  \[ P = \frac{V_{out}^2}{R} \approx \frac{5^2}{73,2k} \approx 0,34\,mW \]
  Resistor com potência de 0,125W é suficiente.

### 5. **Resistores de Configuração (RM1 e RM2)**
- **Valores Escolhidos:**
  - \( R_{M1} = 100k\,\Omega \)
  - \( R_{M2} = 499k\,\Omega \)
- **Potência Dissipada:**
  Negligenciável devido ao baixo consumo no pino de configuração.

### 6. **Resistor de Pull-Up (RPG)**
- **Valor Selecionado:**
  \( R_{PG} = 100k\,\Omega \).
- **Potência Dissipada:**
  \[ P = \frac{V_{PG}^2}{R} = \frac{5^2}{100k} \approx 0,25\,mW \]

### 7. **Capacitores CVDD e CVDRV**
- **Valores:**
  - CVDD: 1µF, **16V**.
  - CVDRV: 4,7µF, **16V**.
- **Ripple de Corrente:** Ambos suportam corrente de ripple mínima devido à função de desacoplamento.

### 8. **Resistores de Enable (RenH e RenL)**
- **Valores:**
  - RenH: 562kΩ.
  - RenL: 309kΩ.
- **Potência Dissipada:**
  \[ P = \frac{V_{in}^2}{R} \]
  - RenH: \( \frac{25,2^2}{562k} \approx 1,13\,mW \).
  - RenL: \( \frac{25,2^2}{309k} \approx 2,05\,mW \).

---

## Conclusão
Os cálculos apresentados garantem que todos os componentes foram selecionados para atender aos requisitos de desempenho do circuito, considerando eficiência, dissipação de potência e segurança dos componentes.

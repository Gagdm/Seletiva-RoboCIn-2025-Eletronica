# Conversor DC-DC com SIC437A

Este projeto implementa um conversor buck baseado no controlador SIC437A da Vishay.

## Objetivo
Desenvolver um regulador DC-DC, utilizando a ferramenta Altium Designer, que receba uma tensão de entrada entre 7,4V e 25,2V e forneça uma saída constante de 5V com corrente mínima de 5A. Além disso, é necessário atentar não apenas para a eficiência do circuito (mínima de 90%), mas também para o valor e as dimensões dos componentes.

---

![Echematic](https://github.com/user-attachments/assets/016dffe6-f8ea-4f01-96c6-930d55ef53fd)

---

### 🟡
- Esta seção é responsável por receber a alimentação do circuito, filtrá-la e garantir uma entrada limpa e estável para o regulador de tensão.

#### Componentes
- JIN? : Um conector para a entrada de alimentação.
- CINB? (150uF): Capacitor de desacoplamento o qual remove ruídos transitórios, como picos de tensão causados pela fonte ou pelo chaveamento do regulador.
- CIND? (0,1uF): Também um capacitor de desacoplamento, trabalhando em conjunto com CINB? para aumentar a eficiência do filtro, abordando diferentes faixas de frequências indesejadas.
> No geral, Esses capacitores garantem que a tensão entregue ao regulador seja o mais estável possível, evitando ruídos que possam interferir no funcionamento do circuito.

---

### 🔴
- Formam um divisor de tensão que define a tensão de saída (VOUT) do regulador e alimentam o pino de feedback (FB), permitindo ao controlador ajustar o ciclo de trabalho (duty cycle) para manter a saída estável.

#### Componentes
- Os resistores RFB1 (73,2kΩ) e RFB2 (10kΩ) dividem a tensão de saída (VOUT) para gerar um sinal proporcional que é enviado ao pino FB do regulador.

$$
RFB1 = \frac{FRB2 (V_{out} - V_{FB})}{V_{FB}}
$$

Temos, Vout = 5V, RFB1 = 10kΩ e Vfb = 0,6V (RFB1 e Vfb são definidos no datasheet do SIC437). Portanto,

$$
RFB1 = \frac{10.10^{3} (5 - 0,6)}{0,6} \simeq 73.333Ω \simeq 73,2kΩ
$$

- COUTD (0,1uF): Reduz ruídos de alta frequência na saída do regulador, ajudando a garantir uma tensão limpa e estável.
> Resumidamente, Permitem que o regulador monitore e ajuste a tensão de saída para mantê-la estável, além de determinam a tensão de saída por meio do divisor resistivo.

---

### 🟢
- Divisor de Tensão, esses resistores formam um divisor de tensão entre VIN (tensão de entrada) e o pino EN do regulador. O objetivo é garantir que o regulador seja habilitado somente quando a tensão de entrada atinge um valor mínimo seguro, prevenindo operação em condições inadequadas.

#### Componentes
- RenH (562kΩ)
- RenL (309kΩ)
> De forma geral, Funcionam como um divisor de tensão e proteção contra subvoltagem.

---

### 🔵 
- Esta parte auxilia o circuito de chaveamento do regulador, especialmente para operar o MOSFET superior em um regulador buck.

#### Componentes
- CBOOT? (0,1µF): Capacitor de bootstrap,fornecendo a energia necessária para acionar o MOSFET superior (high-side) durante o chaveamento, além de ser carregado toda vez que o MOSFET inferior (low-side) está conduzindo.
- RBOOT? (2Ω): Resistor em série com o capacitor de bootstrap, limitando a corrente para evitar danos ao capacitor ou ao circuito do regulador.
> O capacitor de bootstrap carrega uma tensão suficiente para abrir o MOSFET superior. Sem ele, o regulador não conseguiria operar eficientemente em topologias buck.

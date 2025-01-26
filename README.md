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
- Os resistores RFB1 (73,2kΩ) e RFB2 (10kΩ) dividem a tensão de saída (VOUT) para gerar um sinal proporcional que é enviado ao pino FB do regulador. Dessa forma, ajustam a tensão de saída do regulador e garantem que o feedback forneça um sinal preciso ao controlador.

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

---

### 🟣
- Conecta a carga ao circuito regulador e fornece a energia estabilizada.

#### Componentes
- JOUT?: Conector de saída para o dispositivo ou circuito que será alimentado.
- Indutor (2,2µH): Componente fundamental em circuitos buck, uma vez que armazena energia durante o ciclo de chaveamento e libera energia para a carga durante o período off do MOSFET superior. Além disso, auxilia os capacitores a suaviza a corrente de saída.
- COUTA, COUTB, COUTC (47uF): Conjunto de capacitores eletrolíticos que estabilizam a tensão de saída e reduzem o ripple (ondulação), de forma conjunta com o indutor.
> O indutor trabalha em conjunto com os capacitores para garantir uma corrente constante para a carga, eliminando ondulações excessivas.

---

### 🟠
- Este é o coração do circuito, onde ocorre a conversão DC-DC do tipo buck. O regulador reduz a tensão de entrada para um valor de saída menor, controlando o fluxo de energia por meio de chaveamento.

#### Componentes
- IC Regulador Buck SIC437: Realiza a conversão de tensão utilizando MOSFETs internos que alternam entre condução e corte em alta frequência.

---

### 🟤
- Fornece suporte à tensão de VDRVVDRV, que alimenta os drivers internos dos MOSFETs do conversor.

#### Componentes
- CVDRV (4,7uF): É o capacitor conectado ao pino VDRV, que fornece energia aos drivers internos para alternar os MOSFETs. Os drivers alternam rapidamente em cada ciclo (frequência de comutação) e consomem corrente pulsante proporcional à carga de porta total dos MOSFETs.

---

### ⚫
- trabalham juntos para garantir o funcionamento estável, seguro e configurável do regulador DC-DC.

#### Componentes
- CVDD (1uF): Estabilizar e filtrar a alimentação interna do regulador, reduzindo ruídos e garantindo o funcionamento correto do circuito interno, atuando como uma fonte de energia local para suavizar variações instantâneas de corrente demandadas pelos circuitos internos (como drivers de gate e lógica de controle).
> Reduz flutuações e ruídos na alimentação interna do IC regulador, além de ajuda a manter o regulador estável em operações de alta frequência.
- RM1 (100kΩ) e RM2 (499kΩ): Ajustar e configurar parâmetros relacionados ao funcionamento do regulador, como a corrente de operação ou outras características internas do IC. Esses resistores determinam o modo de operação do regulador, como o modo PWM (Pulse Width Modulation) ou modo PFM (Pulse Frequency Modulation), ou definem outros comportamentos específicos.
> Em resumo, Configuram o comportamento do regulador por meio de ajustes de tensão ou corrente e definem modos de operação ou parâmetros como frequência de chaveamento ou eficiência.
- RPG (100kΩ): Força um pino do regulador para o nível lógico baixo quando não há sinal ativo, garantindo comportamento definido e evitando flutuações indesejadas. Logo, Garante um estado definido (baixo) no pino de controle para evitar flutuações ou ativação acidental, devido a isso, Melhora-se a confiabilidade do circuito ao prevenir estados indesejados.
> Resumidamente, CVDD fornece suporte interno ao regulador, estabilizando sua alimentação, RM1 e RM2 ajustam o comportamento do regulador, permitindo personalização de parâmetros operacionais e RPG garante que o regulador tenha um comportamento previsível em estados inativos ou de inicialização.

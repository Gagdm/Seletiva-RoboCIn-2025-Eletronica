# DESENVOLVER UM REGULADOR DE TENSÃO DC-DC
> O conversor DC-DC é utilizado quando a tensão disponível é originária de uma fonte de alimentação DC (pilhas, bateria, retificador) e a carga (placa de desenvolvimento, circuito ou componente) exige um valor diferente de tensão para seu funcionamento.
> Mini Regulador de Tensão MP1584 Step Down é um módulo de tamanho reduzido ideal para utilização em projetos embarcados, projetos de IoT e aeromodelismo, entre outros. Além disso, aceita entradas entre 4,5 e 28 V e a saídas entre 0,8 e20 V, sendo a tensão de saída regulada através do trimpot da placa.

## Tutorial Altium -

1- Workspace ➡️ File ➡️ New ➡️ Project

2- Project ➡️ Add New to project ➡️ Schematic

3- Project ➡️ Add New to project ➡️ PCB
>PCB é achar partes, juntando elas e colocando elas em uma placa impressa com partes mecânicas. Então, precisamos de partes e as encontraremos nas bibliotecas.

### Como add uma biblioteca -

4- Project ➡️ Add New to project ➡️ Schematic Library
> isso será a biblioteca de símbolos, ainda é necessário uma biblioteca para as partes mecânicas.

5- Project ➡️ Add New to project ➡️ PCB Library

### Iniciando o Schematic -

6- Schematic (.SchDoc) ➡️ Properties ➡️ Panels ➡️ Manufacturer Part Search ➡️ Procura o componente pelo nome

Após a escolha do componente e do fornecedor,

7- Component ➡️ Place 
> o esquemático do componente será colocado no arquivo Schematic.

O processo (6 e 7) se repetem para qualquer componente desejado.

Boa prática, 
Double click on a component ➡️ colocar no lugar do nome informações importantes

Para deixar recados para recordar mais tarde,
Right click ➡️ Place ➡️ Note

### Criando símbolos e partes -

1- Schematic Library (double click on it)

2- Place ➡️ Escolhe a forma que o símbolo terá ➡️ Cria a "caixa" do símbolo

3- Place ➡️ Pin
> No X é onde vocẽ pode fazer conexões elétricas com o Pin.
> O mais importante é sempre colocar o Pin na grade.

4- Coloque o Pin, juntamente com a caixa criada, na coordenada (0,0)
> Caso o pino esteja sobrepondo o bloco: Click on the block ➡️ Edit ➡️ Move ➡️ Send to back

5- Properties ➡️ Supplier Links ➡️ Add Supplier Links ➡️ Add o TE Internal # do produto ➡️ OK ➡️ Ok

6- Properties ➡️ edit the information about the item created

7- Properties ➡️ Add ➡️ Parameter (definindo a conexão)

8- Add ➡️ Parameter (Manufacturer product number)

9- Add ➡️ Link

10- Save all

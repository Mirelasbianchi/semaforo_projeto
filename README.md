# 🚦🚦🚦 Projeto: Semáforo Inteligente para o Bairro Butantã

## Sumário
- [Autora](#autora)
- [Contexto do Projeto](#contexto-do-projeto)
- [Objetivos](#objetivos)
- [Parte 1: Montagem Física](#parte-1-montagem-física)
  - [Componentes Utilizados](#componentes-utilizados)
  - [Esquema de Ligação](#esquema-de-ligação)
  - [Tutorial de montagem](#tutorial-de-montagem)
- [Parte 2: Programação e Lógica](#parte-2-programação-e-lógica)
  - [Código](#código)
  - [Funcionamento e Testes](#funcionamento-e-testes)
  - [Vídeo de Demonstração](#vídeo-de-demonstração)
- [Parte 3: Avaliação de Pares](#parte-3-avaliação-de-pares)
- [Aprendizados e Conclusões](#aprendizados-e-conclusões)
- [Possíveis Extensões Futuras](#possíveis-extensões-futuras)
- [Licença](#licença)

---

## Autora
Mirela Schneider Bianchi

---

## Contexto do Projeto
A cidade de São Paulo possui um tráfego intenso, e o bairro do Butantã é um dos pontos de maior movimentação. O controle eficiente de semáforos é essencial para evitar congestionamentos e garantir a segurança dos pedestres.  

Este projeto visa criar uma **simulação funcional de um semáforo urbano**, seguindo tempos típicos de operação e demonstrando como princípios simples de eletrônica e programação podem contribuir para soluções reais de mobilidade urbana.

---

## Objetivos
Desenvolver a **montagem física** de um semáforo em protoboard.  
Implementar o **código de controle** com temporização para as três fases (vermelho, verde e amarelo).  
Demonstrar o **funcionamento contínuo e automatizado** do sistema.  
Aplicar conceitos de **engenharia, lógica sequencial e segurança viária**.  

---

## Parte 1: Montagem Física

### Componentes Utilizados

| Componente | Quantidade | Especificação / Função |
|-------------|-------------|------------------------|
| Arduino Uno | 1 | Controlador principal |
| LED Vermelho | 1 | Indica "Pare" |
| LED Amarelo | 1 | Indica "Atenção" |
| LED Verde | 1 | Indica "Siga" |
| Resistores | 3 | 220 Ω (proteção dos LEDs) |
| Protoboard | 1 | Montagem do circuito |
| Jumpers | 5 | Conexões entre pinos e LEDs |
| Cabo USB | 1 | Alimentação e upload do código |

---

### Esquema de Ligação

| LED | Pino Digital Arduino | Resistor | Conexão ao GND |
|------|----------------------|-----------|----------------|
| Vermelho | 8 | 330 Ω | Sim |
| Amarelo | 9 | 330 Ω | Sim |
| Verde | 10 | 330 Ω | Sim |

### Tutorial de Montagem 

1. **Posicionamento dos LEDs na Protoboard**  
   Os LEDs foram posicionados verticalmente na protoboard seguindo a ordem tradicional empregada em sistemas semafóricos: vermelho na parte superior, amarelo ao centro e verde na parte inferior.  

   Cada LED possui duas pernas (terminais):  
   - **Ânodo (terminal positivo)** → normalmente a perna **mais longa**;  
   - **Cátodo (terminal negativo)** → perna **mais curta**, geralmente próxima ao chanfro ou parte plana da cápsula.  

   No circuito, o **ânodo** é conectado ao pino digital do Arduino responsável pelo controle, enquanto o **cátodo** é conectado ao GND por meio de um resistor. Essa ligação garante o sentido correto da corrente, evitando inversão de polaridade.

<p align="center">
  <img src="./sema.png" width="400" alt="LEDs posicionados na protoboard">
</p>

---

2. **Conexão dos Resistores (Proteção de Corrente)**  
   Cada LED foi conectado em **série** com um resistor de **220 Ω**.  

   A função do resistor é **limitar a corrente elétrica** que atravessa o LED, evitando que ele receba valores superiores ao recomendado (aproximadamente 20 mA). Sem essa proteção, o LED poderia sofrer **sobrecorrente**, ocasionando superaquecimento e queima do componente.

   Esta relação é explicada pela **Lei de Ohm**:

   V = R.I

   Onde:
   - *V* é a tensão aplicada,
   - *R* é a resistência,
   - *I* é a corrente resultante.

   Logo, ao definir R = 220 Ω, garantimos que a corrente permaneça em um nível seguro para o funcionamento contínuo dos LEDs.

<p align="center">
  <img src="./sema1.png" width="400" alt="Conexões com resistores">
</p>

---

3. **Ligação ao Arduino e Organização dos Jumpers**

| LED | Pino Digital do Arduino (Ânodo) | Cátodo → Resistor → GND |
|-----|--------------------------------|--------------------------|
| Vermelho | **8** | Sim |
| Amarelo  | **9** | Sim |
| Verde    | **10** | Sim |

   Quando o Arduino envia um sinal **HIGH (5V)** para o pino, o LED acende; quando envia **LOW (0V)**, o LED apaga. Isso permite a criação da sequência lógica do semáforo via programação.

   Os jumpers foram organizados de maneira paralela e limpa, evitando cruzamento excessivo de fios, o que facilita:
   - Visualização do circuito
   - Identificação de falhas
   - Modificações futuras

<p align="center">
  <img src="./sema3.png" width="400" alt="Conexões com Arduino">
</p>

---

4. **Testes e Ajustes Finais**  
   Após a montagem, cada LED foi testado individualmente através de comandos simples no código (`digitalWrite(pin, HIGH/LOW)`), verificando:
   - Correta polaridade dos LEDs (ânodo e cátodo)
   - Contatos firmes na protoboard
   - Continuidade entre resistor e terra

   Pequenos ajustes foram realizados até que o ciclo completo do semáforo funcionasse de maneira estável e repetitiva.

<p align="center">
  <img src="./sema4.png" width="400" alt="Testes e ajustes finais">
</p>


## Parte 2: Programação e Lógica

O comportamento do semáforo segue a seguinte sequência temporal:

Cor /	Duração	/ Significado
- 🔴 Vermelho	6 segundos	Pare
- 🟢 Verde	4 segundos	Siga
- 🟡 Amarelo	2 segundos	Atenção / Troca de fase

### Código 
```
void setup()
{
  pinMode(8, OUTPUT); //vermelho
  pinMode(9, OUTPUT); //amarelo
  pinMode(10, OUTPUT); //verde
}

void loop()
{
  digitalWrite(8, HIGH); //acende o vermelho
  delay(6000);
  digitalWrite(8, LOW);

  digitalWrite(10, HIGH); //acende o verde
  delay(4000);
  digitalWrite(10, LOW);

  digitalWrite(9, HIGH); //acende o amarelo
  delay(2000);
  digitalWrite(9, LOW);
}

```
## Funcionamento e Testes

Durante os testes:
- O LED vermelho acende por 6 segundos.
- Em seguida, o LED verde permanece aceso por 4 segundos.
- Por fim, o LED amarelo acende por 2 segundos antes de reiniciar o ciclo.
Este ciclo se repete continuamente, simulando o funcionamento de um semáforo urbano em condições normais de tráfego.

 ## Vídeo de Demonstração:
[Clique aqui para assistir](https://drive.google.com/file/d/1wIwsxWDxblmjbJlVcYHwEUNKgwmkOpX3/view?usp=sharing)


## Parte 3: Avaliação de Pares

| Avaliador(a) | Comentário / Nota |
|--------------|------------------|
| Nome 1       | [Comentário aqui] / [0–10] |
| Nome 2       | [Comentário aqui] / [0–10] |

Critérios de avaliação:
- Clareza da montagem física
- Correção do código e tempos de execução
- Qualidade da documentação
- Demonstração em vídeo
- Aprendizados e Conclusões

## Aprendizados e Conclusões

Durante a montagem e programação do semáforo, foi possível compreender de forma prática como componentes eletrônicos básicos, como LEDs, resistores e jumpers, interagem com um microcontrolador para formar um sistema funcional. Aprendi a configurar corretamente pinos digitais do Arduino, a calcular e aplicar resistores para proteger os LEDs, e a organizar a protoboard de forma eficiente para facilitar conexões e manutenção. Além disso, a experiência permitiu consolidar conceitos de temporização em código, loops contínuos e controle sequencial, reforçando a relação direta entre hardware e software em sistemas embarcados simples.


## Possíveis Extensões Futuras
- Adicionar botão de pedestre com temporização adicional.
- Implementar sensor de movimento (ultrassônico ou infravermelho).
- Integrar com display LCD exibindo contagem regressiva.
- Criar uma rede de semáforos inteligentes sincronizados via IoT.


 ## Licença
Este projeto está licenciado sob a licença MIT — sinta-se à vontade para usar, estudar e modificar para fins educacionais.

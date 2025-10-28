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
- [Especificações Elétricas](#especificações-elétricas)
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
| Jumpers | 8 | Conexões entre pinos e LEDs |
| Cabo USB | 1 | Alimentação e upload do código |

---

### Esquema de Ligação

| LED | Pino Digital Arduino | Resistor | Conexão ao GND |
|------|----------------------|-----------|----------------|
| Vermelho | 13 | 220 Ω | Sim |
| Amarelo | 12 | 220 Ω | Sim |
| Verde | 11 | 220 Ω | Sim |

### Tutorial de Montagem

1. **Posicionamento dos LEDs na protoboard**  
   Os LEDs foram posicionados verticalmente na protoboard seguindo a ordem tradicional do semáforo: vermelho no topo, amarelo no meio e verde na parte inferior. Esta disposição facilita a visualização e organização das conexões.  

<p align="center">
  <img src="./imagens/tutorial_montagem_1.jpg" width="400" alt="LEDs posicionados na protoboard">
</p>

2. **Conexão dos resistores**  
   Cada LED foi conectado em série com um resistor de 220 Ω para limitar a corrente e proteger os componentes. Os resistores foram posicionados próximos aos LEDs para reduzir o comprimento dos fios e evitar confusão na protoboard.  

<p align="center">
  <img src="./imagens/tutorial_montagem_2.jpg" width="400" alt="Conexões com resistores">
</p>

3. **Ligação ao Arduino**  
   Cada LED foi conectado a um pino digital do Arduino (vermelho: pino 13, amarelo: pino 12, verde: pino 11) e ao GND através do resistor. Essa configuração permite controlar individualmente cada LED via programação.  

<p align="center">
  <img src="./imagens/tutorial_montagem_3.jpg" width="400" alt="Conexões com Arduino">
</p>

4. **Organização dos jumpers**  
   Os fios de conexão (jumpers) foram dispostos de forma a manter a protoboard organizada, evitando sobreposição e facilitando futuras alterações no circuito.  

<p align="center">
  <img src="./imagens/tutorial_montagem_4.jpg" width="400" alt="Organização dos jumpers">
</p>

5. **Testes e ajustes finais**  
   Após a montagem, foram realizados testes para garantir que cada LED acendesse corretamente conforme o código. Pequenos ajustes nas conexões foram necessários para corrigir contatos soltos e otimizar o fluxo do circuito.  

<p align="center">
  <img src="./imagens/tutorial_montagem_5.jpg" width="400" alt="Testes e ajustes finais">
</p>


## Parte 2: Programação e Lógica

O comportamento do semáforo segue a seguinte sequência temporal:

Cor /	Duração	/ Significado
- 🔴 Vermelho	6 segundos	Pare
- 🟢 Verde	4 segundos	Siga
- 🟡 Amarelo	2 segundos	Atenção / Troca de fase

### Código 
```
// Projeto: Semáforo - Departamento de Engenharia de Trânsito
// Autor: [Seu Nome]
// Data: [dd/mm/aaaa]

int ledVermelho = 13;
int ledAmarelo = 12;
int ledVerde = 11;

void setup() {
  pinMode(ledVermelho, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVerde, OUTPUT);
}

void loop() {
  // Fase Vermelha
  digitalWrite(ledVermelho, HIGH);
  delay(6000);
  digitalWrite(ledVermelho, LOW);

  // Fase Verde
  digitalWrite(ledVerde, HIGH);
  delay(4000);
  digitalWrite(ledVerde, LOW);

  // Fase Amarela
  digitalWrite(ledAmarelo, HIGH);
  delay(2000);
  digitalWrite(ledAmarelo, LOW);
}
```
## Funcionamento e Testes

Durante os testes:
- O LED vermelho acende por 6 segundos.
- Em seguida, o LED verde permanece aceso por 4 segundos.
- Por fim, o LED amarelo acende por 2 segundos antes de reiniciar o ciclo.
Este ciclo se repete continuamente, simulando o funcionamento de um semáforo urbano em condições normais de tráfego.

 ## Vídeo de Demonstração:
 Clique aqui para assistir ao vídeo no YouTube
 (insira o link do seu vídeo)

 Figura 2 — Semáforo em funcionamento
<p align="center">
  <img src="./imagens/semaforo_funcionando.gif" width="500" alt="Funcionamento do Semáforo">
</p>


## Especificações Elétricas
- Componente	Tensão (V)	Corrente (mA)	Observação
- LED Vermelho	2.0	20	Alta visibilidade
- LED Amarelo	2.1	20	Transição segura
- LED Verde	2.2	20	Baixo consumo
- Resistor	-	-	220 Ω de limitação de corrente
- Arduino Uno	5V	-	Alimentação USB ou externa

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

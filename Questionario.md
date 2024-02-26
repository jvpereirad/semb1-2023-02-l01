# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
A compilação cruzada é o processo em que o desenvolvedor desenvolve e compila um programa em uma plataforma diferente da que ele vai 
executado o codigo. Ela é bastante usada em sistemas embarcados para criar programas para micro-processadores devido a baixo poder 
de processamento deles, usamos um computador para desenvolver o código.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
O codigo de startup é um conjunto de instruções que vao ser executadas por um sistema embarcado quando ele é ligado ou iniciado.
É esse codigo que irá fazer a configuração inicial do sistema para preparar pra executar o software principal

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
O makefile serve para automatiar o processo de compilação e vinculação do codigo fonte em diferentes arquivos que podem ter alguma 
dependencia entre si.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
Ele verifica as dependencias do codigo principal e executa as regras de compilação conforme necessário.

#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
a sintaxe utilizada é a seguinte

                                        target: pre_requisitos
                                           comandos

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
As dependencias de um target em um makefile sao as entradas ou pre requisitos necessario para contruir ou atualizar esse target,
elas sao usadas pelo make para determinar se o target precisa ser reconstruido e quando ele precisa ser reconstruido.

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
As regras do makefile sao o que definem como construir ou atualizar um target, elas consistem em um target, suas dependencias e os 
comandos necessarios para executar a construção.

As regras explicitas sao aquelas que o usuario coloca no makefile para definir como construir um determinado target, elas definem 
explicitamente os comandos necessarios para construir um target específico.
Já as regras implicitas são aquelas que já sao forncidas por padrao pelo makefile para construir determinados tipos de arquivos. Elas
sao usadas quando o Makefile nao contem uma regra explicita para um target, mas o utilitario make pode inferir como construií-lo.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
O modo de instrução Thumb é uma versao compactada do conjunto de instruções original ARM, ele foi feito para otimizar o desempenho
em sistemas com restrições de memória como sistemas embarcados.
Suas vantagens são: Intruções compactas, Ecnomia de espaço de codigo, menor largura de banda de memoria, eficiencia de cache e 
desempenho aprimorado com restriçoes de energia.
Ele operam em conjunto com o conjunto de instruções do ARM, oferecendo flexibilidade para os desenvolvedores escolherem entre 
eficiencia de tamanho de codigo (modo Thumb) e funcionalidades completas (modo ARM).

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.
As Arquiteturas ARM Load/Store e Register/register tem algumas diferenças, a principais são:
Na Arquiteturas ARM Load/Store as instruções sao projetadas para serem simples, sao usadas para acessar a memoria e transferem
dados entre a memoria e os registradores do processador.
Já na aquitetura register/register as intruçoes frequentemente operam diretamente nos registros do processador e na memoria,
podem e tendem a ser mais complexas e permitem operações diretas entre dois registradores sem a necessidade de instruções separadas de carga/armazenamento.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
Para os niveis de acesso temos:
Privileged: premite acesso completo a todas as funcionalidades do processador, o codigo pode acessar e modificar todos os registradores
do processador, acessar perifericos, manipular interrupções e acessar qualquer parte da memoria.
Unprivileged: este nicel restringe acessoas a algumas funcionalidades do sistema, o codigo tem acesso limitado a alguns registradores
e partes da memoria e perifericos.

Para os modos de operação temos:
Thread mode: é o modo padrao do Cortex M, o processador executa o codigo e geralmente opera em um dos niveis de acesso. Ele oferece suporte a interrupções e execeções.
Handler mode: é um modo especial de operação usado para tratar interrupções e exceções, quando estas ocorrem o processador muda para 
o Handler mode para executar o codigo de tratamento associado, esse modo tem acesso privilegiado.
User mode: é um modo de operação opcional que pode ser habilitado em alguns processadores Arm Cortex M, é de modo nao privilegiado
e restringe o acesso a alguns recursos e funcionalidades.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
Os processadores ARM tratam exceções e interrupções usando estratégias de priorização, como Group Priority e Subpriority, para garantir que eventos críticos sejam tratados imediatamente e de forma adequada, mesmo quando múltiplos eventos estão ocorrendo simultaneamente.
Os tipos de exceções sao: Exceções Sincronas que sao tratadas durante a execução normal do programa e Exceções Assincronas que o 
processador responde a essas exceções imediatamente, interrompendo a execução do programa e tratando a exceção.
As execeções e interrupções sao agrupadas de acordo com sua criticidade e prioridade, facilitando a alocação eficiente de recursos do 
sistema, isso é a estrategia de group priority. A sub priority fornece uma maneira adicional de priorizar exceções e interrupções 
dentro de um grupo de prioridade, garantindo que exceções mais criticas sejam tratadas primeiro dentro de um mesmo grupo.


### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
Enquanto o CPSR armazena o estado atual do programa durante a execução normal do codigo, o SPSR é usado para armazenar temporariamente
esse estado durante a execução de exceções e interrupções, garantindo que o processador possa retornar ao estado anterior do programa
apos o tratamento.

### (f) Qual a finalidade do **LR** (***Link Register***)?
O link register armazena o endereço de retorno de uma função, permitindo que o programa retorne a instrução correta apos a execução 
de uma função

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
Ele mantem informações importantes sobre o estado do programa, o modo de operação do processador e flags de status ajudando a coordenar
a execução de instruções e o tratamento de exceções e interrupções

### (h) O que é a tabela de vetores de interrupção?
É uma estrutura de dados essencial que é usada para direcionar o processador para os tratadores de interrupção apropriados.

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
O NVIC faz a gestão, priorização, alinhamento e habilitação e desabilitação de interrupções. Ele pode ser utilizado permitindo respostas
imediatas a interrupções, e controlando a latencia de interrupções, ele tambem permite que uma interrupção que algumas interrupções sejam temporariamente desativasdas enquanto acontece outra.

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 
O EXC_RETURN é um valor especial que é escrito no registrador LR quando uma exceção ocorre. Ele contém informações sobre o modo de retorno de exceção, incluindo o modo de operação de thread, o estado de controle do processador, informações sobre pilha e outros detalhes. Existem vários valores possíveis de EXC_RETURN, dependendo do tipo de exceção, do modo de retorno desejado e do contexto de pilha. O valor EXC_RETURN é codificado em bits específicos dentro do registrador LR e é interpretado pelo processador Cortex-M durante o retorno da exceção.

O processador Cortex-M examina o valor do EXC_RETURN extraído do registrador LR e com base no valor do EXC_RETURN, o processador restaura o contexto anterior da pilha, incluindo o modo de operação da thread, os valores dos registradores e outras informações relevantes, após isso, o processador continua a execução do programa no ponto onde foi interrompido, permitindo um retorno suave da interrupção.

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 
Para o Cortex-M3:
No Cortex-M3, durante a chegada de uma interrupção, o contexto da CPU (registradores de propósito geral) é automaticamente salvo na pilha principal. Isso envolve salvar os registradores essenciais do processador na pilha, como PC, LR, registradores R0-R3, etc.
O salvamento de contexto pode levar um tempo significativo, especialmente se muitos registradores estiverem envolvidos, o que pode impactar o tempo de resposta da interrupção.

Para o Cortex-M4F:
No Cortex-M4F, além do salvamento de contexto da CPU, também é necessário salvar e restaurar os registradores de ponto flutuante (se estiverem em uso) durante a chegada de uma interrupção. Isso aumenta o tempo necessário para salvar e restaurar o contexto, pois há mais registradores envolvidos. O uso adicional da pilha para armazenar os registradores de ponto flutuante também pode aumentar o uso de memória, especialmente em sistemas com memória limitada.

O conceito de lazy stack é uma técnica para otimizar o salvamento de contexto durante a chegada de uma interrupção, adiando o salvamento de alguns registradores até que sejam necessários. Isso é especialmente útil quando o código do usuário (ISR) não faz uso de todos os registradores salvos no contexto. Com o lazy stack, apenas os registradores essenciais são salvos inicialmente, e os registradores adicionais são salvos somente se forem modificados durante a execução da ISR.
O lazy stack pode ser configurado pelo programador por meio de opções de configuração específicas do compilador ou diretivas de código.
O compilador pode gerar código otimizado para aproveitar o lazy stack, analisando o código da ISR e decidindo quais registradores precisam ser salvos imediatamente e quais podem ser adiados.Isso pode reduzir o tempo necessário para salvar e restaurar o contexto da ISR, melhorando o desempenho geral do sistema.


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)

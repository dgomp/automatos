# Autômatos Finitos Não Determinísticos
Estudo sobre autômatos finitos não determinísticos (AFND), baseado em exercício para a cadeira de "Linguagens e Autômatos", do professor França (Uni7).


## O que é?

	Ser um Autômato Finito Não Determinístico (AFND) significa que não há como saber
 	exatamente como será o caminho, já que há a possibilidade de mais de um caminho,
 	ou seja, um conjunto de novos estados.

### Exemplos
	Segue, abaixo, 03 (três) exemplos de Autômatos Finitis Não Determinísticos (AFND),
 	de modo a auxiliar na fixação do conteúdo:

* **Exemplo 1**

	  Com base nesse diagrama, sempre será iniciado com aa ou ab, mas nunca como bb.
	  Dado que há, a partir de q0, há mais de um caminho, ou seja, posso fazer o
	  "a" ou o "b" através de mais de uma forma, temos um AFND.
  
	 ![image](https://github.com/dgomp/automatos/assets/52968011/3a9a0f95-0994-4d0f-9f58-b94888e4a7a5)

  Agora, vamos testar:
    1. **Aceitação** com **ababaa**, **aaabababb**, **aaa** e **abb**;
    2. **Rejeição** com **aba**, **abab**, **baba** e **aab**;
 
       ![image](https://github.com/dgomp/automatos/assets/52968011/9a590ff4-553c-4a31-839b-c5d080ba7c6c)

  Como resultado, temos que:
    1. **ababaa**, **aaabababb**, **aaa** e **abb** foram aceitos;
    2. **aba**, **abab**, **baba** e **aab** foram rejeitados;
 
       ![image](https://github.com/dgomp/automatos/assets/52968011/8312cca7-4a40-439b-abda-c84dc9b4ef9f)

  Analisando o diagrama, é facilmente perceptível que:
    * Não há como iniciar com "b", já que o único caminho, nesse momento, é com "a";
    * Não é possível "aba", pois é menor do que o caminho;
    * Não é possível "abab", pois se utilizasse o loop, não chegaria ao fim, e se seguisse no caminho, no "q2", não há opção para "a";
    * Não é possível "aab", pois é menor do que o caminho e, mesmo que fosse maior (aaba), no "q1", não há opção para "b";

  Temos, portanto, a seguinte **Tabela de Transição**:

    |   :δ:   |      a     |      b     |
    | :-----: | :--------: | :--------: |
    | `start` |   `{q0}`   |    `-`     |
    | `q0`    | `{q0, q1}` | `{q0, q2}` |
    | `q1`    |    `{q3}`  |    `-`     |
    | `q2`    |    `-`     |   `{q3}`   |
    | `q3`    |   `{q3}`   |   `{q3}`   |


* **Exemplo 2**
  
	  Agora, vamos fazer um conjunto de palavras com sufixo "abcd" ou "badc".
	  Como há a possibilidade de mais de um caminho para "a" e para "b", em "start",
	  trata-se de caso de Autômato Finito Não Determinístico (AFND).

	 ![image](https://github.com/dgomp/automatos/assets/52968011/9fda0a3c-6309-4c35-8635-0ef2668c3f38)

  É hora de testar:
    1. **Aceitação** com **abcd**, **aabcd**, **babcd**, **bbadc**, **cabcd** e **dbadc**;
    2. **Rejeição** com **dcabc** e **cdadc**;
 
       ![image](https://github.com/dgomp/automatos/assets/52968011/817f73d7-3e61-4778-8747-1e07c09f7f36)

  Vamos para o resultado:
    1. **abcd**, **aabcd**, **babcd**, **bbadc**, **cabcd** e **dbadc** foram aceitos;
    2. **dcabc** e **cdadc** foram rejeitados;

       ![image](https://github.com/dgomp/automatos/assets/52968011/3bcc7303-e3d8-44c7-b4e7-5e6c76aa5fca)

  Sigamos para a análise:
    * É possível iniciar com "a", "b", "c", "d", sendo o início com a" e "b" claros exemplos de AFND;
    * "abcd" dá certo porque segue o fluxo normal, tradicional;
    * "aabcd" funciona porque faz um loop em start (a) e, depois, segue o fluxo normal em s0-s1-s2-s3;
    * "babcd" é aceito porque faz um loop em start (b) e, depois segue no "abcd" em s0-s1-s2-s3;
    * "bbadc" é possível porque faz um loop em start (b) e, depois, segue no padrão em "badc" em s4-s5-s6-s7;
    * "cabcd" também dá certo porque faz um loop em start (c) e, depois, segue o formato "abcd" em s0-s1-s2-s3;
    * "dbadc" também faz loop em start (d) e, posteriormente, segue no fluxo "badc" em s4-s5-s6-s7;
    * "dcabc" não funciona porque, apesar de fazer o loop em start ("d" e "c"), segue no "abc" (s0-s1-s2), mas não chega ao fim (s3);
    * "cdadc" não é aceito porque, mesmo fazendo o loop em start ("c" e "d"), segue no "a" (s0), mas não tem "d" nesse caminho. A outra hipótese, seria fazer o loop também no start (a), mas também seria barrado no d;


  Temos, portanto, a seguinte **Tabela de Transição**:

    |   :δ:   |        a      |       b       |      c     |      d     |
    | :-----: | :-----------: | :-----------: | :--------: | :--------: |
    | `start` | `{start, s0}` | `{start, s4}` | `{start}`  | `{start}`  |
    | `s0`    |      `-`      |     `{s1}`    |    `-`     |    `-`     |
    | `s1`    |      `-`      |      `-`      |   `{s2}`   |    `-`     |
    | `s2`    |      `-`      |      `-`      |    `-`     |   `{s3}`   |
    | `s3`    |      `-`      |      `-`      |    `-`     |    `-`     |
    | `s4`    |     `{s5}`    |      `-`      |    `-`     |    `-`     |
    | `s5`    |      `-`      |      `-`      |    `-`     |   `{s6}`   |
    | `s6`    |      `-`      |      `-`      |   `{s7}`   |    `-`     |
    | `s7`    |      `-`      |      `-`      |    `-`     |    `-`     |


* **Exemplo 3**
  
	  Vamos para um AFND mais simples, dessa vez, com dupla possibilidade de caminho em s0 e s2,
	  de modo ao aprendizado ficar bem fácil.

  
	 ![image](https://github.com/dgomp/automatos/assets/52968011/0b0081cc-595c-43f1-955c-65713950ad3d)

  Chegou o momento de testarmos:
    1. **Aceitação** com **aaaaaaaaaaab** e **abbbbbaaa**;
    2. **Rejeição** com **bbaaa** e **aabb**;
 
       ![image](https://github.com/dgomp/automatos/assets/52968011/e6756b2a-f3f7-47ce-aaf7-36b3ac2a8f13)

  Vejamos como ficou:
    1. **aaaaaaaaaaab** e **abbbbbaaa** foram aceitos;
    2. **bbaaa** e **aabb** foram rejeitados;

       ![image](https://github.com/dgomp/automatos/assets/52968011/8322d097-4f90-4b5e-9ea7-6ba64dc9115c)

  Conclusões tiradas disso:
    * Sempre deve ser iniciado com "a", pos do start para o s0, o caminho é apenas "a";
    * "aaaaaaaaaaab" porque usa o primeiro "a" para chegar em s0. Os demais a podem ser utilizados em s0, desde que sobre dois "a" para chegar até s2 e concluir com o "b" em loop;
    * "abbbbbaaa" funciona porque faz o caminho de start para s0 (a) e, posteriormente, fica fazendo loop em s0 (bbbbb). Posteriormente, Escolhe fazer um loop em s0 (a) e seguri para s1 e, depois para s2, ou já segue para s1 (a), s2 (a) e, depois faz um loop em s2;
    * "bbaaa" não funciona porque do start para s0, é um "a", logo, fica sem ter como seguir;
    * "aabb" não é aceito porque, apesaar de seguir do start para s0 (a), e conseguir fazer um loop em s0 (a) ou seguir para s1 (a), não consegue chegar em s2, pois s2 somente aceita "a";


  Segue, então, a **Tabela de Transição**:

    |   :δ:   |      a     |    b   |
    | :-----: | :--------: | :----: |
    | `start` |   `{s0}`   |   `-`  |
    | `s0`    | `{s0, s1}` | `{s0}` |
    | `s1`    |   `{s2}`   |   `-`  |
    | `s2`    |   `{s2}`   | `{s2}` |

  `Os testes foram realizados através do [Automaton Simulator](https://automatonsimulator.com).

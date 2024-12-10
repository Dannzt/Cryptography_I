 <h1 align="center">Notes </a> </h1>

  <h2 align="center"> Some pessoal week notes <br> in Portuguese</h2> 


<details>	
 <summary><b> Week 1 </b> </b></summary> 

 week 1
 --------
 O tópico desta semana é uma visão geral do que é a criptografia, bem como nosso primeiro exemplo de cifras. Os senhores aprenderão sobre pseudoaleatoriedade e como usá-la para criptografia. Também veremos algumas definições básicas de criptografia segura.

 --------
### **1. DES (Data Encryption Standard)**

- **Descrição**: Algoritmo de cifragem simétrica desenvolvido nos anos 70 pela IBM e padronizado pelo NIST em 1977.
- **Funcionamento**:
    - Usa **chave de 56 bits** (com 8 bits de paridade) e opera em **blocos de 64 bits**.
    - Realiza **16 rodadas** de permutações (P-boxes) e substituições (S-boxes), envolvendo uma função de expansão, XOR com a chave e substituição.
- **Propriedades**:
    - **Simetria**: Mesma chave para cifrar e decifrar.
    - **Eficiência**: Adequado para hardware dos anos 70/80.
- **Problemas**:
    - O tamanho pequeno da chave torna-o vulnerável a ataques de força bruta (quebrado em menos de 24 horas).
- **Status**: Substituído por algoritmos mais seguros (e.g., AES).

---

### **2. Triple DES (3DES)**

- **Descrição**: Extensão do DES para superar sua limitação de segurança.
- **Funcionamento**:
    - Aplica o DES três vezes sobre os dados: C=E(K3,D(K2,E(K1,M))).
        
        C=E(K3,D(K2,E(K1,M)))C = E(K_3, D(K_2, E(K_1, M)))
        
        - EEE: Cifragem.
        - DDD: Decifragem.
    - Pode operar com duas ou três chaves:
        - **Modo 2-chaves**: K1=K3 → Chave efetiva de 112 bits.
            
            K1=K3K_1 = K_3
            
        - **Modo 3-chaves**: Chave efetiva de 168 bits.
- **Propriedades**:
    - Resistente a ataques de força bruta e meet-in-the-middle.
    - Compatível com sistemas legados baseados em DES.
- **Problemas**:
    - Lento em comparação ao AES.
- **Status**: Gradualmente descontinuado em favor do AES (NIST descontinuou 3DES em 2023).

---

### **3. Double DES (2DES)**

- **Descrição**: Variante do DES que aplica o algoritmo duas vezes com duas chaves diferentes.
- **Funcionamento**:
    - C=E(K2,E(K1,M))C = E(K_2, E(K_1, M))C=E(K2,E(K1,M)), onde K1 e K2 são chaves independentes.
        
        K1K_1
        
        K2K_2
        
- **Problemas**:
    - Vulnerável ao ataque **meet-in-the-middle**, reduzindo a segurança efetiva de 112 bits para cerca de 257 operações (devido à necessidade de armazenamento e comparação de intermediários).
        
        2572^{57}
        
- **Status**: Não amplamente adotado, substituído por 3DES.

---

### **4. Triple DES em padrão NIST**

- **Descrição**: O NIST padronizou o 3DES para cenários de transição entre DES e AES.
- **Modos de operação**:
    - **ECB (Electronic Codebook)**: Divide os dados em blocos independentes (vulnerável a padrões repetidos).
    - **CBC (Cipher Block Chaining)**: Introduz encadeamento entre blocos para melhorar a segurança.
- **Problemas**:
    - Obsoleto devido ao desempenho inferior e aumento das vulnerabilidades teóricas (por exemplo, ataques de texto conhecido).
- **Status atual**: Descontinuado oficialmente pelo NIST em 2023.

---

### **5. AES (Advanced Encryption Standard)**

- **Descrição**: Algoritmo de cifragem simétrica que substituiu o DES/3DES como padrão em 2001.
- **Funcionamento**:
    - Baseado na cifra Rijndael.
    - Opera em **blocos de 128 bits**, com chaves de 128, 192 ou 256 bits.
    - Realiza 10, 12 ou 14 rodadas de operações, incluindo substituição (SubBytes), permutação (ShiftRows), mistura (MixColumns) e chave XOR (AddRoundKey).
- **Propriedades**:
    - Alta segurança e resistência contra ataques modernos, como análise diferencial ou de chave-relacionada.
    - Projetado para ser eficiente em hardware e software.
- **Uso**:
    - Amplamente adotado em protocolos de segurança (e.g., TLS, VPNs, criptografia de discos e dispositivos móveis).
- **Status**: Padrão global para cifragem simétrica.

---

### **6. LFSP (Linear Feedback Shift Register - Pseudo-Random)**

- **Descrição**: Um gerador de sequências pseudoaleatórias baseado em registradores de deslocamento com feedback linear.
- **Funcionamento**:
    - Um registro binário de tamanho n gera a próxima saída com base em valores anteriores e uma função de feedback.
        
        nn
        
    - Sequência periódica com bom desempenho estatístico.
- **Propriedades**:
    - Simples e eficiente em hardware.
    - Usado em cifras de fluxo e sistemas de comunicação (e.g., geração de chaves de sessão).
- **Problemas**:
    - **Inseguro para criptografia**: Se o estado interno for descoberto, as próximas saídas podem ser previstas.
- **Uso moderno**: Aplicações limitadas a sistemas onde segurança não é a prioridade principal.

---

### **7. PRG (Pseudo-Random Generator)**

- **Descrição**: Um algoritmo que expande uma semente curta em uma sequência de bits pseudoaleatórios, com aparência indistinguível de aleatórios.
- **Propriedades**:
    - Indistinguibilidade: Um PRG seguro torna suas saídas imprevisíveis.
    - Base em problemas difíceis (e.g., RSA, curvas elípticas) para segurança criptográfica.
- **Usos**:
    - Geração de chaves criptográficas.
    - Algoritmos de cifra de fluxo e protocolos de segurança.
- **Exemplo seguro**:
    - PRG baseados em AES ou funções hash modernas (SHA-256).
- **Status**: Fundamental para criptografia moderna.
 
 ------------------------------------------------------------------------
  </details>
 
  <details>	
 <summary><b> Week 2 </b></summary> 

week 2
--------

Apresentamos uma nova primitiva chamada cifra de bloco que nos permitirá criar formas mais poderosas de criptografia. Examinaremos algumas construções clássicas de cifras de bloco (AES e 3DES) e veremos como usá-las para criptografia. As cifras de bloco são o cavalo de batalha da criptografia e têm muitas aplicações. Na próxima semana, veremos como usar cifras de bloco para fornecer integridade de dados. A tarefa opcional de programação desta semana pede que os alunos criem um sistema de criptografia/descriptografia usando o AES.

--------
   
<h3 align="center"> <a> CPA Security : Semantic Security for many-time key</a>  </h3>

<h3 align="center">Ciphers insecure under CPA </h3>

Quando temos uma mensagem criptografia uma única vez, dado a mesma mensagem criptografada duas vezes não é realmente seguro pois, podemos mandar a mesma mensagem criptografada duas vezes, quando vemos que a forma semântica é a mesma, vemos que a forma semântica m1 e m2 semântica serão iguais, sabendo a forma que é a criptografia e descobrindo a mensagem secreta. Porque com o mesmo conteúdo nesses dois arquivos.

![image.png](https://i.imgur.com/A8up6Vw.png)

**Solution 1: Encriptação randomica:**

Uma forma que poderia ser abordada para resolver o problema de uma criptografia única seria a randomização dos caracteres criptografados.

Onde um algoritmo cifrado, será movido todo o texto para uma bola cheia de caracteres aleatórios com mensagens aleatórias, fazendo com o que o texto cifrado tenha o tamanho maior que o texto normal e não cifrado, fazendo com que texto simples tinha tenha o espaço maior de bits, fazendo com que por exemplo se o texto simples (não cifrado) tenha por volta de 128bits, o texto cifrado tenha que adicionar 128bits extras. o texto cifrado com o dobro do tamanho total do texto.

Portanto dessa forma a probabilidade da mesma mensagem cifrada mostrar textos diferentes é bem maior.

Então a criptografia randômica é uma boa solução mas em alguns casos ela realmente apresenta alguns custos.

![image.png](https://i.imgur.com/zGEIsWN.png)

**Solution 2: nonce-based Encryption:**

 Nonce é um valor publico, o adversário tem acesso a essa ao valor nonce, mas toda vez que for passada uma mensagem será escolhida um novo nonce para essa mensagem. ela não precisa sem segura e nem aleatória. O único requsito que o nonce tem que ser EXCLUSIVO. 

Um valor único que não pode ser repetir.

Um exemplo seria no protocolo http que por meio de um mecanismo de transporte confiável, que o pacotes enviados pelo remetente são considerados recebidos em ordem de destinatário. Portanto, se o remetente envia o pacote #5 e depois o pacote #6, o destinatário receberá o pacote o pacote #5 e em seguida o pacote #6 nessa ordem. Mostrando que teve mantida a ordem. 

Fazendo com que nesse caso não faça sentido incluir o nonce nos pacotes, porque o nonce está implícito entre os dois lados.

Ao contrario de por exemplo o protocolo Isec, que não garante a ordem de entrega dos pacotes, fazendo com que você possa receber o pacote #6 antes do pacote #5. Nsse caso, ainda é bom usar um contador de pacotes como nonce. mas agora o nonce precisa ser incluído no pacote para que o destinatário saiba qual nonce usar para descriptografar o pacote recebido.

Basicamente a criptografia baseada em nonce é uma maneira muito eficiente de obter segurança de CPA. Em particular, se o nonce estiber implícito, ele nem mesmo aumenta o tamanho do texto cifrado.

Nesse modo seria muito util na utilização de vários dispositivos, pode eu poderia ter dois dispositivos em lugares diferentes compartilhando a mesma mensagem, mas com crifras de nonce COMPLETAMENTE DIFERENTES, como em um laptop e um celular compatilhando a mesma mensagem mas com criptografias distintas uma da outra.

O NONCE SEMPRE VAI SER EXCLUSIVO.

<h3 align="center"> <a>CBC: Encadeamento de blocos de cifra. </a> </h3>

O encadeamento de blocos de cifra usa uma cifra de bloco para escolher a segurança do texto simples, em particular com o blocos de cifras aleatórios IVeX 

Utilizando o bloco cifrado na primeira cifra de bloco para passar uma mascara com os dois juntos para o segundo bloco de cifra e assim por diante, ate a 3 camada de m[3]

![image.png](https://i.imgur.com/bHkZwfx.png)

E o texto cifrado final será essencialmente o IV, o IV inical que escolhemos junto com todos os blocos de texto cifrado. Devo dizer que IV significa Vetor de Inicialização.

<h3 align="center"> <a>CBC: CPA Analysis </a> </h3>

No CBC, cada bloco cifrado é influenciado pelo bloco anterior e pelo vetor de inicialização (IV). Porém, se o IV for previsível ou reutilizado, o modo CBC pode se tornar vulnerável a ataques CPA. O atacante pode explorar a relação entre blocos de texto simples e cifrado para inferir informações sobre a chave ou os dados originais.

Tendo que ser muito muito muito meno que o valor de X. para descobrir o valor.

**CBC Não pode ser previsível, o invasor pode prever que o IV não é seguro para CPA**

![image.png](https://i.imgur.com/kSeXBoK.png)

An Exemple Crypto API (OpenSSL)

![image.png](https://i.imgur.com/xFAIjzg.png)

Muito importante que o programador saiba que isso precisa ser feito, caso contrário, a criptografia CBC é insegura. Um último detalhe técnico sobre CBC é o que fazer quando a mensagem não é um múltiplo do comprimento do bloco de cifra de bloco? Isso é o que fazemos se o último bloco de mensagem for menor que o comprimento do bloco AES, por exemplo? Então, o último bloco de mensagem tem menos de dezesseis bytes. E a resposta é se adicionarmos um pad ao último bloco para que ele fique com dezesseis bytes, tão longo quanto o tamanho do bloco AES. 
 Onde em um campo que você prencher 5 bytes com string de 55555 cada byte terá o valor de 5 em cada byte.
  Esse exemplo acontecer um problema quanto tiver 16 bytes
  
(copiei pq não entendiporranhumaaqui)<br>
Então suponha que o valor seja cinco, então ele simplesmente remove os últimos cinco bytes da mensagem. Agora a questão é o que fazemos se de fato a mensagem for um múltiplo de dezesseis bytes, então de fato nenhum preenchimento é necessário? Se não preenchermos nada, bem, isso é um problema porque o decifrador vai olhar para o último byte do último bloco que não faz parte da mensagem real e ele vai remover essa quantidade de bytes do texto simples. Então isso realmente seria um problema. Então a solução é, se de fato não houver nenhum preenchimento necessário, ainda assim temos que adicionar um bloco fictício. E já que adicionamos o bloco fictício, este seria um bloco que basicamente contém dezesseis bytes, cada um contendo o número dezesseis. Ok, então adicionamos essencialmente dezesseis blocos fictícios. O decifrador, que quando ele está decifrando, ele olha para o último byte do último bloco, ele vê que o valor é dezesseis, portanto ele remove o bloco inteiro. E o que sobra é o texto simples real. Então é um pouco lamentável que, de fato, se você estiver criptografando mensagens curtas com CBC e as mensagens tiverem, digamos, 32 bytes, então elas são um múltiplo de dezesseis bytes, então você tem que adicionar mais um bloco e fazer todos esses textos cifrados terem 48 bytes apenas para acomodar o preenchimento do CBC. Devo mencionar que há uma variante do CBC chamada CBC com roubo de texto cifrado que realmente evita esse problema.

Construction 2: Rand crt-mode

<h3 align="center"> <a>Randomized Counter Mode (CTR):</a> </h3>

![image.png](https://i.imgur.com/bx9KJRy.png)

É um modo de cifra de blocos que utiliza uma **PRF (Função Pseudoaleatória)** em vez de uma **PRP (Permutação Pseudoaleatória)**, tornando-o mais flexível que o CBC. No CTR, um vetor de inicialização (IV) aleatório é escolhido para cada mensagem. Este IV serve como base para gerar um "contador" que cifra os blocos da mensagem através de uma operação XOR com o resultado da função PRF.

**Principais Vantagens do CTR sobre o CBC:**

1. **Paralelização:**
    - CTR é totalmente paralelizável, permitindo a criptografia simultânea de blocos.
    - CBC é sequencial, dificultando o uso eficiente de hardware.
2. **Eficiência:**
    - Dispensa a operação de decriptação, utilizando apenas a PRF no sentido direto.
    - Compatível com primitivas como Salsa20 (uma PRF, não uma PRP).
3. **Segurança Aprimorada:**
    - CTR permite criptografar mais blocos com a mesma chave antes de comprometer a segurança, em comparação ao CBC.
    - CBC exige maior cautela na reutilização de chaves devido a parâmetros mais restritivos.
4. **Ausência de Problemas de Preenchimento:**
    - CBC requer a adição de blocos extras (dummy blocks) para mensagens que são múltiplos do tamanho do bloco.
    - CTR não enfrenta esse problema.
5. **Menor Expansão do Texto Cifrado:**
    - Em fluxos de mensagens pequenas, CBC expande significativamente o texto cifrado.
    - CTR mantém o tamanho do texto cifrado proporcional ao texto plano.

**Limitações de Ambos os Modos:**

- Tanto CBC quanto CTR garantem apenas confidencialidade, não fornecendo integridade.
- Para proteção contra adulterações, devem ser combinados com mecanismos de integridade, como autenticação criptográfica.

**Conclusão:**

O modo CTR supera o CBC em diversos aspectos cruciais: paralelização, segurança, eficiência e flexibilidade. Por isso, é amplamente recomendado em sistemas modernos. No entanto, ambos os modos devem ser complementados com mecanismos que garantam integridade para mitigar vulnerabilidades em cenários práticos.




 -----------------------------------------------------------------------------------------------------------------------------------------------
</details> 

<details>	
 <summary><b> Week 3 </b> </b></summary> 
 
week 3
--------
O tópico desta semana é a integridade dos dados. Discutiremos várias construções clássicas para sistemas MAC que são usadas para garantir a integridade dos dados. Por enquanto, discutiremos apenas como evitar a modificação de dados não secretos. Na próxima semana, voltaremos à criptografia e mostraremos como fornecer confidencialidade e integridade. O projeto de programação desta semana mostra como autenticar grandes arquivos de vídeo. Mesmo que o senhor não faça o projeto, leia a descrição do projeto - ele ensina um conceito importante chamado cadeia de hash.

--------
Um exemplo os arquivos do nosso disco no nosso Windows, que não são protegidos pois não tem problemas de confidencialidade ou em proteção de banners web onde eles também não tem medo de poderem copiar ou baixar as imagens no site… sem problemas de confidencialidade.

Mas existe outro caso MAC’s para fornecer integridade em mensagens, um código de autenticação que tem uma chave compartilhada entre ambos, onde com a mensagem gerada pelos dois junto com a tag de bob verifica se o valor vai ser “sim” ou “não”
![image.png](https://i.imgur.com/zFAvsLC.png)

Então considerando CRC, CRC é significa verifição de redundância cíclica. é mandada entro da tag de alice e mandada para a tag de bob para ver se o valor é correto ou não.

O problema desse modelo é que é muito facil para um atacante bloquear essa mensagem, e atacar emcima dela, só indo na mensagem m e tag que ela está completamente bloqueada (mesmo que ela esteja completamente encriptada, mas vai ser bloqueada) fazendo com que seja protegida por detecção de ataques randômicos mas não de ataques maliciosos. 

E nosso objetivo é garantir integridade até mesmo um atacante mal-intencionado não possa modificar as mensagens no caminho entre os dois.

Um chamado “Ataque de mensagem escolhida” que basicamente, Alice manda uma mensagem e quando enviada envia a tag junto com a mensagem fazendo com que ela envie as tag’s recebidas e manda para o atacante 

(Exemplo: Alice recebe um email, talvez Alice queria salvar o e-mail no disco , então ela computara a tag no disco , e ele peça para mandar mais informações, fazendo com que alice mande a sua tag junto com a tag do atacante que estava computavel no disco.

Esse caso dificuldade a criptografia da chave secreta aleatória. fazendo com que faça uma chave secreta errada.

A proteção de arquivos no sistema também é parecido com essa ideia, onde cada arquivo é seguro com uma tag, mas caso a maquina foi infectada as tag’s são modificadas em cada arquivo, fazendo com que o arquivo possa criar chaves validas em arquivos criados por ele mesmo, sem que o computador detecte essa invalidade pois ele é um programa valido pelo proprio dispositivo. 

Mas para contornar isso, precisar dar um reboot no sistema, e verificar o mac de cada arquivo, se ver que não tem tags validas o usuário detectará todos os arquivos que foram modificados pelo vírus. 

(o virus pode trocar os arquivos também, fazer com que um arquivo original seja copiado pelo virus, mas na verdade o arquivo original ser o arquivo detectado como viruse o virus ser o arquivo falando ser o orignal)

![image.png](https://i.imgur.com/a1MjkTN.png)

Os **Message Authentication Codes (MACs)** baseados em **Pseudo-Random Functions (PRFs)** são mecanismos criptográficos que garantem a integridade e autenticidade de mensagens. Esses MACs utilizam as propriedades das PRFs para gerar valores de autenticação difíceis de falsificar.

### Estrutura básica

Um MAC baseado em PRF funciona da seguinte forma:

1. Uma função PRF é usada como base, representada por Fk(x), onde:Fk(x)
    - k é uma chave secreta.
    - x é o valor de entrada (geralmente a mensagem ou uma transformação dela).
2. O MAC é gerado como MAC(k,m) = Fk(m), onde:MAC(k,m) = Fk(m)
    - k é a chave secreta compartilhada.
    - m é a mensagem que se deseja autenticar.

### Características principais

- **Integridade**: Um adversário não pode modificar a mensagem sem que o receptor perceba, pois a alteração resultaria em um MAC inválido.
- **Autenticidade**: Apenas quem conhece a chave secreta pode gerar o MAC correto para uma mensagem específica.
- **Segurança baseada na PRF**: A segurança do MAC depende da qualidade da PRF. Uma PRF bem projetada torna difícil para um adversário distinguir suas saídas de números verdadeiramente aleatórios.

### Vantagens dos MACs baseados em PRFs

1. **Eficiência computacional**: PRFs, como aquelas baseadas em construções de cifragem (por exemplo, AES), são rápidas e eficientes para aplicações práticas.
2. **Flexibilidade**: Podem ser aplicados a mensagens de tamanhos variados, geralmente usando técnicas como preenchimento ou divisão da mensagem em blocos.
3. **Segurança comprovada**: A segurança é formalmente analisada e está ligada à robustez da PRF subjacente.

### Exemplos práticos

Um exemplo comum de MAC baseado em PRF é o **HMAC (Hash-based Message Authentication Code)**. Ele utiliza uma função de hash criptográfica como PRF, combinando eficiência e segurança. A fórmula básica do HMAC é:

HMAC(k,m) = Hash((k ⊕ ipad) ∥ Hash((k ⊕ opad) ∥ m))

Onde:

- ⊕ é a operação XOR.
- ipad e opad são constantes específicas.
- Hash é uma função hash como SHA-256.

Esse tipo de MAC é amplamente usado em protocolos de segurança, como SSL/TLS, IPSec e outros.

**CBC-MAC:** 

tem uma simularidade muito grande com o AES, fazendo uma cifra por bloco, passando para cada matrix e criptando novamente.
![image](https://github.com/user-attachments/assets/d11e08d7-02c1-43bd-a169-b84d45826145)

Sendo no final uma chave independente F(k1) passando a tag depois disso tudo.

Fazendo com que o CBC-MAC seja seguro para mensagens de comprimento fixo, mas não é adequado para comprimentos variáveis sem modificações adicionais. Para aplicações práticas modernas, é recomendado o uso de **CMAC** ou outros esquemas de autenticação, como HMAC, que são mais robustos e seguros contra ataques conhecidos.

**NMAC:** 

Utiliza de uma forma um pouco diferente, a criptografia funciona onde os blocos criptografam a chave que está na função F passando pro cada bloco de M onde no final T que é a parte mais inidentificável do modelo NMAC, não sendo um mac muito seguro pois não conseguimos mapear este elemento T.

Um sistema de criptografia feita em cascata.
![image](https://github.com/user-attachments/assets/48a87ffc-1f5c-429d-9033-1629006585a8)

O **PMAC (Parallelizable Message Authentication Code)** e o **Carter-Wegman MAC** são métodos para gerar códigos de autenticação de mensagens (MACs), garantindo a integridade e autenticidade dos dados. Eis um resumo de ambos:

---

### **PMAC (Parallelizable Message Authentication Code)**

- **Definição**: Construção de MAC projetada para alta eficiência e paralelização.
- **Funcionamento**:
    1. Processa blocos de dados simultaneamente.
    2. Utiliza um cifrador de bloco (ex: AES) em modo especial para gerar o código de autenticação.
    3. Processa cada bloco independentemente, facilitando a execução paralela.
- **Vantagens**:
    - Ideal para sistemas modernos com suporte à computação paralela.
    - Oferece alta eficiência sem comprometer a segurança.
- **Aplicações**: Comum em sistemas que processam grandes volumes de dados rapidamente.

---

### **Carter-Wegman MAC**

- **Definição**: Técnica que combina hashing universal com criptografia para gerar MACs seguros.
- **Funcionamento**:
    1. Usa uma função de hashing universal para mapear a mensagem em um valor hash.
    2. Criptografa esse valor com uma chave secreta, gerando o MAC.
- **História**: Proposto por Carter e Wegman em 1981 como método eficiente de autenticação de mensagens.
- **Vantagens**:
    - Alta eficiência computacional.
    - Resistência a ataques de força bruta devido ao hashing universal.
- **Aplicações**: Usado em protocolos de rede e sistemas que priorizam eficiência e segurança.

---

### **Comparação**

| Característica | PMAC | Carter-Wegman MAC |
| --- | --- | --- |
| **Eficiência** | Alta, especialmente com paralelismo | Alta, devido ao uso de hashing |
| **Complexidade** | Relativamente mais complexo | Mais simples de implementar |
| **Uso** | Sistemas modernos e paralelos | Protocolos de rede e sistemas gerais |

Ambos os métodos têm características distintas e são aplicáveis conforme as necessidades de desempenho, segurança e simplicidade do sistema.

O **Generic Birthday Attack** é um conceito fundamental na criptografia relacionado ao **paradoxo do aniversário**. Ele explora a probabilidade de encontrar colisões em funções hash ou em outros contextos matemáticos. Eis um resumo:

---

### **Definição**

O Generic Birthday Attack é uma abordagem genérica, não específica de algoritmos, que busca encontrar colisões em funções hash ou problemas relacionados. Baseia-se na ideia de que, em um conjunto suficientemente grande, as chances de duas entradas diferentes gerarem o mesmo resultado (colisão) aumentam significativamente devido ao paradoxo do aniversário.

---

### **Funcionamento**

- Para uma função hash de comprimento n bits:n
    - A busca por colisões tem complexidade **O(2^(n/2))**, e não O(2^n), devido ao aumento exponencial da probabilidade de colisão conforme o número de entradas cresce.
        
        O(2^n)
        
    - O ataque envolve a geração de várias entradas e a comparação dos valores hash resultantes.
- Consiste em criar pares e verificar se há alguma repetição (colisão).

---

### **Exemplo**

- Considere uma função hash de 128 bits:
    - Embora haja 2^128 possibilidades únicas, o Generic Birthday Attack permite encontrar colisões com cerca de 2^64 tentativas, significativamente menos que uma busca exaustiva.
        
        2^128
        
        2^64
        

---

### **Implicações na Criptografia**

1. **Segurança de Funções Hash**:
    - Funções hash modernas (como SHA-256) são projetadas para resistir a esses ataques, garantindo comprimentos suficientemente grandes para n.
        
        n
        
    - O comprimento do hash deve ser o dobro da segurança desejada (por exemplo, para 128 bits de segurança, usam-se hashes de 256 bits).
2. **Certificados Digitais e Assinaturas**:
    - A resistência a colisões é crucial para evitar fraudes, como a falsificação de assinaturas digitais ou certificados.

---

### **Conclusão**

O Generic Birthday Attack não explora fraquezas específicas de uma função, mas sim uma propriedade estatística universal. Para resistir a ele, funções hash e algoritmos criptográficos devem ser projetados com tamanhos de chave e hash adequados, garantindo segurança contra colisões probabilísticas.

(foi de gepeto mesmo, minha tia não estava me deixando fazer)
 
-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

  <details>	
 <summary><b> Week 4</b> </b></summary> 
   
 week 4
 --------
 O tópico desta semana é criptografia autenticada: métodos de criptografia que garantem tanto a confidencialidade quanto a integridade. Também discutiremos alguns pontos importantes, como a forma de pesquisar dados criptografados. Esta é a nossa última semana de estudo  da criptografia simétrica. Na próxima semana, começaremos com o gerenciamento de chaves e a criptografia de chave pública. Como de costume, há também um projeto de programação de crédito extra. O projeto desta semana envolve um pouco de rede para experimentar um        ataque de texto cifrado escolhido em um site de brinquedo.
 
 --------
 ![image.png](https://i.imgur.com/qdRj6Ty.png)

Nesse exemplo vemos como seria o trafego de um sistema na internetem TCP/IP, passando o packet para o serv, e distribuindo para as respectivas portas.

![image.png](https://i.imgur.com/INe5NNO.png)

Neste exemplo vemos que o IPsec é mais seguro, pois o packet com uma chave, manda a mensagem criptografada com a chave pro serv, quanto o data desencripta a mensagem ai sendo transferida para a porta=80.

Passando para bob a mensagem correta.

Então agora gostaria de mostrar que sem integridade, nesta configuração, não podemos alcançar nenhuma forma de confidencialidade. 

![image.png](https://i.imgur.com/qAuv1PZ.png)

Pois quando caso um atacante intercepte a mensagem encaminhada para o webserver pode ser mudado para a porta de destino para bob, fazendo com que mensagens do server vai para o caminho errado e compartilhando prováveis informações sigilosas. ]

Vimos 2 exemplos que mostram como dois ataques ativos podem destruir completamente a criptografia segura do CPA.

**Authenticated Encryption**

**Authenticated Encryption (AE)** é uma abordagem criptográfica que combina duas funções fundamentais em uma única operação: **confidencialidade** e **autenticidade**. O objetivo principal do AE é garantir que os dados transmitidos ou armazenados não apenas permaneçam confidenciais (protegidos contra acesso não autorizado), mas também sejam autenticamente verificados (protegidos contra alterações não autorizadas).

![image.png](https://i.imgur.com/kEbOdMb.png)

Duas copias CCA game:

O termo "CCA" refere-se a "Chosen-Ciphertext Attack" (Ataque por Texto Cifrado Escolhido), um modelo de ataque na criptografia onde o atacante pode escolher textos cifrados específicos e obter suas respectivas decifrações. O objetivo é reunir informações que permitam deduzir a chave secreta ou comprometer a segurança do sistema criptográfico.

Existem duas principais variantes desse ataque:

1. **CCA1 (Ataque por Texto Cifrado Escolhido Não Adaptativo)**: O atacante escolhe um conjunto de textos cifrados para serem decifrados antes de receber o texto cifrado alvo. Após obter as decifrações desses textos, o atacante tenta inferir informações sobre o texto cifrado alvo, sem a possibilidade de realizar novas consultas de decifração após essa etapa.
2. **CCA2 (Ataque por Texto Cifrado Escolhido Adaptativo)**: Nesta variante mais poderosa, o atacante pode continuar a escolher e decifrar textos cifrados mesmo após receber o texto cifrado alvo, com a restrição de não consultar a decifração do próprio texto cifrado alvo. Essa capacidade adaptativa torna o ataque mais eficaz e representa um desafio maior para a segurança dos sistemas criptográficos.

Para proteger sistemas contra ataques CCA, é essencial utilizar esquemas de criptografia que ofereçam segurança comprovada contra esses tipos de ataques. Por exemplo, o esquema Cramer-Shoup é conhecido por ser seguro contra ataques CCA2.

Além disso, a implementação de medidas como a autenticação de mensagens pode ajudar a prevenir ataques CCA, garantindo que qualquer modificação não autorizada nos textos cifrados seja detectada.

Em resumo, os ataques CCA destacam a importância de desenvolver e implementar sistemas criptográficos robustos que resistam a adversários capazes de manipular e decifrar textos cifrados escolhidos, assegurando a confidencialidade e integridade das informações.

Agora vamos apresentar 3 exemplos

![image.png](https://i.imgur.com/epdh0Ra.png)

No exemplo SSL:  (Mac-then-Encrypt)

A forma como o SSL combina criptografia e MAC na esperança de obter criptografia autenticada, é basicamente, você pega o texto simples, ele passa antes um criptografia tag, no final passando a mensagem criptografada com a tag e descriptografa.

No exemplo IPsec: (Encrypt,then-mac)

( No exemplo manda um texto simples, é criptografada no inicio antes de ir, e é entregue para a tag com a mensagem criptografada.

No exemplo SSH: (encrypt-and-mac)

 é bem semelhante ao IPsec, mas a diferença é que a mensagem é computada no final com a tag, é não pelo texto criptografado.

### **1. GCM (Galois/Counter Mode)**

- **Tipo**: Modo autenticado de cifra.
- **Características**:
    - Combina confidencialidade e autenticidade.
    - Baseado no modo de contador (CTR) para criptografia.
    - Utiliza um código de autenticação universal de Galois (GHASH) para verificar a integridade e autenticidade.
- **Vantagens**:
    - Extremamente rápido, adequado para hardware e software.
    - Permite paralelismo eficiente.
- **Limitações**:
    - Vulnerável a reutilização do mesmo IV (vetor de inicialização) com a mesma chave, o que compromete segurança.
- **Usos**:
    - HTTPS, VPNs, protocolos de segurança de rede.

---

### **2. CCM (Counter with CBC-MAC)**

- **Tipo**: Modo autenticado de cifra.
- **Características**:
    - Combina CTR para criptografia e CBC-MAC para autenticação.
    - Funciona em blocos.
    - Requer que a cifra seja executada duas vezes: uma para criptografia e outra para autenticação.
- **Vantagens**:
    - Simplicidade e compatibilidade com implementações AES existentes.
    - É determinístico, útil para ambientes sensíveis à sincronização.
- **Limitações**:
    - Mais lento que GCM devido ao uso de CBC-MAC e processamento sequencial.
    - Não suporta paralelismo eficiente.
- **Usos**:
    - Ideal para sistemas embarcados e aplicações IoT (Internet das Coisas).

---

### **3. EAX (Encrypt-then-MAC Mode)**

- **Tipo**: Modo autenticado de cifra.
- **Características**:
    - Segue o paradigma **Encrypt-then-MAC**: primeiro criptografa os dados e, em seguida, calcula a autenticação.
    - Combina CTR para criptografia e CMAC para autenticação.
- **Vantagens**:
    - Flexível e altamente seguro devido à separação clara entre criptografia e autenticação.
    - Suporte a mensagens de comprimento variável.
- **Limitações**:
    - Desempenho inferior ao GCM em cenários de alta velocidade.
    - Requer múltiplas chamadas para a cifra subjacente (uma para CMAC e outra para CTR).
- **Usos**:
    - Aplicações onde a segurança e flexibilidade são mais críticas do que o desempenho bruto.

---

### Comparação Geral:

| Característica | **GCM** | **CCM** | **EAX** |
| --- | --- | --- | --- |
| **Velocidade** | Alta | Média | Média |
| **Paralelismo** | Sim | Não | Parcial |
| **Flexibilidade** | Alta | Baixa | Alta |
| **Complexidade** | Média | Baixa | Média |
| **Uso de IV Único** | Fundamental | Importante | Importante |

### **TLS (Transport Layer Security)**

O **TLS** é um protocolo criptográfico amplamente utilizado para garantir **segurança** e **privacidade** em comunicações digitais, especialmente na internet.

---

### **Objetivos principais:**

1. **Confidencialidade**: Garantir que as informações trocadas não sejam acessíveis por terceiros.
2. **Integridade**: Assegurar que os dados não sejam alterados durante a transmissão.
3. **Autenticação**: Verificar a identidade das partes envolvidas na comunicação (como o cliente e o servidor).

---

### **Principais componentes:**

1. **Handshake Protocol**:
    - Etapa inicial onde cliente e servidor negociam:
        - Versão do protocolo.
        - Algoritmos criptográficos.
        - Troca de chaves para estabelecer um canal seguro.
    - Pode incluir autenticação mútua (geralmente apenas o servidor é autenticado via certificado).
2. **Registro de Dados (Record Protocol)**:
    - Define como os dados são fragmentados, comprimidos, criptografados e autenticados antes de serem enviados.
3. **Alert Protocol**:
    - Utilizado para comunicação de erros ou alertas entre cliente e servidor.
4. **Change Cipher Spec Protocol**:
    - Sinaliza a troca de parâmetros de criptografia durante a conexão.

---

### **Principais versões:**

1. **TLS 1.0 e 1.1**:
    - Obsoletos devido a vulnerabilidades e métodos de criptografia ultrapassados.
2. **TLS 1.2**:
    - Introduziu maior flexibilidade na escolha de algoritmos de criptografia.
    - Suporta AEAD (Authenticated Encryption with Associated Data), como GCM.
    - Ainda amplamente usado.
3. **TLS 1.3** (atual):
    - Mais seguro e eficiente.
    - Removeu algoritmos inseguros (ex.: MD5, SHA-1, RC4).
    - Melhorou a performance reduzindo o número de round trips no handshake.

---

### **Principais algoritmos usados em TLS:**

1. **Criptografia de Chave Pública**:
    - RSA, Diffie-Hellman, ECDH.
2. **Assinaturas Digitais**:
    - RSA, ECDSA.
3. **Criptografia Simétrica**:
    - AES (com GCM ou CBC), ChaCha20.
4. **Funções Hash**:
    - SHA-256, SHA-384.

---

### **Fluxo típico de uma conexão TLS**:

1. **Handshake**:
    - Cliente e servidor negociam parâmetros de criptografia.
    - O servidor envia seu certificado para autenticação.
    - Chaves são trocadas e geradas.
2. **Estabelecimento de Sessão**:
    - Um canal seguro é configurado.
3. **Transferência de Dados**:
    - Os dados são criptografados e transmitidos.
4. **Encerramento**:
    - As partes encerram a conexão de forma segura.

---

### **Usos comuns do TLS:**

- **HTTPS**: Proteger sites e aplicativos web.
- **E-mail**: SMTP, IMAP e POP3 seguros.
- **VPNs**: Garantir segurança em conexões remotas.
- **Outros protocolos**: FTPS, XMPP, entre outros.

O **TLS** é fundamental para a segurança digital moderna. O uso da versão mais recente (**TLS 1.3**) é recomendado para aproveitar melhor desempenho e maior segurança.

-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

<details>	
 <summary><b> Week 5 </b> </b></summary> 
 
week 5
--------
O tópico desta semana é a troca básica de chaves: como configurar uma chave secreta entre duas partes. Por enquanto, consideramos apenas protocolos seguros contra espionagem. Essa pergunta motiva os principais conceitos de criptografia de chave pública, mas antes de criarmos sistemas de chave pública, precisamos fazer um breve desvio e abordar alguns conceitos básicos da teoria dos números computacionais. Começaremos com algoritmos que remontam à antiguidade (Euclides) e chegaremos até Fermat, Euler e Legendre. Também mencionaremos de passagem alguns conceitos úteis da matemática do século XX. Na próxima semana, faremos bom uso do nosso trabalho árduo desta semana e construiremos vários sistemas de criptografia de chave pública.

--------
 
-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

  <details>	
 <summary><b> Week 6 </b> </b></summary> 
   
 
--------
O tópico desta semana é a criptografia de chave pública: como criptografar usando uma chave pública e descriptografar usando uma chave secreta. A criptografia de chave pública é usada para o gerenciamento de chaves em sistemas de arquivos criptografados, em sistemas de mensagens criptografadas e para muitas outras tarefas. Os vídeos abrangem duas famílias de sistemas de criptografia de chave pública: uma baseada em funções de alçapão (RSA em particular) e outra baseada no protocolo Diffie-Hellman. Construímos sistemas que são seguros contra adulteração, também conhecidos como segurança de texto cifrado escolhido (segurança CCA). Houve uma grande quantidade de pesquisas sobre segurança CCA na última década e, dado o tempo alocado, podemos apenas resumir os principais resultados dos últimos anos. As aulas contêm sugestões de leituras adicionais para os interessados em saber mais sobre sistemas de chave pública com segurança CCA. O conjunto de problemas desta semana envolve um pouco mais de matemática do que o normal, mas deve expandir seu conhecimento sobre criptografia de chave pública. Por favor, não se acanhe em postar perguntas no fórum. Esta é a última semana do curso Crypto I. Espero que todos tenham aprendido muito e aproveitado o material. A criptografia é um belo tópico com muitos problemas em aberto e espaço para mais pesquisas. Espero vê-los em Crypto II, onde abordaremos outros tópicos básicos e alguns tópicos mais avançados.


--------


-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

<details>	
 <summary><b> Certificate </b> </b></summary> 
 
Certificado
--------
![image](https://github.com/user-attachments/assets/54359617-9b21-4d8f-9fb7-d2b6905bdf7a)



-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

----------------------------


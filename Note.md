 <h1 align="center">Notes </a> </h1>

  <h2 align="center"> Some pessoal week notes <br> in Portuguese</h2> 


<details>	
 <summary><b> Week 1 </b> </b></summary> 

 week 1
 --------
 O tópico desta semana é uma visão geral do que é a criptografia, bem como nosso primeiro exemplo de cifras. Os senhores aprenderão sobre pseudoaleatoriedade e como usá-la para criptografia. Também veremos algumas definições básicas de criptografia segura.

 --------
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
 
-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

  <details>	
 <summary><b> Week 4</b> </b></summary> 
   
 week 4
 --------
 O tópico desta semana é criptografia autenticada: métodos de criptografia que garantem tanto a confidencialidade quanto a integridade. Também discutiremos alguns pontos importantes, como a forma de pesquisar dados criptografados. Esta é a nossa última semana de estudo  da criptografia simétrica. Na próxima semana, começaremos com o gerenciamento de chaves e a criptografia de chave pública. Como de costume, há também um projeto de programação de crédito extra. O projeto desta semana envolve um pouco de rede para experimentar um        ataque de texto cifrado escolhido em um site de brinquedo.
 
 --------

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
   
week 6
--------
O tópico desta semana é a criptografia de chave pública: como criptografar usando uma chave pública e descriptografar usando uma chave secreta. A criptografia de chave pública é usada para o gerenciamento de chaves em sistemas de arquivos criptografados, em sistemas de mensagens criptografadas e para muitas outras tarefas. Os vídeos abrangem duas famílias de sistemas de criptografia de chave pública: uma baseada em funções de alçapão (RSA em particular) e outra baseada no protocolo Diffie-Hellman. Construímos sistemas que são seguros contra adulteração, também conhecidos como segurança de texto cifrado escolhido (segurança CCA). Houve uma grande quantidade de pesquisas sobre segurança CCA na última década e, dado o tempo alocado, podemos apenas resumir os principais resultados dos últimos anos. As aulas contêm sugestões de leituras adicionais para os interessados em saber mais sobre sistemas de chave pública com segurança CCA. O conjunto de problemas desta semana envolve um pouco mais de matemática do que o normal, mas deve expandir seu conhecimento sobre criptografia de chave pública. Por favor, não se acanhe em postar perguntas no fórum. Esta é a última semana do curso Crypto I. Espero que todos tenham aprendido muito e aproveitado o material. A criptografia é um belo tópico com muitos problemas em aberto e espaço para mais pesquisas. Espero vê-los em Crypto II, onde abordaremos outros tópicos básicos e alguns tópicos mais avançados.


--------


-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

<details>	
 <summary><b> Week 7 </b> </b></summary> 
 
week 7
--------
Parabéns! Chegamos ao final do curso. Este módulo contém apenas o exame final que abrange todo o curso. Espero que todos tenham aprendido muito durante essas 6 semanas. Boa sorte no exame final e espero vê-lo em um curso futuro!

--------

-----------------------------------------------------------------------------------------------------------------------------------------------
  </details>

----------------------------


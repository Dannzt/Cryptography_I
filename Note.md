 <h1 align="center">Notes </a> </h1>
  <br>
  
CPA Security : Semantic Security for many-time key

Ciphers insecure under CPA

Quando temos uma mensagem criptografia uma única vez, dado a mesma mensagem criptografada duas vezes não é realmente seguro pois, podemos mandar a mesma mensagem criptografada duas vezes, quando vemos que a forma semântica é a mesma, vemos que a forma semântica m1 e m2 semântica serão iguais, sabendo a forma que é a criptografia e descobrindo a mensagem secreta. Porque com o mesmo conteúdo nesses dois arquivos.

![image.png](https://i.imgur.com/A8up6Vw.png)

Solution 1: Encriptação randomica:

Uma forma que poderia ser abordada para resolver o problema de uma criptografia única seria a randomização dos caracteres criptografados.

Onde um algoritmo cifrado, será movido todo o texto para uma bola cheia de caracteres aleatórios com mensagens aleatórias, fazendo com o que o texto cifrado tenha o tamanho maior que o texto normal e não cifrado, fazendo com que texto simples tinha tenha o espaço maior de bits, fazendo com que por exemplo se o texto simples (não cifrado) tenha por volta de 128bits, o texto cifrado tenha que adicionar 128bits extras. o texto cifrado com o dobro do tamanho total do texto.

Portanto dessa forma a probabilidade da mesma mensagem cifrada mostrar textos diferentes é bem maior.

Então a criptografia randômica é uma boa solução mas em alguns casos ela realmente apresenta alguns custos.

![image.png](https://i.imgur.com/zGEIsWN.png)

Solution 2: nonce-based Encryption:

 Nonce é um valor publico, o adversário tem acesso a essa ao valor nonce, mas toda vez que for passada uma mensagem será escolhida um novo nonce para essa mensagem. ela não precisa sem segura e nem aleatória. O único requsito que o nonce tem que ser EXCLUSIVO. 

Um valor único que não pode ser repetir.

Um exemplo seria no protocolo http que por meio de um mecanismo de transporte confiável, que o pacotes enviados pelo remetente são considerados recebidos em ordem de destinatário. Portanto, se o remetente envia o pacote #5 e depois o pacote #6, o destinatário receberá o pacote o pacote #5 e em seguida o pacote #6 nessa ordem. Mostrando que teve mantida a ordem. 

Fazendo com que nesse caso não faça sentido incluir o nonce nos pacotes, porque o nonce está implícito entre os dois lados.

Ao contrario de por exemplo o protocolo Isec, que não garante a ordem de entrega dos pacotes, fazendo com que você possa receber o pacote #6 antes do pacote #5. Nsse caso, ainda é bom usar um contador de pacotes como nonce. mas agora o nonce precisa ser incluído no pacote para que o destinatário saiba qual nonce usar para descriptografar o pacote recebido.

Basicamente a criptografia baseada em nonce é uma maneira muito eficiente de obter segurança de CPA. Em particular, se o nonce estiber implícito, ele nem mesmo aumenta o tamanho do texto cifrado.

Nesse modo seria muito util na utilização de vários dispositivos, pode eu poderia ter dois dispositivos em lugares diferentes compartilhando a mesma mensagem, mas com crifras de nonce COMPLETAMENTE DIFERENTES, como em um laptop e um celular compatilhando a mesma mensagem mas com criptografias distintas uma da outra.

O NONCE SEMPRE VAI SER EXCLUSIVO.

CBC: Encadeamento de blocos de cifra.

O encadeamento de blocos de cifra usa uma cifra de bloco para escolher a segurança do texto simples, em particular com o blocos de cifras aleatórios IVeX 

Utilizando o bloco cifrado na primeira cifra de bloco para passar uma mascara com os dois juntos para o segundo bloco de cifra e assim por diante, ate a 3 camada de m[3]

![image.png](https://i.imgur.com/bHkZwfx.png)

E o texto cifrado final será essencialmente o IV, o IV inical que escolhemos junto com todos os blocos de texto cifrado. Devo dizer que IV significa Vetor de Inicialização.

CBC: CPA Analysis

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


----------------------------


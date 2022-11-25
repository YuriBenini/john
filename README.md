[![Círculo CI](https://circleci.com/gh/openwall/john/tree/bleeding-jumbo.svg?style=shield)](https://circleci.com/gh/openwall/john/tree /sangramento-jumbo)
[![Downloads](https://img.shields.io/badge/Download-Windows%20Build-blue.svg)](https://github.com/openwall/john-packages/releases/tag/jumbo- dev)
[![Licença](https://img.shields.io/badge/License-GPL%20v2%2B-blue.svg)](https://github.com/openwall/john/blob/bleeding-jumbo/ documento/LICENÇA)
[![Search hit](https://img.shields.io/github/search/openwall/john/goto.svg?label=GitHub%20Hits)](https://github.com/search?utf8=% E2%9C%93&q=john%20the%20ripper&type=)

João, o Estripador
===============

Esta é a versão "jumbo" aprimorada pela comunidade de John, o Estripador.
Tem muito código, documentação e dados fornecidos pelo jumbo
desenvolvedores e a comunidade de usuários. É fácil adicionar um novo código
ao jumbo, e os requisitos de qualidade são baixos, embora ultimamente tenhamos
começou a submeter todas as contribuições a alguns testes automatizados.
Isso significa que você obtém muitas funcionalidades que não são necessariamente
"maduro", o que por sua vez significa que erros neste código são esperados.

A página inicial de John, o Estripador é:

https://www.openwall.com/john/

Se você tiver algum comentário sobre este lançamento ou sobre o JtR em geral, por favor
junte-se à lista de discussão john-users e poste lá:

https://www.openwall.com/lists/john-users/

Para contribuições para o jumbo de John the Ripper, use pull requests em
GitHub:

https://github.com/openwall/john/blob/bleeding-jumbo/CONTRIBUTING.md

Incluída abaixo está a documentação básica do núcleo de John the Ripper.

---

John, o cracker de senha do Estripador.

John the Ripper é um cracker de senha rápido, atualmente disponível para
muitos tipos de Unix, macOS, Windows, DOS, BeOS e OpenVMS (o último
requer um patch contribuído). Seu objetivo principal é detectar
Senhas Unix. Além de vários tipos de hash de senha crypt(3) mais
comumente encontrados em vários tipos de Unix, suportados fora da caixa são
Kerberos/AFS e hashes do Windows LM, bem como códigos de viagem baseados em DES, mais
centenas de hashes e cifras adicionais em versões "-jumbo".


Como instalar.

Consulte INSTALAR para obter informações sobre a instalação do John em seu sistema.


	Como usar.

Para executar o John, você precisa fornecer alguns arquivos de senha e
especifique opcionalmente um modo de cracking, como este, usando a ordem padrão
de modos e assumindo que "passwd" é uma cópia do seu arquivo de senha:

john passwd

ou, restringindo-o apenas ao modo wordlist, mas permitindo o uso
das regras de confusão de palavras:

john --wordlist=password.lst --rules passwd

Senhas quebradas serão impressas no terminal e salvas no
arquivo chamado $JOHN/john.pot (na documentação e no
arquivo de configuração para John, "$JOHN" refere-se a "casa" de John
diretório"; qual diretório realmente é depende de como você instalou
John). O arquivo $JOHN/john.pot também é usado para não carregar a senha
hashes que você já quebrou quando executou John na próxima vez.

Para recuperar as senhas quebradas, execute:

john --mostrar senha

Durante o cracking, você pode pressionar qualquer tecla para status, ou 'q' ou Ctrl-C para
abortar a sessão salvando seu estado em um arquivo ($JOHN/john.rec por
predefinição). Se você pressionar Ctrl-C pela segunda vez antes de John ter um
chance de concluir o manuseio de seu primeiro Ctrl-C, John abortará
imediatamente sem salvar. Por padrão, o estado também é salvo a cada
10 minutos para permitir a recuperação em caso de acidente.

Para continuar uma sessão interrompida, execute:

john --restaurar

Estas são apenas as coisas mais essenciais que você pode fazer com John. Por
uma lista completa de opções de linha de comando e para uso mais complicado
exemplos você deve consultar OPÇÕES e EXEMPLOS, respectivamente.

Observe que distribuições "binárias" (pré-compiladas) de John podem
incluir executáveis ​​alternativos em vez de apenas "john". você pode precisar
escolha o executável que melhor se adapta ao seu sistema, por ex. "john-omp" para
tirar proveito de várias CPUs e/ou núcleos de CPU.


Características.

John the Ripper foi projetado para ser rico em recursos e rápido. Isto
combina vários modos de craqueamento em um programa e é totalmente
configurável para suas necessidades específicas (você pode até definir um
modo de cracking usando o compilador embutido que suporta um subconjunto de C).
Além disso, John está disponível para várias plataformas diferentes, o que permite
você usar o mesmo cracker em todos os lugares (você pode até continuar um
sessão de cracking iniciada em outra plataforma).

Fora da caixa, John suporta (e detecta automaticamente) o seguinte Unix
Tipos de hash crypt(3): tradicional baseado em DES, "bigcrypt", BSDI estendido
baseado em DES, baseado em FreeBSD MD5 (também usado no Linux e no Cisco IOS) e
Baseado no OpenBSD Blowfish (agora também usado em algumas distribuições Linux e
suportado por versões recentes do Solaris). Também suportado fora da caixa
são hashes Kerberos/AFS e Windows LM (baseados em DES), bem como hashes baseados em DES
tripcodes.

Ao executar em distribuições Linux com glibc 2.7+, John 1.7.6+
adicionalmente suporta (e detecta automaticamente) hashes de criptografia SHA (que são
realmente usado por versões recentes do Fedora e Ubuntu), com opcional
Paralelização OpenMP (requer GCC 4.2+, precisa ser explicitamente
ativado em tempo de compilação, descomentando a linha OMPFLAGS adequada próxima
o início do Makefile).

Da mesma forma, ao executar em versões recentes do Solaris, John 1.7.6+
suporta e detecta automaticamente SHA-crypt e hashes SunMD5, também com
paralelização OpenMP opcional (requer GCC 4.2+ ou recente Sun Studio,
precisa ser habilitado explicitamente em tempo de compilação, descomentando o
linha OMPFLAGS adequada perto do início do Makefile e em tempo de execução
configurando a variável de ambiente OMP_NUM_THREADS para o valor desejado
número de processos).

Versões "-jumbo" adicionam suporte para centenas de hash e cifra adicionais
tipos, incluindo implementações integradas rápidas de SHA-crypt e SunMD5,
Hashes de senha do Windows NTLM (baseado em MD4), vários macOS e Mac OS X
hashes de senha de usuário, hashes rápidos como MD5 bruto, SHA-1, SHA-256 e
SHA-512 (que muitos "aplicativos da web" historicamente usam indevidamente para
senhas), vários outros hashes de senha de "aplicativo da web", vários SQL
e hashes de senha do servidor LDAP e muitos outros tipos de hash, também
tantos não hashes, como chaves privadas SSH, arquivos S/Key skeykeys,
Kerberos TGTs, sistemas de arquivos criptografados, como arquivos macOS .dmg e
"pacotes esparsos", arquivos criptografados como ZIP (PKZIP clássico e
WinZip/AES), RAR e 7z, arquivos de documentos criptografados como PDF e
Microsoft Office - e estes são apenas alguns exemplos. Para carregar alguns
esses arquivos maiores para cracking, um programa *2john incluído correspondente
deve ser usado primeiro e, em seguida, sua saída é alimentada no JtR -jumbo.


Interface gráfica do usuário (GUI).

Existe uma GUI oficial para John the Ripper: Johnny.

Apesar do fato de Johnny ser orientado para o núcleo JtR, todas as funções básicas
a funcionalidade deve funcionar em todas as versões, incluindo jumbo.

Johnny é um programa separado, portanto você precisa ter John the Ripper
instalado para usá-lo.

Mais informações sobre Johnny e seus lançamentos estão no wiki:

https://openwall.info/wiki/john/johnny


Documentação.
O restante da documentação está localizado em arquivos separados, listados aqui em
a ordem de leitura recomendada:

* INSTALAR - instruções de instalação
* OPÇÕES - opções de linha de comando e utilitários adicionais
* MODOS - modos de cracking: o que são
* CONFIG (*) - como personalizar
* REGRAS (*) - sintaxe das regras da lista de palavras
* EXTERNO (*) - definindo um modo externo
* EXEMPLOS - exemplos de uso - fortemente recomendado
* FAQ - palpite
* MUDANÇAS (*) - histórico de mudanças
* CONTATO (*) - como entrar em contato com o autor ou obter suporte
* CRÉDITOS (*) - créditos
* LICENÇA - direitos autorais e termos de licenciamento
* CÓPIA - GNU GPL versão 2, conforme referenciado pela LICENÇA acima

(*) a maioria dos usuários pode ignorá-los com segurança.

Existem muitos arquivos de documentação adicionais no "doc" do jumbo
diretório, que você também deseja explorar.

Leitura feliz!

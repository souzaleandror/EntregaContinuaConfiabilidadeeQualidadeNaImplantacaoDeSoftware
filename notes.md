#### 22/07/2023

Curso de Entrega Contínua: confiabilidade e qualidade na implantação de software

@01-O que é Entrega Contínua?

@@01
Introdução

Boas vindas ao curso sobre entrega contínua, sou Nico Steppat e serei seu instrutor.
Veremos como a entrega contínua se encaixa com a prática de integração contínua e aprenderemos sobre padrões de publicação e releases.

Entenderemos com detalhes quais são as etapas de um deployment pipeline e qual sua responsabilidade em cada etapa.

Vamos começar?

@@02
Bibliografia e links externos

A Entrega Contínua e todos os conceitos e práticas relacionados são bastante discutidos na literatura e web em geral, devido a sua importância.
Seguem algumas fontes que usamos para criar este curso:

Livro Continuous Delivery, do Jez Humble
Livro DevOps Handbook, do Gene Kim
Livro DevOps, da Casa do Código, do Danilo Sato
Artigo da ThoughtWorks: Continuous integration
Série de artigos do Martin Fowler sobre Entrega Contínua: Software Delivery Guide
Série de artigos da Caelum:
Branches e integração contínua: o problema de feature branches
Integração Contínua - Builds rápidos com Grids e paralelismo
Integração contínua: deploys e aprovações sem dor de cabeça para o cliente
Artigos sobre Entrega Contínua e padrões relacionados, do Jez Humble

https://www.amazon.com.br/Continuous-Delivery-Deployment-Automation-Addison-Wesley-ebook/dp/B003YMNVC0

https://www.amazon.com.br/DevOps-Handbook-World-Class-Reliability-Organizations-ebook/dp/B01M9ASFQ3/

https://www.casadocodigo.com.br/products/livro-devops

https://www.thoughtworks.com/pt/continuous-integration

https://martinfowler.com/delivery.html

https://blog.caelum.com.br/branches-e-integracao-continua-o-problema-de-feature-branches/

https://blog.caelum.com.br/integracao-continua-builds-rapidos-com-grids-e-paralelismo/

https://blog.caelum.com.br/integracao-continua-deploys-e-aprovacoes-sem-dores-de-cabeca-para-o-cliente/

https://continuousdelivery.com/

@@03
Diminuindo risco

Por que um curso de entrega contínua é importante? Para responder essa pergunta observaremos o mesmo gráfico do curso anterior de integração contínua.
A imagem ilustra que se fazemos poucas integrações em nosso projeto, o risco de surgirem problemas nas integrações aumenta.

grafico

O mesmo ocorre no caso do deploy, principalmente se for algo complexo. Não devemos fazer o deploy ser um evento raro e demorado, mas sim um processo natural e frequente no projeto.

Devemos lembrar que a prioridade número um de uma equipe é deixar o cliente satisfeito, com um projeto funcional e com entrega contínua carregada de valor.

Devemos, portanto, realizar deploys frequentes e preferencialmente automatizados e com feedbacks rápidos, como manda o processo ágil. Mas como podemos chegar a estas boas práticas?

Ao longo do curso aprenderemos alguns padrões para atingirmos o estado de entrega contínua, mas o principal é o pipeline de deploy: nosso software passará por várias estapas automatizadas que irão gerar mais qualidade no produto final.

Parece simples, mas esse pipeline apresenta dificuldades reais de implementação dentro de ambientes empresariais. Geralmente temos uma equipe múltipla envolvida na construção de um projeto e que atuam de maneira muito diferente, e isso pode gerar ruídos.

Por isso o DevOps é importante, criar um ambiente de trabalho colaborativo e ágil. Trata-se de uma modificação cultural muito mais do que implementação de ferramentas.

Temos uma provocação: quantos livros e artigos sobre design de software lemos ao longo de nossas carreiras? Quantos cursos realizamos? É importante acessarmos esses conteúdos para descobrirmos novas práticas e modelos de trabalho.

Este curso é para discutirmos essas boas práticas e colocarmos o código do nosso projeto em execução de maneira segura e ágil. Existem três livros interessantes que podemos citar como referência:

Continuous Delivery, Jez Humble e David Farley
DevOps HandBook, múltiplos autores
DevOps, Casa do Código

https://caelum-online-public.s3.amazonaws.com/1649+-+entrega+agil/01/1_2_1_grafico.png

@@04
Como deve ser a publicação do software?

A entrega contínua visa diminuir o risco na hora do deploy do software.
Para tal, a publicação do software deve ser:

Na nuvem
 
Alternativa correta
Conteinerizada
 
Alternativa correta
Granular
 
Alternativa correta! O tamanho importa. Deploys menores têm menos risco e são mais fáceis de entender quando dá algum problema.
Alternativa correta
Frequente
 
Alternativa correta! Implantações podem ser muito complexas e difíceis, e justamente por isso devemos repetí-las, para deixar o processo seguro e confiável.
Isso também é conhecido como Frequência reduz a dificuldade.
Alternativa correta
Automatizada
 
Alternativa correta! É essencial automatizar o máximo possível, desde a criação dos ambientes, instalação do software, configuração e execução dos testes.

https://martinfowler.com/bliki/FrequencyReducesDifficulty.html

@@05
Release Antipatterns

Comentamos sobre o coração da entrega contínua, o pipeline de deploy. Existem muitos formatos possíveis, mas ao observarmos essa representação gráfica, notaremos que existem uma série de etapas na construção de um projeto e cada uma delas possui complexidade específica.
etapa

O deploy é complexo, existem diversos componentes arquiteturais envolvidos que precisam ser escolhidos, configurados e alterados para que o software seja funcional.

É natural que um processo tão minucioso tenda a apresentar problemas, e o conceito de entrega contínua demandou muitas observações e meditações sobre esses infortúnios de projeto.

Discutiremos primeiramente quais são as más práticas ou "antipatterns" e então apresentar as alternativas.

1. Gerenciamento manual de ambientes

Cada ambiente precisa ser configurado e reconfigurado, e temos vários. Deveria ser fácil destruir o pipeline e reconstruí-lo com a mesma facilidade. Se etapas que já são complexas forem executadas manualmente teremos a presença de erros e inconsistências. Há casos em que o deploy funcionou em ambiente de homologação, mas não de produção, e é importante mencionar que são ambientes muito similares.

O mesmo pode ocorrer dentro do ambiente de produção, por exemplo o cluster, que possui várias máquinas envolvidas. Se as máquinas não forem idênticas a medida que o software se expande complexifica, teremos problemas. Isso ocorreu porque algo foi aplicado manualmente.

A regra de ouro é: Todos os ambientes são tratados como código, versionados e criados de maneira automatizada.

2. Deploy manual

Geralmente temos um manual que define as etapas de um deploy, mas geralmente a aplicação evolui e a documentação não é mais precisa e real. Há desenvolvedores que não sabem como o deploy é de fato realizado, afinal é um fazer delegado a poucas pessoas dentro da empresa em algumas configurações de equipe. Os deploys podem ser lentos e durarem horas ou dias. Nessa configuração teremos um deploy vagaroso, sujeito a erros e não confiável.

A regra de ouro é: apenas duas tarefas devem ser executadas manualmente: escolher a versão do release e o clique em "deploy buttom.

Dessa maneira qualquer pessoa da equipe pode realizar o deploy, o resto é automatizado, encapsulado e seguro.

3. Deploy apenas no fim do ciclo

Por exemplo, os desenvolveremos em aplicações estáveis e grandes focam em testes de criação de novas features e não interagem com a equipe de produção. Dessa maneira não sabemos se as novas features serão de fato funcionais e estáveis em produção.

Desse modo, teremos como resultado uma equipe pouco integrada, os problemas serão avistados apenas no dia da plubicação, e isso torna o processo mais lento.

A regra neste caso é: deployment faz parte do desenvolvimento desde a primeira interação, todos definem um delivery team.

Conhecemos três antipatterns clássicos que atrapalham a agilidade da construção de um projeto confiável. Devemos portanto ter:

Gerenciamento automatizado de ambientes
Deploy automatizado
Deploy frequente em cada ciclo de desenvolvimento

https://caelum-online-public.s3.amazonaws.com/1649+-+entrega+agil/01/1_3_1_etapa.png

@@06
Entrega Contínua vs Deploy Contínuo

Neste vídeo, discutiremos rapidamente as diferenças entre "entrega contínua' e "deploy contínuo". São conceitos similares, mas a diferença reside na última etapa do pipeline de construção do software entre a homologação e produção.
Na entrega contínua as modificações e atualizações não são enviadas prontamente para a produção, isto é, ficam "paradas" na homologação. Não existe uma razão técnica para segurar estas alterações, elas são de fato seguras e funcionais, mas os motivos envolvem estratégias de negócio.

Por exemplo, uma empresa deseja lançar um conjunto de features novas para o cliente em um evento especial de vendas.

deploy e entrega

No caso do deploy contínuo, as modificações vão de fato para o ambiente de produção. Veremos ao longo do curso que existem formas de ocultar funcionalidades que estão em produção.

https://caelum-online-public.s3.amazonaws.com/1649+-+entrega+agil/01/1_4_1_deploy+e+entrega.png

07
Entrega ou deploy?

Qual é a diferença entre entrega contínua e deploy contínuo?
Selecione uma alternativa

A entrega contínua é totalmente automatizada, sem nenhuma aprovação humana, e o deploy contínuo depende de uma aprovação humana
 
Alternativa correta
No deploy contínuo, todas alterações entram em produção, sem nenhuma aprovação humana. A entrega contínua depende de uma aprovação humana
 
Alternativa correta! O importante é que, na entrega contínua, as alterações não entrem em produção automaticamente, pois existe um motivo de negócio (marketing, por exemplo). Tecnicamente, não existe nenhuma razão para reter alterações.
Alternativa correta
Nenhuma, ambos são especializações da integração contínua
 
Parabéns, você acertou!

08
O que aprendemos?

Nesta aula, começamos a definir a Entrega Contínua (Continuous Delivery) e entender a diferença entre Entrega Contínua e Deploy Contínuo (Continuous Deploy).
A entrega contínua:

Visa diminuir todo o risco do deploy através de deploys frequentes e bem testados
Normalmente é implementada através de um pipeline de entrega do software
O pipeline representa o fluxo contínuo das alterações (valor) do código até o ambiente de produção
Visa automatizar todo o processo do deploy e aplicar cada alteração
O Deploy Contínuo coloca qualquer alteração em produção
A Entrega Contínua não coloca qualquer alteração em produção, mas só por motivos de negócio

#### 24/07/2023

@02-Fundamentos

@@01
Antes da Entrega Contínua

Definimos a entrega contínua e definimos seu elemento mais importante: o pipeline ue garante a entrega de valor para o cliente.
Descobriremos qual é a base para começar a implementar esta metodologia em nosso ambiente de trabalho. Quais são os princípios e fundamentos da entrega contínua?

Primeiramente precisamos começar com a integração contínua, que já estudamos no curso anterior, e as regras de outro desse processo são:

Build automatizado
Testes contínuos
Gerenciamento de configuração
Devemos realizar builds automatizados a fim de minimizar erros no processo, além de realizar testes contínuos de escalas diferentes que sejam claros e significativos e criar ambientes fáceis de reproduzir em qualquer máquina.

Antes de pensarmos em entrega contínua já teremos várias etapas anteriores que devem ser respeitados. Devemos lembrar que integração contínua não é o uso de uma ferramenta de gestão específica ou geração de relatórios, mas uma metodologia ágil que envolve alguns pressupostos, como master "deployavel".

Feito isso a equipe pode tentar estender o servidor de integração em uso e criar uma pipeline, mas neste caso existem alguns princípios arquiteturais que devemos aplicar.

@@02
Princípios

Definimos rapidamente a integração contínua, etapa essencial para se chegar até a entrega contínua. Mas quais são os princípios que norteiam esta prática?
Podemos definir a entrega contínua como o ato de>

Entregar software com alta qualidade e grande valor, de maneira eficiente, rápida e confiável"
A métrica principal é o software executável que satisfaz o cliente. O deploy não deve ser algo complexo ou extraordinário, sim algo simples,fácil e de baixo risco.

Vejamos os princípios básicos da entrega contínua:

I. Automatize

*II. Versione *

III. Repita

V. Defina "done"

VI. Crie delivery team

VII. Use melhoria contínua

Automatizar também faz parte da integração contínua, como ja frisamos diversas vezes. Versionar é importante não só para o código, mas tudo que é relacionado aos ambientes e testes. É importante repetir o deploy, não devemos deixar para realizá-lo no fim de semana depois de três alterações.

Devemos garantir a qualidade, se há algum temor de colocar o código em produção é porque os testes não forneceram a segurança necessária.

É importante definir o "done" corretamente. Não basta ter algo comitado e testado, "done" significa "em produção". Devemos, ainda, criar uma equipe de entrega com desenvolvedores, analistas, operation e assim por diante. Uma equipe multifuncional garantirá o sucesso do projeto.

Devemos utilizar a melhoria contínua, isto é, que cada etapa do pipeline tenha feedbacks rápidos sobre o estaus do software.

Estes são os princípios da entrega contínua.

@@03
Pré-requisitos

Das técnicas abaixo, quais representam a base da entrega contínua?

Deploy contínuo
 
Alternativa correta
Testes contínuos
 
Alternativa correta! É essencial ter testes de vários níveis e totalmente automatizados, que executam a cada commit.
Alternativa correta
Refatoração contínua
 
Alternativa correta
Integração contínua
 
Alternativa correta! Lembra-se da regra de ouro: sempre deve ter um master/trunk estável e os desenvolvedores devem comitar uma vez por dia no master/trunk.

@@04
Elementos principais

Na aula passada aprendemos os princípios da entrega contínua e sua definição. Neste ponto, discutiremos os elementos que compõe essa metodologia, e temos três itens principais:
1. Cultura DevOps Ela envolve: feedback, colaboração, confiança, melhoria e aprendizagem contínua.

2. Patterns São os padrões de deploy, ou releases de baixo risco. Nós ainda discutiremos esse assunto ao longo do curso, alguns padrões são blue/green, canary, feature toggle e outros.

3. Arquitetura A arquitetura é uma fase importante, pois quando falamos sobre arquitetura estamos mencionando a estrutura do sistema. As decisões estruturais são as mais difíceis dentro de um projeto, é necessário que ela seja estipulada no começo do trabalho. Quando pensamos na arquitetura queremos definir testabilidade, estabilidade, desempenho e outras propriedades como deployability.

Quanto melhor for a arquitetura do sistema, mais fácil será praticarmos entrega contínua. Se existem dificuldades em recriar o ambiente de produção isso influencia a testabilidade, afinal devemos criar um clone da produção para que o teste seja possível.

O mesmo se dá com o deployability. Se a base de código é muito grande, sentiremos dificuldade em inserir elementos na fase de produção. Nesta fase entram as boas práticas e os serviços e uma melhor base de dados.

@@5
Responsável pela entrega

Na entrega contínua, quem é responsável pela entrega do software?

A equipe de operações que cuida do monitoramento do sistema
 
Alternativa errada! A responsabilidade está com equipe inteira. Isso inclui pessoas de operações, mas também outros envolvidos. Todos representam um único time, o delivery time.
Alternativa correta
Todos os envolvidos na criação e entrega de software
 
Alternativa correta! Todos os envolvidos, do analista e desenvolvedor até o DBA e operações, todos devem fazer parte da equipe de entrega, o delivery time.
Alternativa correta
A responsabilidade está com o líder técnico da equipe
 
Alternativa correta
O desenvolvedor que fez a alteração no código

@@06
O que aprendemos?

Nesta aula, aprendemos sobre os fundamentos e princípios da Entrega Contínua:
Vimos que a base da Entrega Contínua é a Integração Contínua
Vimos os princípios, que são:
Automatize
Versione
Repita
Garanta a qualidade
Defina o "done"
Crie o delivery team
Use melhoria contínua
Além disso, falamos os elementos mais importantes para implementar a entrega contínua, como a cultura DevOps, Pattern de deployment e mudanças arquiteturais.

@03-Deployment Pipeline

@@01
Etapas do pipeline

Nesta aula entraremos de fato no deployment pipeline. No curso anterior sobre integração contínua utilizamos a metáfora do "botão de integração" que é acionado e o código sincronizado com qualidade e sem problemas.
Agora não queremos apenas integrar, mas mostrar a alteração para o cliente, por isso seria interessante um botão de "release". Mas para essa lógica funcionar devemos ter cuidado, devemos garantir por meio de etapas a qualidade do nosso produto.

Conheceremos as etapas clássicas do deploy.

1. Build

O começo de tudo é a build, isto é o desenvolvedor vai construir o software.

2. Testes de aceitação automatizados

Depois da construção do software são executados os testes necessários. Por meio dos testes criamos relatórios sobre a qualidade do sistema. Se alguma etapa falhar ela é congelada por aqui e o artefato não é promovido.

3 Homologação UAT A próxima etapa - caso tudo ocorra como o esperado - é a promoção do artefato. Este é o ambiente classico de User Acceptance Testing, ou simplesmente homologação. Nesta fase não executamos os testes mais complexos e que não podem ser automatizados.

4. Produção

Depois da aprovação manual, iremos para o ambiente de produção, em que o artefato será de fato produzido de maneira segura.

Cada etapa citada constrói mais confiança no produto. Os testes não garantem tudo, mas diminuímos muito a probabilidade de erros. O ambiente de homologação deve ser o mais parecido possível com o de produção para garantirmos a eficiência do deploy.

Nesse processo podem ter outras etapas. Abaixo teremos um exemplo um pouco mais sofisticado de pipeline, com unit tests, analysis AAT, homologação, testes de performance e produção.

pipe

O pipeline representa o processo de produção específico de uma equipe ou empresa, portanto não temos um padrão rígido.

Temos outro exemplo de pipeline que exibe o que acontece no momento em que é detectada uma falha no software. Além das etapas clássicas, temos a equipe (chamada delivery team) e o controle de versão. '

wiki

O processo de pipeline se inicia a cada comit que é testado separadamente. Nesta etapa os desenvolvedores utilizam ferramentas como Slack ou Telegram para se comunicarem sobre o estado do build, e se acontece algum problema toda a equipe é responsável.

https://caelum-online-public.s3.amazonaws.com/1649+-+entrega+agil/03/3_1_1_pipe.png

https://caelum-online-public.s3.amazonaws.com/1649+-+entrega+agil/03/3_1_2_wiki.png

@@02
Vantagens do pipeline

Quais são as vantagens de usar deployment pipeline?

Entrega otimizada através de ferramentas típicas do mundo DevOps
 
Alternativa correta
Entrega versionada
 
Alternativa correta
Entrega confiável
 
Alternativa correta! As etapas são testes do nosso sistema, começando com testes simples e rápidos, até chegar aos testes mais sofisticado.
Alternativa correta
Feedback rápido
 
Alternativa correta! Cada etapa dá feedback para a equipe sobre a qualidade do software.

@@03
Frequência de builds

Em que momento o pipeline começa a trabalhar?

momento o pipeline começa a trabalhar?
Alternativa correta
A cada commit
 
Alternativa correta! Para cada commit novo devemos construir e testar o software!
Alternativa correta
Só quando um desenvolvedor notifica o pipeline
 
Alternativa correta
Normalmente à noite, quando poucos desenvolvedores estão ativos
 
Alternativa correta
Normalmente a cada hora

@@04
Boas práticas

Lembremos as etapas clássicas do pipeline: build unit test, AAT, UAT e Produção. A pipeline é a única forma de realizar o deploy, assim chegamos em um estado seguro para o ambiente de produção. Outro ponto importante é o que o pipeline deve ser ágil, isto é, o seu desempenho dever ser satisfatório na resolução de problemas.
O build é a primeira etapa do projeto, e deve ser executado apenas uma vez, e sempre devemos utilizar o artefato inicial para evitar incompatibilidades.

O build em si deveria ser independente do ambiente, ou seja, o software não deve levar configurações hardcode. Já mencionamos também que os ambientes de homologação devem ser semelhantes ao ambiente de produção.

Os ambientes devem ser efêmeros, isto é, temporários. Não é uma ação sempre fácil de ser realizada em todos os projetos, mas é algo interessante, pois podemos criar cenários limpos para novos testes, afinal quando executamos um teste devemos criar um cenário para ele, e então analisar o comportamento do software.

Devemos garantir que o deploy para ambientes sempre seja igual, e esse escript que dará segurança ao pipeline. Idealmente devemos sempre utilizar a mesma maneira de deploy para cada fase do projeto.

Essas são algumas boas práticas da entrega contínua.

@@05
Referente aos ambientes

Os ambientes da pipeline devem ser:

Os ambientes da pipeline devem ser:
Alternativa correta
Reaproveitados
 
Alternativa correta
Containerizados
 
Alternativa correta
Temporários
 
Alternativa correta! Idealmente, criamos todo o ambiente do zero, para não levar nenhuma "sujeira" de instalações e testes anteriores.
Alternativa correta
Iguais ou semelhantes ao ambiente de produção
 
Alternativa correta! Quanto mais semelhante o ambiente, mais garantias temos que o deploy vai funcionar e os testes vão dar feedback real.

@@06
Ordem das etapas

Qual é a ordem aconselhada das etapas de um pipeline de implantação?

Unit Test --> Aceitação Automatizada --> Produção --> Homologação
 
Alternativa correta
Unit Test --> Aceitação Automatizada --> Homologação --> Produção
 
Alternativa correta! O importante é que os testes rápidos fique à esquerda, e que cada ambiente à direita se aproxime do ambiente de produção.
Alternativa correta
Unit Test --> Homologação --> Aceitação Automatizada --> Produção
 
Alternativa correta
Aceitação Automatizada --> Unit Test --> Homologação --> Produção

@@07
O que aprendemos?

Nesta aula, começamos a ver mais detalhes sobre o deployment pipeline. Vimos os stages (etapas) principais de um pipeline, que são:
Build/Commit stage
Automated Acceptance Testing Stage (Testes de aceitação)
User Acceptance Testing Stage (Homologação)
As etapas build e AAT são totalmente automatizadas. UAT é manual.

As etapas existem pois queremos receber feedback o mais rápido possível, ou seja, executamos os testes rápidos bem no início do pipeline.

Também falamos sobre algumas boas práticas na construção e execução do pipeline:

O pipeline é a única forma de deploy
O desempenho do pipeline importa, ou seja, otimize-o
Build do artefato no início e apenas uma vez
O build deve ser independente do ambiente
Ambientes deve ser iguais ou muito semelhantes ao de produção
Use ambientes efêmeros (temporários) onde puder
O deploy deve ser executado igual para qualquer ambiente

#### 26/07/2023

@04-Stage de commit e teste de aceitaçã

@@01
Commit Stage

Anteriormente, conhecemos as etapas do pipeline e falamos sobre boas práticas. Agora, focaremos em cada uma das etapas mais detalhadamente, começando pelo build, unit test e commit stage. Tudo que aprendemos sobre integração contínua aplica-se nesse ponto.
Nosso objetivo é garantir que não introduzimos um bug e tudo continua funcionando. É nesta etapa em que rodamos os testes de unidade (ou commit test), buildamos e disponibilizamos o artefato, e geramos relatórios de qualidade.

É ideal que esta etapa não demore mais do que 10 minutos. Quando uma pessoa altera o código-fonte e faz o commit, ela deve aguardar o resultado dessa etapa antes de seguir para outra tarefa. Não é obrigatório esperar as demais etapas do pipeline, mas é essencial aguardar o build. Por isso, é importante que ele seja executado em até 10 minutos. Portanto, o build é executado por commit na área de builds agendados.

Se esse processo estiver demorando mais que 10 minutos, é interessante otimizá-lo. Podemos executá-lo em paralelo, por exemplo. Como comentamos, vamos executar os testes de unidade, buildar e disponibilizar o artefato em um repositório na nuvem, e gerar os relatórios de qualidade. Os testes e a análise de código estático podem ser realizados paralelamente.

Idealmente, não devemos criar novas etapas. A pipeline deve ser curta e não ter muitas etapas. Logo, é melhor aumentá-la verticalmente, executando etapas intermediárias em paralelo.

Vale lembrar que tudo estará no repositório! É importante que todos da equipe de entrega tenham acesso aos artefatos — não somente o binário (o produto), mas também os relatórios.

Resumidamente, os passos clássicos dessa etapa são:

testes de unidade
build
análise estática
É importante que essa etapa seja rápida, pois a pessoa desenvolvedora deve aguardá-la para continuar seu trabalho. Como boas práticas, é interessante não testar a interface, evitar acessos ao banco de dados e async.

O objetivo é assegurar que nenhum bug foi introduzido e as demais funcionalidades continuam funcionando. Uma boa cobertura de testes é uma boa garantia de que o projeto continua funcionando, mas não é o suficiente.

Para agilizar, usa-se um repositório de artefatos como cache, caso o processo esteja ultrapassando os 10 minutos considerados ideais. O desempenho é importante!

Ademais, toda a equipe é responsável e deve ter acesso aos artefatos produzidos — tanto o binário quanto os relatórios. Quando um build quebra, toda a equipe precisa verificar o que está acontecendo. É preciso um código estável, não basta apenas regra de integração contínua.

Todos os scripts devem ser mantidos dentro do controle de versão, incluindo ambientes, configurações, migração, schemas, testes, entre outros. Eles devem evoluir junto do projeto para chegarmos à entrega contínua.

Também é preciso manter os ambientes dos devs atualizados. Tudo deve estar no sistema de controle de versão, porque precisamos ter consciência de que o ambiente usado para rodar os testes é diferente do ambiente do desenvolvedor.

Passamos rapidamente por esse assunto porque se trata de integração contínua e temos cursos específicos sobre organização do repositório, ferramentas de build, testes e assim em diante. Caso você queira se aprofundar nesse assunto, você pode buscar na plataforma da Alura.

No próximo vídeo, estudaremos os testes de aceitação automatizados.

@@2
Sobre o Commit Stage

O que é executado no Commit Stage?

Testes unitários
 
Alternativa correta! Logo após o build, devemos executar os testes de unidade, pois são os mais rápidos (feedback!).
Alternativa correta
Análise de qualidade de código
 
Alternativa correta! Os relatórios de qualidade são gerados nessa etapa. Podem ser executados em paralelo aos testes de unidade.
Alternativa correta
Teste de integração
 
Alternativa correta
Build
 
Alternativa correta! O primeiro passo é buildar a aplicação.

@@03
Resultado do Commit Stage

Assumindo que o build e os testes passaram, qual é o resultado do commit stage?

Plano de teste
 
Alternativa correta! Um plano de teste é relacionado com a equipe de Quality Assurance (QA) e não é um resultado do pipeline.
Alternativa correta
Relatórios de qualidade
 
Alternativa correta! O pipeline (servidor de construção) deve publicar os relatórios da análise de código junto com os testes de unidade.
Alternativa correta
Pipeline como script
 
Alternativa correta
Um artefato de build
 
Alternativa correta! Isso pode ser um JAR, DLL, imagem Docker, GEM ou ZIP, dependendo da sua plataforma.

@@04
Stage de testes de aceitação

Continuaremos nosso curso de entrega contínua, e lembraremos que nosso foco é o pipeline de deploy. Neste vídeo estudaremos a etapa de testes de aceitação automatizados. Nesta fase queremos testar a aplicação inteira e avaliar se ela preenche os requisitos de negócio. Esta é uma etapa essencial para chegar ao deploy contínuo e inserir a aplicação na fase de produção de maneira segura.
Diferente dos testes de unidade, esse tipo de teste garante que as funcionalidades em conjunto estejam plenamente operantes e atenderão o requisito do cliente. Tais testes são caros e trabalhosos, portanto é fácil de pular esta etapa devido ao seu custo e dificuldade.

Vamos utilizar um exemplo concreto: imagine que façamos uma refatoração na base do código e vários pontos são modificados. Neste momento, vários testes irão quebrar, por isso que a base de testes também deve ser atualizada, e neste momento como podemos garantir que um novo bug não foi criado?

Os testes de aceitação acessam a interface do software, como seria a experiência de usuário, e a ferramenta clássica para esta etapa é o Selenium. O teste de aceitação fornece uma garantia maior do ponto de vista do usuário.

Neste teste, a primeira fase é nosso artefato estar disponibilizado em um repositório, e caso tudo tenha ocorrido certo, o pipeline é notificado e sistemas como Jenkins fazem o papel necessário nesta fase.

O ambiente precisa ser todo configurado, e ele precisa ser similar ao ambiente de produção. Esta etapa é fundamental, porque se não ocorrem erros aqui a chance de algum imprevisto se dar na etapa de produção é muito reduzida.

Antes de executarmos todos os testes - já que são demorados - faremos o que é conhecido como smoke tests, testes menores que garantirão que as partes fundamentais da aplicação estão operantes.

O resultado dessa operação é um relatório que notificará a equipe do status da aplicação. Esta é uma etapa muito importante, afinal é a última fase dos testes automatizados, em seguida teremos uma maior presença humana.

Em resumo:

esquipe define as especificações (analistas,qa,dev)
responsabilidade a equipe
smoke tests para o ambiente
mock de sistemas externos
bons requisitos
boas práticas no design e implementação de testes
desempenho não é o mais importante
A responsabilidade da definição do teste é dividida entre toda equipe, assim como a correção de erros. Para garantir que o ambiente está adequado, devemos realizar um conjunto de pequenos testes dos recursos principais. Precisamos de bons requisitos para escrever as especificações e o teste na aplicação final real. Testes de aceitação são caros de escrever e manter, por isso desde o início devemos utilizar boas práticas no momento de criá-los. O desempenho importa, claro, mas não é o mais importante, geralmente são lentos.

@@05
Sobre testes de aceitação

O que é verdade sobre o stage de testes de aceitação automatizada?

Essa etapa é iniciado quando o commit stage foi executado com sucesso.
 
Alternativa correta! Quando executamos a primeira etapa com sucesso, automaticamente é chamado a etapa dos testes de aceitação automatizados.
Alternativa correta
O ambiente pode ser totalmente diferente do ambiente de produção.
 
Alternativa correta
Precisa de aprovação humana, normalmente alguém da equipe QA.
 
Alternativa correta
Nessa etapa é testado o sistema todo.
 
Alternativa correta! São testes baseados em requisitos, de alto nível (black box tests) e por isso muito valiosos.

@@06
O que aprendemos?

Nesta aula, definimos as etapas/stages de commit e de testes de aceitação automatizados (AAT):
Ambas as etapas executam os testes de maneira automatizada
O stage de commit foca nos testes de unidade e integração.
O stage AAT foca nos testes funcionais, que testam o sistema todo, baseado em um requisito
O commit stage deve executar rápido (menos de 10 minutos) e iniciar a cada commit
O stage AAT inicia quando commit stage foi executado com sucesso
O stage AAT é mais demorado
Os testes de aceitação são mais caros de escrever e manter, mas trazem muito valor, pois testam o sistema todo. Os testes de aceitação são escritos pela equipe inteira (analista, desenvolvedor, etc).

Quando um build quebra, todos são responsáveis. Consertar o problema é prioridade da equipe.

@05-Stage de Homologação

@@01
Stage de homologação

Seguiremos com nosso curso de entrega contínua, e nesta aula abordaremos a terceira fase do pipeline: homologação. A questão principal é de como podemos garantir o pleno funcionamento da aplicação de acordo com a expectativa do cliente.
Nesta fase os testes são executados pelo cliente, isto é, um usuário real do produto utiliza a interface do software, por isso essa etapa também é conhecida como "teste de aceitação".

A etapa de homologação não é tão precisa, não existe sempre uma completa aceitação ou rejeição por parte do usuário, mas pontos que precisam ser melhorados ou mantidos dentro do sistema.

Como existem várias pessoas envolvidas no projeto, cada uma terá uma visão diferente de negócio, e então com os feedbacks pequenas - ou grandes - mudanças serão requeridas.

Devemos lembrar que:

"Our highest priority is to satisfy the customer through early and continuous delivery of valuable software".
Isto é, a máxima prioridade é satisfazer o cliente ao oferecermos um produto com valor e aplicação. Em resumo, esta etapa contém:

*- Testes manuais pelo cliente * O cliente consegue usar o sistema de acordo com o esperado? Realiza as ações requisitadas? Apresenta dificuldade

- Validar o software

- Usabilidade contínua

- Equipe participativa

Trata-se de um universo amplo: construção do modelo de estes, recriação do ambiente de produção e assim por diante, mas estes são os pontos principais testa etapa do pipeline.

@@02
Sobre a homologação

Qual é o objetivo do ambiente de homologação?

Executar testes de integração
 
Alternativa correta
Testar o deploy no ambiente igual ao de produção
 
Alternativa correta! Como o ambiente de homologação é igual (ou muito parecido) com o de produção, temos mais garantias que o deploy vai funcionar.
Alternativa correta
Dar feedback para a equipe sobre a aceitação e usabilidade do software
 
Alternativa correta! A equipe deve participar e aprender com o usuário.
Alternativa correta
Validar se o software atende as expectativas
 
Alternativa correta! Idealmente, o usuário final testa e valida o software.

@@03
Stage de teste de carga

A todo tempo falamos das quatro etapas do pipeline de deploy e que uma boa prática é não permitir que ela cresça demais horizontalmente, isto é, devemos focar nestas 4 etapas.
Em paralelo a homologação, podemos executar o "Capacity Testing Stage". A pergunta que queremos responder é: como garantir que o software realmente suporta a quantidade de requisições, transações e acessos de usuários?

Criar esses cenários é algo complexo, existem ferramentas disponíveis e este é um conteúdo para um curso específico. O cenário de produção é algo dinâmico, pois precisamos pensar e reproduzir o comportamento dos usuários.

Os testes de carga buscam descobrir qual é a real capacidade do nosso sistema, ou seja, seu baseline. Conhecendo nosso sistema, devemos estabelecer metas claras e utilizar ferramentas de monitoração para descobrir as modificações arquiteturais que são necessárias.

Estes testes são mais caros devido a sua complexidade. Na fase de homologação não precisamos rodar a cada commit ou build, mas que o projeto seja monitorado desde o início. Podemos começar pelos testes de aceitação e criar um cenário, para elaborar os testes de carga ou fazer um replay dos dados de reprodução: gravamos o comportamento das requisições e realizamos um replay desses dados. Algumas ferramentas que podemos utilizar para isto são JMeter, Getling, Webbload, Apache Bench, LoadNinja.

Mesmo depois de passarmos para a produção, ainda existem riscos possíveis, e este problema trabalharemos nas próximas aulas.

@@04
Como testar?

Qual boa prática identificamos quando abordamos os testes de carga?

Deve ter uma meta clara
 
Alternativa correta! É preciso saber qual métrica que estamos avaliando e aonde queremos chegar.
Alternativa correta
Deve rodar em ambiente mais leve do que o de produção
 
Alternativa correta
Deve ser executado pelos desenvolvedores
 
Alternativa errada! Não é preciso, pois podem ser executados por equipe de testes.

@@05
O que aprendemos?

Nesta aula, falamos sobre os stages que possuem uma aprovação humana:
Homologação (User Acceptance Testing Stage)
Teste de carga (Capacity Testing Stage)
O ambiente de homologação serve para o usuário final validar se o software atende aos requisitos e expectativas. A equipe deve participar nesses testes e eles representam uma oportunidade de aprender e receber feedback sobre a aceitação e usabilidade do software. Esses testes devem ser executados desde início do projeto.

O ambiente para testes de carga serve para garantir que o software atende os requisitos não funcionais, como desempenho e carga. Os testes devem fazer parte do desenvolvimento do software e ser aplicados em ciclos. Aqui, é importante definir métricas claras e monitorar o sistema.

#### 27/07/2023

@06-Estratégias de releases

@@01
Releases de baixo risco

Nesta aula conversaremos sobre a última fase do pipeline: a produção. Mesmo nesta fase, ainda pensaremos em como inserir nossa aplicação com o menor risco possível, mesmo tendo passado por diversas etapas que irão ampliar a segurança e estabilidade do sistema ao longo do processo.
Era comum no meio dos desenvolvedores utilizar alguns "carimbos" de qualidade do software, como o Pré-Alpha, Alpha, Beta, Release Candidate e Release. Hoje em dia utilizamos o pipeline, com etapas sofisticadas com releases durante o desenvolvimento do projeto.

Já aprendemos ao longo do curso que a tarefa de redução de riscos deve começar ao início do projeto, lembremos de:

deploy e pipeline desde a primeira interação em ambientes similares.
automação, one-click deploy e smoke test ambiente
aspectos arquiteturais: testability e deployability
Além desses pontos,temos o "The twelve-factor app", são 12 boas práticas documentadas que nos fornecerem uma referência de como a aplicação deve se comportar dentro de um ambiente de nuvem. Ainda tempos outras medidas para deixar o sistema ainda mais confiável na última fase do pipeline.

Já mencionamos que os deploys devem ser realizados de maneira contínua, este é o tema do nosso curso. Devemos realizar *releases incrementais *, mesmo que a funcionalidade seja grande devemos realizar a implementação e realizar o deploy, assim chegamos mais perto do estado final do sistema.

Sabemos eventualmente não podemos inserir o módulo de maneira parcial, por isso existe a técnica "Brench by Abstraction" que já discutimos no curso anterior. Criamos uma abstração dentro do código com dois caminho, em fase de desenvolvimento ele pode ser testado, embora na fase de produção ele não exista ainda.

A entrega contínua faz a diferença entre o deploy e o release, e até agora utlizamos essas duas palavras como se fossem a mesma coisa, e na verdade não o são.

Deploy é criar um ambiente, garantir que ele exista de maneira correta, instalar o software e configurá-lo. Já o release é a publicação de fato, o momento em que o cliente utiliza o produto.

Devemos desacoplar o deploy do release, e para isso existem estratégias como:

Blue/Green Deployment
Canary Releases
Feature Toggles (Feature Flags)
Estudaremos mais detalhadamente cada uma dessas possibilidades adiante.

@@02
Atributos arquiteturais
PRÓXIMA ATIVIDADE

Quais atributos arquiteturais do software influenciam a entrega contínua?

Usabilidade
 
Alternativa correta
Testabilidade
 
Alternativa correta! Todo pipeline é relacionado com testes e o feedback deles. Um software que é difícil de testar, ou não possui testes, já não atende a integração contínua, menos ainda a entrega contínua.
Alternativa correta
Deployabilidade
 
Alternativa correta! Esse atributo define a facilidade de implantar o software. Microsserviços, por exemplo, possuem vantagens aqui.
Alternativa correta
Escalabilidade

@@03
Blue-Green Deployment

Anteriormente, mencionamos alguns princípios para deploys de baixo risco. Para garantir a segurança do nosso deploy, devemos aplicar algumas estratégias de release.
Temos duas questões principais:

Como evitar que a aplicação fique offline durante o deploy (zero downtime)?
Como voltar para a versão anterior (rollback) em caso de erro?
Começaremos por conhecer o Blue/Green Deployment. Tecnicamente, o deploy já foi realizado, mas temos duas versões: uma antiga(azul) e a nova(verde) que já está em ambiente de produção.

Entre as versões há um roteador, então em algum momento podemos modificar o fluxo para o novo ambiente, a nova versão. O ambiente velho (blue) fica no ar ainda um bom tempo caso algum problema surja. As conexões que existiam para o azul ficarão disponíveis até que realmente apenas a versão verde esteja totalmente funcional.

@@04
Deploy vs Release
PRÓXIMA ATIVIDADE

Por que separar o deploy do release?

Para fazer A/B testing
 
Alternativa correta
Para diminuir o risco da entrega
 
Alternativa correta! São duas etapas diferentes que podem dar erradas.
Alternativa correta
Para separar a decisão técnica (deploy) da decisão de negócio (release)
 
Alternativa correta! Podemos testar o deploy sempre, mas quando o negócio definir a publicação.

@@05
Feature Toggles e Canary Release

Aprendemos anteriormente sobre o Blue/Green Deployment, que oscila entre duas versões da aplicação: uma mais nova e outra mais antiga. Já o Canary Release executa ações parecidas, na verdade, podemos pensar que se trata de uma evolução.
Neste caso, as duas versões são utilizadas ao mesmo tempo, tanto azul quanto a verde, mas a nova versão não é acessada por todos os usuários. Uma parcela dos usuários que têm acesso a nova versão serão agentes de um teste.

O critério de direcionamento da nova versão em teste para alguns usuários varia, podemos usar 5% do nosso tráfego para a nova versão e monitorar o comportamento do sistema. Outro critério possível é o geográfico ou em estratégias de mercado, idade e assim por diante, isso vai variar de acordo com as necessidades do negócio e dados disponíveis sobre os usuários.

Uma vez que o teste for concluído, os usuários integralmente são direcionados para a nova versão. Esse metodologia também é utilizada para A/B Test.

O Canary Release é muito utilizado, e também é conhecido como "dark lauching" em tradução livre "lançamento no escuro", afinal nem todos os usuários sabem que existe um novo feature.

Outra estratégia com o mesmo objetivo é o Feature Toggles, também um dark lauching, mas neste caso trata-se de uma configuração no código que disponibiliza um switch de versões.

Um exemplo é quando é oferecida a consdição de "beta tester" para o usuário de alguma aplicação, caso a resposta seja positiva, alguma configuração no cadastro possibilitará o acesso à nova feature. Mas temos a mesma base de código, não são duas versões blue ou green.

Esta estratégia pode ser combinada ao Canary Release: uma parcela dos usuários que será direcionado para a versão nova utilizará o Feature Toggles habilitado. Há pessoas que defendem que toda a nova funcionalidade deve ser um Feature Toggles, mas para isso ser implementado de maneira correta deve-se elaborar uma estratégia para lidar com essa proposta.

@@06
Blue-Green vs Canary
PRÓXIMA ATIVIDADE

Qual é a diferença entre Blue-Green Deploy e Canary Release?

O Blue-Green sempre usa Feature Toggles, e o Canary não.
 
Alternativa correta
No Blue-Green, apenas uma parte dos usuários usa o ambiente novo. No Canary todos os usuários usam o ambiente novo.
 
Alternativa correta
No Canary, apenas uma parte dos usuários usa o novo ambiente. No Blue-Green todos os usuários usam o ambiente novo.
 
Alternativa correta! No Canary Release, apenas uma parte dos usuários são direcionados para o novo ambiente. No Blue-Green todos os usuários vão ser direcionados para o ambiente novo.

@@07
Para saber mais: The Twelve-Factor App
PRÓXIMA ATIVIDADE

The Twelve-Factor App é um site (ou metodologia) que define 12 boas práticas para construir software na era de nuvem. Muitas das boas práticas discutidas no curso aparecem no Twelve-Factor, assim como gerenciamento de configuração, portabilidade entre ambientes ou implantação contínua. Vale conferir!
The Twelve-Factor App

https://12factor.net/pt_br/

@@08
O que aprendemos?
PRÓXIMA ATIVIDADE

Nesta aula, falamos sobre estratégias ou patterns de implantação. Foi importante mencionar que o deploy e o release são duas operações distintas. Ou seja, podemos fazer deploy da aplicação, mas mesmo assim ainda não publicar as novas features.
Ter features invísiveis para o cliente também é chamado de dark launching, quando já implantamos o novo software, mas o cliente ainda não tem acesso (ou só alguns clientes).

Resumindo:

Vimos a diferença entre deploy (implantação) e release (publicação)
Deploy é colocar as alterações em produção (provisionar, configurar, instalar)
Release é deixar as alterações visíveis
Os padrões para o release do software são:

Blue-Green Deployment
Canary Release
Feature Toggles

@@09
Conclusão

Parabéns pela finalização do curso! Aprendemos juntos ao longo das aulas o que é a entrega contínua e os problemas que essa prática busca resolver: um deploy e release com menos risco, isto é, garantir um sistema saudável, estável e com valor para o cliente de maneira ágil.
Aprendemos sobre os testes de automação, quais os elementos principais da entrega contínua e a cultura DevOps. Este último ponto se refere à forma como a equipe é organizada e seu modo de trabalho.

Aprendemos que a arquitetura também influencia a qualidade do deploy, tornando-o mais fácil ou mais difícil de ser realizado. Estudamos alguns padrões de pipeline de deployment e suas etapas principais, bem como seus objetivos e características.

Na última etapa do pipeline - a produção - conhecemos algumas estratégias de deploy e release, conceitos diferentes que precisam ser separados.

Muito obrigado, e continue estudando!
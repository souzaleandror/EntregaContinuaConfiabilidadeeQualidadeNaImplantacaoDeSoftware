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
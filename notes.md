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

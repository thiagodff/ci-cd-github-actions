# Projeto

Esse projeto é um template de React com a estrutura, eslint e prettier configurados.

## Pipeline que iremos configurar para esse projeto

yarn -> yarn lint -> yarn test -> yarn build

1. Uma ferramenta de CI/CD
2. Um servidor para rodar a pipeline
3. Um servidor de deploy

# CI e CD

## CI - Continuos Integration - Integração Contínua

Integra o nosso código, nosso produto, o git é uma excelente ferramenta de integração entre os desenvolvedores, mas hoje em dia apenas o git não é o suficiente.

Como saber se o código que outro desenvolvedor fez está seguindo os padrões da empresa, se está funcionando corretamente, se não irá adicionar um bug na aplicação, se está seguindo a style guide.

Uma prática/processo para integrar os códigos da nossa aplicação.

Processo de exemplo: validação de lint -> validação de testes -> verificação de commit

## CD - Continuos Delivery - Entrega Contínua

Vem logo após o CI (se existir). Uma prática/processo para criar o entregável o resultado. Realiza todos os passos para gerar a build final que será entregue ao usuário, porém não irá enviar para o usuário.

Processo de exemplo: buildar ou compilar o projeto -> enviar o código para o servidor (criando uma nova instância do kubernets se necessário).

## CD - Continuos Deployment - Deploy Contínuo

A prática/processo de entregar o resultado do código para o usuário final.

Para trabalhar com Continuos Deployment é necessário que o software tenha um preparo para aceitar a nova aplicação, pois algumas features nós podemos querer só estejam acessíveis após um certo horário, por exemplo.

Muitas empresas mantém o deploy contínuo desabilitado para ter um melhor controle do "virar a chave" para a aplicação ir pro ar. Por exemplo, decidir colocar no ar as novas features somente no horário em que menos pessoas estão utilizando sua aplicação.

## Feature Flag

Existem situações que a empresa não quer se uma feature seja lançada até determinada data ou que determinada ação ocorra.

O controle dessa funcionalidade estar disponível é a partir de uma flag, pode ser uma tabela de flags no banco de dados. Pode ser utilizado o flag base.

Geralmente essa funcionalidade é reaproveitada para controlar o que o usuário vai ter acesso ou não.

## Feature Branching

O mesmo problema da questão anterior mas resolvido utilizado branch's, que só irão para master no momento ideal, porém tem alguns problemas como o código dessa branch ficar desatualizado com o da master.

# Pipeline

É o fluxo, uma esteira para definir a execução de cada etapa do CI e CD.

É basicamente um arquivo com um script que define o passo a passo que deverá rodar.

## Stages

Steps:

- Setup
  - yarn
  - post-install
- CI
  - Lint (vem primeiro pois é mais rápido do que os testes)
  - Testes

Fluxo para toda branch com PR criada:

Branches -> CI -> CD -> CDeployment -> Url Preview -> Master

Master -> CI -> CD -> CDeployment

![Processo de CI CD](./assets/ci_cd.jpg 'CI CD process')

A parte do monitor entra os KPI que são os indicadores do software, se estão sendo bem atendidos.

# Ferramentas

Hoje em dia existe muitas ferramentas e muitas que estão nascendo estão vindo de forma nichadas, apenas para projetos node, react, etc.

A ferramenta mais utilizada para integração contínua e entrega contínua é o Jenkins:

- Self hosted (você instala e hospeda onde quiser)

Algumas concorrentes que também são muito utilizadas no mercado:

- Circle CI
- Travis CI
- Cloud Build
- Github Actions (muito boa pois já integra direto com seu repositório)
- AWS Codedeploy

Ferramentas com setup facilitado, principalmente para times que não tem DevOps:

- Vercel (somente funciona com react, node, next, porém a configuração é bem facilitada, toda nova pr aberta ele gera uma URL para preview e ajuda muito os QA)

Ferramentas para React Native

- App Center (React native, ios, android, flutter)
- Bitrise
- Fastlane (algumas funcionalidades interessantes como tirar screenshots da tela para colocar na pagina da google play)

## Jenkins

Uma das ferramentas mais utilizadas que integra com praticamente qualquer linguagem. É uma ferramenta bem completa e precisa de várias configurações para funcionar, se sua aplicação precisa de algo como o Jenkins muito provavelmente existirá um time de CRE infra/DevOps no time para cuidar disso. É uma ferramenta pra quando precisamos escalar nossos projetos, geralmente custa bem mais caro do que um plano do github actions.

Ele é self hosted, ou seja, você deve instalar em sua máquina e rodar localmente, dentro dele você pode configurar um novo projeto.

O Jenkins oferece inúmeros plugins para auxiliar no desenvolvimento, por padrão só é possível criar um projeto freestyle.

Podemos adicionar parâmetros para por exemplo escolher buildar para homologação, dev, sandbox ou production. Também é possível fazer isso através da URL se for chamar ele através de um web hook utilizando o build triggers.

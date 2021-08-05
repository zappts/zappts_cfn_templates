# Parâmetros do template do Code Pipeline

Alguns templates de pipeline podem vir com parâmetros de configuração. Vamos entender esses parâmetros?

## DeploymentRegion

O Code Pipeline exige que quando o Source Step, o passo que faz dowload do código-fonte, é o Code Commit, este precisa estar na MESMA região em que o Code Pipeline se encontra. Ou seja, se seu código está em um Code Commit em OHIO, suas Pipelines OBRIGATORIAMENTE precisam estar em OHIO também. Então, como fazemos deploy para outras regiões? O parâmetro DeploymentRegion serve justamente para isso. Especificando esse parâmetro, os passos de build e deploy são realizados na região onde você quer que seja deployada a aplicação. Esse conceito é chamado de cross-region-actions.

Saiba mais: https://docs.aws.amazon.com/codepipeline/latest/userguide/actions-create-cross-region.html

## ParameterOverrides

Em um Code Pipeline onde um dos passos é fazer o deploy de um template de Cloud Formation, é possível passar quais são os parâmetros para esse template via a tag ParametersOverride. Dessa maneira eu não preciso gerenciar no repositório do código quais são os parâmetros para cada ambiente pois estes ficam gerenciados dentro da pipeline. 

Saiba mais: 

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stackinstances-override.html
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline-parameter-override-functions.html


## Conditions

O CloudFormation permite utilizar condições para que determinados parâmetros sejam criados ou definir quais propriedades devem ser associadas àquele parâmetro. O template de CodePipeline pode ser compilado tanto para javascript quanto typescript. Por isso o parâmetro HasTS é utilizado para indicar se o repositório é em typescript ou javascript. Isso é utilizado pela condition HasTSCondition para alterar os parâmetros do CodeBuild

Saiba mais:

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/conditions-section-structure.html

## RdsExecution

RdsExecution é um passo da pipeline criado por nós para rodar queries SLQ no banco quando a pipeline executa. Dado uma pasta chamada db_updates no root do seu projeto, o passo RdsExecution executará todos os arquivos SLQ desta pasta se houver algum. Seus scripts SQL podem conter uma tabela de controle para que não seja executado mais de uma vez
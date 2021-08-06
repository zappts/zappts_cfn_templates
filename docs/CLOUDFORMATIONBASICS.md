# CloudFormation Basics

Olá! Leia esta seção para saber mais como criar templates em CloudFormation

## Propriedades

Cada item do CloudFormation pode ser considerado. Vamos entender como funciona cada uma delas

### AWSTemplateFormatVersion

O TemplatFormatVersion indica a versão do template que se está fazendo deploy. Geralmente costuma usar como exemplo abaixo:

AWSTemplateFormatVersion: '2010-09-09'

### Description

Description contém a descrição para identificar qual o contexto do template

### Parameters

Os parâmetros definem variáveis que queremos utilizar no nosso template. Ao fazer o deploy do template, precisamos informar qual o valor daquele parâmetro. Também é possível especificar um valor Default caso nenhum valor seja passado. Todo parâmetro é necessário especificar o seu tipo.

## Resources

Essa propriedade conterá todos os recursos AWS que serão criado no template

Saiba Mais:

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html

## Transform

O recurso transform possibilita executar macros em cima do template. Assim você pode customizar a sintaxe do template adequado a sua necessidade ou simplificar alguns templates. O Serverless Framework utiliza macros e transform para aplicar simplificações na criação de recursos serverless.

Saiba mais:

https://docs.aws.amazon.com/pt_br/AWSCloudFormation/latest/UserGuide/transform-section-structure.html
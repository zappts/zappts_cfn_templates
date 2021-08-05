# Conditions

Conditions, como o próprio nome sugere, permite colocar condições no template para que determinada ação seja executada caso a condição seja validada.

## Como criar conditions

Conditions são uma propriedade do template. Você pode abrir uma seção de Conditions e criar suas condições para serem utilizadas no template. Vamos a um exemplo:

```
Conditions:
  IsProdCondition: !Equals [!Ref Stage, "prod"]
  IsDevCondition: !Equals [!Ref Stage, "dev"]
  HasVPCCondition: !Equals [!Ref HasVPC, "true"]

```

Nestes dois exemplos, criamos uma condição para verificar se um parâmetro é igual a prod ou se igual a dev. Dessa forma, podemos utilizar essa condition para criar recursos somente quando o ambiente for de produção. Também criamos um parâmetro para dizer se os recursos são pertencentes a uma VPC ou não.

Um caso de uso interessante é quando queremos criar uma infraestrutura mais simplificada em dev, então deixamos de criar alguns recursos ou especificar VPCs quando estamos em dev e só criamos os mesmos quando estamos em produção.

Podemos utilizar diversos operadores em Conditions para fazer a avaliação de parâmetros. São aceitos as operações: AND, EQUALS, OR e NOT. Também é possível aninhar condição para criar uma condição mais complexa. Veja o exemplo a seguir:

```
  IsDevOrProdCondition: !Or 
    - !Condition IsProdCondition
    - !Condition IsDevCondition
```

Nesse caso, se uma das duas condições IsProdCondition ou IsDevCondition forem verdadeiras, então a condição IsDevOrProdCondition será verdadeira também.

## Utilizando Conditions nos recursos

Há duas maneiras mais recorrentes de utilizar Conditions nos recursos. A primeira forma é para determinar toda a criação de um recurso baseado se a condição é verdadeira ou não. Se a condição é válida, o recurso é criado. Caso contrário, o recurso não será criado.

Outra maneira é utilizar o operador IF para alterar os valores de propriedades dentro dos recursos. Sendo assim, quando uma condição é verdadeira podemos utilizar um determinado valor e quando a condição for falsa, utilizamos outro.

 Veja o exemplo abaixo:

```
# Aurora Writer Instance
  AuroraWriterInstance:
    Type: AWS::RDS::DBInstance
    Condition: IsDevOrProdCondition
    Properties: 
      DBClusterIdentifier: !Ref AuroraDBCluster
      DBInstanceClass: db.t3.small
      DBInstanceIdentifier: !Sub dw-${Stage}-table
      DBSecurityGroups: 
        - !If
          - HasVPCCondition
          - !Ref SecurityGroupIds
          - !Ref AWS::NoValue
      DBSubnetGroupName:  !If [HasVPCCondition, !Ref SubnetGroupDBName, !Ref AWS::NoValue]
      EnablePerformanceInsights: !If [IsProdCondition, true, false]
      Engine: aurora-mysql
      PubliclyAccessible: !If [HasVPCCondition, false, true]
```

Nesse exemplo estamos criando uma instância de Banco de Dados para o Aurora. Com a tag Condition no nível do recurso definimos a criação ou não do recurso como um todo. Nesse caso, o banco só será criado para os ambientes desenvolvimento e produção para que qualquer outro ambiente possa reaproveitar o mesmo banco de desenvolvimento.

Dentro das propriedades do recurso utilizamos as funções IF para avaliar as conditions e definir o valor de cada propriedade. Por exemplo, só trataremos de propriedades de rede (security groups e subnets) se nosso banco estiver dentro de uma VPC. Só habilitaremos performance insights se o banco criado for o de produção.


Saiba mais: 
https://docs.aws.amazon.com/pt_br/AWSCloudFormation/latest/UserGuide/conditions-section-structure.html



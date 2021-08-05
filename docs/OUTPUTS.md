# Outputs

Outputs são utilizados para exportar variáveis do CloudFormation e deixar o valor disponível globalmente. A vantagem de utilizar Outputs é que você pode importar o valor da variável em outro template e economizar em lógica de parâmetros

## Como utilizar Outputs

Utilize a tag Outputs para indicar qual valor estará exportando e criar um alias para aquela variável

```
Outputs:
  Example Sqs export:
    Description: "Example Sqs Export "
    Value: !GetAtt ExampleSqs.Arn
    Export:
      Name: !Sub ${Stage}-example-sqs
```

Neste exemplo, o arn de uma fila sqs é exportado com o nome ${Stage}-example-sqs. Ao importar esse nome em outro template, podemos acessar o arn daquele recurso e referenciá-lo em outros recursos, como é feito abaixo:


```
  LambdaFromSqsExample:
    Type: AWS::Serverless::Function
    Properties:
      FunctionName: !Sub "${Stage}-example"
      Role: !GetAtt LambdaRole.Arn
      CodeUri: ./../
      Handler: app/src/handler/example.example
      Runtime: nodejs12.x
      Timeout: 900
      Events:
        SqsEvent:
          Type: SQS
          Properties:
            Queue:
                  Fn::ImportValue:
                    Fn::Sub: ${Stage}-example-sqs
```

No exemplo acima, uma lambda é criada com um evento SQS. Precisamos do arn da fila que está em outro template. Utilizamos a função ImportValue para importar o valor do SQS.
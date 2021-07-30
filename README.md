# Bem vindo ao Zappts Cloud Formation Templates!

Olá! Somos a Zappts :grinning: 

Esse repositório é dedicado a disponibilizar templates de Cloud Formation para nossa comunidade :nerd_face:

## O que é Cloud Formation?

Cloud Formation é um serviço da AWS em que você descreve recursos para provisionar na nuvem. Esses recursos ficam atrelados ao template podendo ser facilmento copiados, alterados e versionados. 

Saiba mais sobre Cloud Formation: https://aws.amazon.com/pt/cloudformation/

## Como esse repositório está estruturado?

Cada template está dentro de uma pasta representando o serviço e seu contexto. Por exemplo

- templates
   - codepipeline
     * codepipeline-for-lambdas
       - arquivo.yaml
       - arquivo-parametros.json (opcional)
       - arquivo.sh (opcional)

Arquivos de parâmetros e scripts para executar via CLI o deploy do template são opcionais
## Como contribuir?

Para contribuir e disponibilizar seu template é simples! 

1. Faça fork do projeto
2. Adicione os seus templates seguindo a estrutura de pastas do projeto
3. Seu template é complexo? Use a pasta docs para falar sobre ele
4. Abra um PR (Pull Request) para a branch develop

Semanalmente é feito de PRs em main e uma nova versão taggeada da main é disponibilizada :)

É Zappter e quer contribuir sem precisar fazer fork? Fale com a gente!

## Sobre a Zappts

Prazer, somos a Zappts! E aceleramos a transformação digital da sua empresa! :rocket:

Saiba mais: https://zappts.com/

Quer fazer parte do time? Acesse: https://zappts.gupy.io/

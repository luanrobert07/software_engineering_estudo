# 🌍 Padronizando código em seu time

https://refactoring.guru/design-patterns

------------------------

- [📜 Introdução ao Design Patterns](#-introdução-ao-design-patterns)
  - [📚 O que é Design Patterns](#-o-que-é-design-patters)
    - [Ferramentas](#ferramentas)
      - [⚛️ EditorConfig](#-eitor-config)
      - [🌲 Vagrant/Docker](#-vagrant-docker)
    - [🔄 Fluxo de desenvolvimento](#-fluxo-de-desenvolvimento)
      - [🚀 Code Review](#-code-review)
      - [🌐 Pair programming](#-pair-proggraming)
      
  - [🧠 Objetivo de aprendizagem](#-objetivo-de-aprendizagem)
  - [✔️ Entrega mínima](#️-entrega-mínima)

## 📚 Introdução ao Design Patterns
Manter a organização e o padrão no código é um dos maiores desafios de um time na programação
Pense em seu projeto como um corpo humano, cada “gambiarra” ou fuga do padrão é como se seu projeto ingerisse algo muito ruim que com o tempo irá torná-lo inoperável ou até matá-lo.

### O que é Design Patterns
Os Design Patterns são formas comuns de escrever código a fim de solucionar problemas que provavelmente você irá encontrar com o crescimento do seu código.
Esses padrões vão muito além de formas de separar o código em arquivos com nomes legais, os Design Patterns são embasados em milhares de problemas que pessoas como você já tiveram e dentre elas encontraram um padrão que funciona bem.

Design patterns (Padrões de projeto), que no final, se resumem a soluções típicas para problemas comuns em um projeto de software.
Os padrões de projeto (design patterns) são como plantas pré-projetadas de uma construção, que você pode alterar para se adequar melhor na resolução de um problema recorrente em seu código. O que diferencia os padrões de projeto das funções e bibliotecas é que você não pode simplesmente copiá-los direto para seu programa, já que eles não são um pedaço de código, mas sim um conceito que serve como uma solução.

Design patterns are typical solutions to commonly occurring problems in software design. They are like pre-made blueprints that you can customize to solve a recurring design problem in your code.

### Ferramentas

#### ⚛️ EditorConfig
o EditorConfig gerencia as configurações do seu editor baseado em cada projeto. Está utilizando indentação com 2 espaços? Linha em branco no final do arquivo? Deixa que essa ferramenta realiza a configuração para todos os outros integrantes do time automaticamente.

Para iniciar, você deve criar um arquivo chamado .editorconfig na raiz do seu projeto e dentro dele vamos começar a especificar as regras:
```
root = true
[*]
indent_size = 2
insert_final_newline = true
end_of_line = lf
charset = utf-8
```
root: Define se esse é o arquivo principal do EditorConfig (você pode ter mais arquivos em pastas);
[*]: Define quais arquivos vão sofrer essa configuração, no caso estou repassando todos (você pode definir por exemplo: */.js ou até lib/*.php;
As outras configurações representam o tamanho de indentação, linha em branco no fim do arquivo, tipo de quebra de linha e charset respectivamente. Você pode encontrar uma lista de configurações possíveis aqui.

Agora instale a extensão no seu editor de preferência e pronto, todos que tiverem também a extensão e abrirem seu projeto estarão com o editor configurado exatamente da mesma forma que você.

#### 🌲 Vagrant/Docker
Vagrant: Fácil de configurar, ótimo para quem está iniciando (vídeo para quem quer começar: https://www.youtube.com/watch?v=gx50Kv6-2KA)
Docker: Utilize principalmente se tiver seu processo de build automatizado, vai ajudar bastante.

### 🔄 Fluxo de desenvolvimento

#### 🚀 Code Review
Code review significa basicamente revisar o código, mas quem? Eu mesmo? Na verdade não. A ideia é que toda vez que um desenvolvedor terminar uma feature e for integrá-la ao projeto, o seu código passe por uma revisão por pelo menos outro desenvolvedor do time.

Apesar de parecer complicado gerenciar esse fluxo de desenvolvimento, uma ferramenta de controle de versão como o Git, unida ao poder do Github e suas Pull Requests, pode tornar tudo isso muito menor custoso.
#### 🌐 Pair programming

Técnica utilizada em metodologias ágeis como a XP que consiste em dois programadores escreverem código ao mesmo tempo, no mesmo computador, um ao lado do outro. Com dois teclados? Não, um de cada vez. Enquanto um programa o outro analisa se faria da mesma forma e voltamos ao antigo ditado onde duas cabeças pensam melhor que uma.

### Tipos de padrões:

### Padrões criacionais
Estes padrões oferecem diversas alternativas de criação de objetos, o que aumenta a flexibilidade e a reutilização de código. Alguns dos principais padrões desse tipo são:

- Factory Method
- Abstract Factory
- Builder

### Padrões estruturais
Nos mostram como montar objetos e classes em estruturas maiores, sem perder a eficiência e flexibilidade. Alguns dos principais padrões desse tipo são:

- Adapter
- Bridge
- Composite

### Padrões comportamentais
Nos ajudam a trabalhar melhor com os algoritmos e com a delegação de responsabilidades entre os objetos. Os padrões que se destacam nesse tipo são:

- Chain of Responsibility
- Command
- Interpreter


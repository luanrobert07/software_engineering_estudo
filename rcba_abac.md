# 🌍 RBAC e ABAC: Modelos de Controle de Acesso no Desenvolvimento de Software

------------------------

- [📜 Introdução ao RBAC e ABAC](#-introdução-ao-rbac-abac)
  - [📚 O Que é RBAC?](#-o-que-é-rbac)
    - [Benefícios do RBAC](#beneficios-rbac)
    - [⚛️ Desafios do RBAC](#-desafios-rbac)
  - [📚 O Que é ABAC?](#-o-que-é-abac)
    - [Benefícios do ABAC](#beneficios-abac)
    - [⚛️ Desafios do ABAC](#-desafios-abac)
    
  - [🧠 Objetivo de aprendizagem](#-objetivo-de-aprendizagem)
  - [✔️ Entrega mínima](#️-entrega-mínima)

## 📚 O Que é RBAC?
Role Base Access Control
O RBAC é um modelo de controle de acesso no qual as permissões são atribuídas a funções, e não diretamente a indivíduos. Uma "função" representa um conjunto de permissões necessárias para realizar um conjunto específico de tarefas. Os usuários são então atribuídos a essas funções, herdando suas permissões.

Examples: An organization might have roles like 'Admin', 'Manager', and 'Employee', with different permissions for each role.

### Benefícios do RBAC
- Simplificação Administrativa: A centralização das permissões em funções reduz a complexidade e o esforço necessários para gerenciar direitos de acesso.
- Segurança Aprimorada: Implementando o princípio do menor privilégio, minimiza-se o risco de acesso excessivo.
- Consistência e Conformidade: Facilita a aderência a políticas de segurança e requisitos de conformidade.

## 📚 O Que é ABAC?
Controle de Acesso Baseado em Atributos
Atribui permissões com base em políticas que avaliam atributos dos usuários, do ambiente e dos recursos a serem acessados. Este modelo permite políticas de acesso dinâmicas, adaptando-se facilmente a diferentes contextos e necessidades.

O ABAC funciona, em síntese, como um executor de lógicas de permissão que recebe a solicitação de acesso, correlaciona o conjunto de atributos relacionados à identidade, ao recurso e ao evento em curso e submete seu pacote de correlações ao repositório de políticas de acesso. Tudo isto segundo o princípio booleano “if-then”.

### Benefícios do ABAC
- Granularidade e Flexibilidade: Capacidade de definir políticas de acesso altamente específicas baseadas em uma ampla gama de atributos.
- Adaptabilidade: Facilmente ajustável a mudanças nos requisitos de acesso.
- Controle Baseado em Contexto: Permite levar em conta o contexto da solicitação de acesso, como localização ou hora do dia.

### Como funciona?

O ABAC concede permissões baseadas em quem o usuário é e não no que ele faz, o que permite controles granulares. Os atributos são analisados para avaliar como eles interagem em um ambiente e, posteriormente, são aplicadas regras com base nos relacionamentos.  

Veja como o processo normalmente funciona:

- É feita uma solicitação de acesso. 
- A ferramenta de controle de acesso baseado em atributo verifica os atributos para determinar se eles correspondem às políticas existentes.  
- Com base no resultado da análise da ferramenta ABAC, a permissão é concedida ou negada. 

### Qual é a diferença entre RBAC vs. ABAC?
Enquanto o RBAC baseia a permissão na função do usuário, o controle de acesso baseado em atributos (ABAC) baseia-se em atributos relacionados ao usuário (por exemplo, cargo, nível de antiguidade, deveres de trabalho), recurso (por exemplo, tipo de arquivo/aplicativo, sensibilidade ou fonte), ou contexto (por exemplo, onde, como e/ou quando o recurso está sendo acessado).

O ABAC aumenta exponencialmente as opções de permissão com a adição de atributos específicos, adicionando outro nível de controle em comparação com o RBAC. Embora infinitamente mais flexível do que o RBAC, esta flexibilidade também acrescenta complexidade que pode aumentar o risco se não for implementada e gerenciada adequadamente.

### Examples of Use Cases:

RBAC: Suitable for environments with well-defined roles and stable access requirements, such as corporate IT systems, ERP systems, and HR systems.
ABAC: Ideal for environments requiring dynamic and context-sensitive access control, such as cloud computing, healthcare systems, and environments with regulatory compliance needs.

| **Feature**         | **RBAC**                           | **ABAC**                          |
|---------------------|------------------------------------|-----------------------------------|
| **Basis of Access** | Roles                              | Attributes (user, resource, environment) |
| **Granularity**     | Coarse                             | Fine                              |
| **Flexibility**     | Less flexible                      | Highly flexible                   |
| **Management**      | Easier to manage                   | More complex to manage            |
| **Use Cases**       | Stable roles and permissions       | Dynamic, context-sensitive access control |

### Implementação no Desenvolvimento de Software
- Planejamento Detalhado das Políticas de Acesso: Definir claramente quem precisa de acesso a quais recursos e sob quais condições.
- Seleção de Ferramentas Adequadas: Utilizar frameworks e bibliotecas que suportem a implementação desejada do modelo de controle de acesso.
- Monitoramento e Auditoria: Implementar mecanismos para revisar e auditar o acesso, assegurando que as políticas sejam seguidas e identificando potenciais abusos.

A escolha entre RBAC e ABAC, ou uma combinação dos dois, dependerá das necessidades específicas de cada projeto. Enquanto o RBAC pode ser suficiente para necessidades de acesso mais estáticas e bem definidas, o ABAC oferece flexibilidade e granularidade para ambientes dinâmicos e complexos.

<div align="center">
  <iframe width="560" height="315" src="https://youtu.be/NG8qTapopj4?si=Amq_nN_8rz8d5yPg" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
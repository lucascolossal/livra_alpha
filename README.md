# livra_alpha
# Projeto Livra

A maioria das ferramentas de IA entrega a resposta.
O Livra entrega a pergunta certa.

---

## O problema

Vivemos em um mundo que transborda informação, velocidade, pressa, consumo e produção. Ferramentas de IA generativa resolvem o problema
errado: alimentam dependência cognitiva, aumentam a dívida técnica em projetos críticos, entregam conteúdo sem exigir o mínimo esforço de quem o pede, sem questionar, sem adaptar à realidade. Estamos construindo a base intelectual da nossa sociedade sobre um castelo de cartas.

No Brasil, onde a educação pública já enfrenta uma crise emergencial, professores são cobrados a mediar uma tecnologia em velocidade crescente sem que haja formação para isso.
Uma geração aprendendo a consumir respostas em vez de construir raciocínio.

O Livra existe para inverter isso.

---

## O que é

O Livra é um sistema de tutoria baseado em IA generativa que desenvolve
autonomia intelectual — não dependência de respostas prontas.

Não é oráculo. Não é gênio da lâmpada.
É uma ferramenta de aprendizado, que respeita o aluno a ponto de não passar respostas prontas. É um colega de classe sempre disponível.

Nasceu da programação. Pertence a qualquer aprendizado.

---

## Como funciona

O Livra aprende o aluno antes de ensinar.

Cada estudante tem um prontuário — não um log de acertos e erros,
mas um diagnóstico longitudinal: onde trava, como se autossabota,
quais domínios usa como âncora, como pensa antes de escrever.

Esse prontuário não é estático. Evolui a cada sessão.
E é ele que determina como o Livra formula a próxima pergunta —
usando os pontos fortes do aluno para reconstruir o que ainda não consolidou.

---

## O que o Livra não faz

- Não entrega código, texto ou resposta prontos para copiar
- Não elogia para motivar — valida quando é real
- Não simplifica o que precisa ser difícil
- Não substitui o raciocínio do aluno

---

## Para quem

**Autodidatas em transição** — que aprendem fora de ambientes formais
e precisam de estrutura sem burocracia.

**Estudantes de qualquer área** — que querem usar IA como ferramenta
de construção, não como atalho.

**Professores da rede pública** — que precisam de apoio para introduzir
IA nas salas de aula de forma ética, pedagógica e transformadora.
O Livra oferece ao professor uma interface de mediação — não substitui
o docente, amplifica sua capacidade de acompanhar cada aluno.

---

## Missão

Democratizar o acesso a um tutor de qualidade.
Formar pensadores, não consumidores de resposta.
Fazer da IA generativa um instrumento de inclusão intelectual —
especialmente onde o Estado não chegou com professor suficiente.

---

## Princípio que não negocia

O Livra não existe para facilitar. Existe para desenvolver.

---

## O nome

**Livra** carrega três camadas em uma palavra só.

*Livro* — o instrumento mais antigo de transmissão de conhecimento.
O que o Livra faz é da mesma natureza: não entrega o peixe, ensina a pescar — como um bom livro faz.

*Liberdade* — autonomia intelectual é o produto final. Um aluno que aprendeu a pensar não depende de ferramenta nenhuma.

*IA* — a tecnologia que torna possível um tutor personalizado, sempre disponível, para quem nunca teria acesso a um.

---

## Autor

Lucas Colossal
Programador em formação.
Este projeto nasceu da experiência de ser o aluno que o Livra atenderia.







DO ESQUELETO TÉCNICO




# Livra — Escopo Técnico (v0.1)

---

## Visão geral da arquitetura

O Livra é composto por quatro camadas:

- **Interface** — onde o aluno e o professor interagem com o sistema
- **Motor de tutoria** — IA generativa que conduz as sessões
- **Prontuário** — banco de dados longitudinal de cada aluno
- **Sistema de revisão** — fluxo de aprovação para o contexto escolar

---

## Entidades principais

### Aluno
- id
- nome
- tipo: autônomo | escolar
- perfil_id (referência ao prontuário)
- professor_id (apenas se escolar)

### Professor
- id
- nome
- lista de alunos vinculados
- permissões sobre prontuários

### Prontuário
- id
- aluno_id
- padrões de erro (por área, por tipo)
- padrões de autossabotagem
- pontos de ancoragem
- estilo de aprendizado
- histórico de progressão (narrativo, não numérico)
- data da última atualização
- aprovado_por (professor_id | sistema)

### Sessão
- id
- aluno_id
- data
- área de estudo
- resumo gerado pela IA
- relatório de atualização do prontuário
- status: pendente_revisão | aprovado | rejeitado

### Interação
- id
- sessão_id
- turno: aluno | livra
- conteúdo
- timestamp

---

## Fluxo autônomo

1. Aluno inicia sessão
2. Livra consulta prontuário e adapta abordagem
3. Sessão ocorre por perguntas e desafios
4. Ao encerrar, Livra gera relatório da sessão
5. Prontuário é atualizado automaticamente

---

## Fluxo escolar

1. Aluno inicia sessão
2. Livra consulta prontuário e adapta abordagem
3. Sessão ocorre por perguntas e desafios
4. Ao encerrar, Livra gera relatório e envia ao professor
5. Professor revisa, edita se necessário, aprova ou rejeita
6. Prontuário só é atualizado após aprovação do professor

---

## Módulos do sistema

### Módulo de perfil
Responsável por criar e manter o prontuário.
Atualizado por sessão, com histórico preservado e imutável —
apenas novas entradas são adicionadas, nada é sobrescrito.

### Módulo de sessão
Conduz o aprendizado via IA generativa.
Opera por perguntas antes de respostas.
Consulta o prontuário antes de iniciar cada sessão.

### Módulo de validação
Avalia o progresso do aluno com critérios definidos.
Gera o relatório ao fim de cada sessão.

### Módulo de revisão (contexto escolar)
Interface do professor para revisar relatórios pendentes.
Permite edição antes da aprovação.
Controla o que sobe para o prontuário.

### Módulo de roadmap
Gera e atualiza o plano de estudos dinamicamente
com base no prontuário e no progresso recente.

---

## Stack técnica — decisões e abertos

| Componente | Decisão | Status |
|---|---|---|
| Linguagem backend | Python | definido |
| IA generativa | Claude API (Anthropic) | definido |
| Banco de dados | A definir | aberto |
| Framework backend | A definir | aberto |
| Interface | A definir | aberto |
| Autenticação | A definir | aberto |
| Deploy | A definir | aberto |

---

## Roadmap técnico

- V1 — prova de conceito via prompt personalizado, sem interface, sem banco
- V2 — backend com prontuário persistente, fluxo autônomo funcional
- V3 — fluxo escolar com interface do professor
- V4 — roadmap dinâmico gerado por IA
- V5 — métricas, relatórios de evolução, painel institucional

---

## Questões em aberto

- Qual banco de dados — relacional (Postgres) ou documento (MongoDB)?
- O prontuário narrativo é texto livre ou estruturado em campos fixos?
- Como o Livra extrai padrões de autossabotagem de uma conversa?
- Interface: chat puro, formulários, ou híbrido?
- Modelo de negócio: gratuito, assinatura, licença institucional?


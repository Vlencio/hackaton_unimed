# Treino 1: Rastreador de Guias de Autorização

**Tempo:** 4 horas cronometradas, sem pausa para pesquisar o que não for essencial.
**Formato:** sozinho, simulando que o resto da equipe está fazendo o pitch.

## Contexto

Beneficiários da Unimed Uberlândia reclamam de três coisas na autorização de exames e procedimentos:

1. Não sabem em que pé está o pedido. O prazo informado é de "até 5 dias úteis" e ninguém retorna.
2. O app mostra "autorizado", mas o laboratório vê "pendente".
3. No intercâmbio (paciente de uma Unimed atendido por outra), cada Unimed diz que o problema está na outra.

Sua missão é construir um **hub de status de guias**: uma fonte única de verdade, que todas as partes consultam, e que avisa cada mudança.

## Atores

| Ator | O que precisa fazer |
|---|---|
| **Atendente da Unimed** | Ver a fila de guias e mudar o status (com justificativa quando negar) |
| **Laboratório/prestador** | Consultar uma guia pelo número ou CPF e ver o status real na hora |
| **Beneficiário** | Ver as próprias guias e o histórico de cada uma, e receber aviso a cada mudança |

## Regras de negócio

- **Status possíveis:** `SOLICITADA → EM_ANALISE → AUTORIZADA` ou `NEGADA`. Uma guia `PENDENTE_DOCUMENTO` pode voltar para `EM_ANALISE`.
- **Transições inválidas são bloqueadas.** Exemplo: `NEGADA → AUTORIZADA` sem passar por nova análise.
- **Toda mudança gera um evento** com status anterior, status novo, quem mudou e quando. O histórico nunca é apagado nem editado.
- **Negativa exige justificativa** em texto.
- **Prazo:** guia sem decisão após 5 dias úteis da solicitação fica marcada como **atrasada**. O prazo é fictício para o treino.
- **Intercâmbio:** cada guia tem uma *Unimed de origem* (a do beneficiário) e uma *Unimed executora* (onde o exame será feito). As duas veem a mesma guia e o mesmo status.

## Dados sintéticos (gerar no início)

- **3 Unimeds:** Uberlândia, Ribeirão Preto e Sorocaba.
- **50 beneficiários** distribuídos entre elas, com CPF falso e número de carteirinha.
- **100 guias** em status variados, algumas de intercâmbio e algumas já atrasadas.
- Nenhum dado real. Diga isso no pitch: é o seu argumento de LGPD.

## Obrigatório (sem isso, não está pronto)

- [ ] Painel do atendente: lista de guias com filtro por status e destaque nas atrasadas
- [ ] Mudar status pelo painel, respeitando as transições válidas
- [ ] Tela do laboratório: busca por número da guia ou CPF, mostrando o status atual
- [ ] Tela do beneficiário: minhas guias + linha do tempo de cada uma
- [ ] Mudança no painel aparece nas outras telas **sem precisar recarregar manualmente** (ou com no máximo um refresh automático curto)
- [ ] Notificação a cada mudança de status. Pode ser simulada (um log ou uma "caixa de mensagens" na tela), não precisa ser WhatsApp de verdade
- [ ] No ar com um link acessível (deploy)

## Bônus (só se o obrigatório estiver fechado)

- Contador "guias atrasadas por Unimed" no painel
- Mensagem da notificação em linguagem simples, gerada por IA ("Seu exame de sangue foi autorizado. Pode agendar no laboratório X.")
- Tempo médio até a decisão, por Unimed


## Ao terminar, anote

- Onde travou e quanto tempo perdeu ali
- O que precisa estar pronto **antes** do hackathon (template, deploy, gerador de dados) para não perder esse tempo no dia

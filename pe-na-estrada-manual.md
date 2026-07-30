# Manual do Pé na Estrada

Guia rápido de cada função do app. Por Fênix Soluções Tecnológicas.

## Navegação geral

- O app abre no **Menu**, com 4 botões grandes: Nova Chamada, Abastecimento, Histórico e Config.
- O ícone **🏠** no canto do cabeçalho, em qualquer tela, volta pro Menu.
- Se você tiver uma corrida em andamento e fechar/reabrir o app, ele pula o Menu e já abre direto na corrida, pra você não perder o passo.
- O cabeçalho tem sempre 3 linhas: a data de hoje, o resumo do dia (corridas, km, tempo) e o status de conexão/sincronização.

## Status de conexão (bolinha no cabeçalho)

- 🔴 **Offline** — sem internet, salvando só neste aparelho.
- ⚪ **Online sem conta** — internet ok, mas sem login, dados só locais.
- ⚪ **Sincronizando...** — enviando os dados pra nuvem agora.
- 🟢 **Online sincronizado** — tudo enviado e salvo na nuvem.

## Nova Chamada (a corrida, passo a passo)

**Passo 1 — Iniciar**
- Informe o KM de saída (odômetro, 6 dígitos), o valor a receber, e opcionalmente os endereços de coleta e entrega.
- Use o botão 🔍 pra buscar o endereço certo — ele mostra a distância até você e prioriza suas cidades atendidas (configuradas na Config).

**Passo 2 — Cheguei para a Coleta**
- Quando chegar no ponto de coleta, toque no botão e informe o KM daquele momento.
- O botão 🗺️ abre a rota no Google Maps até a coleta.

**Passo 3 — Cheguei para a Entrega**
- Ao chegar no destino, informe o KM. O app pergunta se a entrega foi concluída.
- **Se sim**, a corrida vai direto pra tela de encerrar.
- **Se não** (recusada), o app manda voltar pro ponto de coleta.

**Passo 4 — Recusa e retorno**
- Ao voltar na coleta, informe o KM de chegada.
- Você escolhe entre **Tentar Nova Entrega** (repete o Passo 3 com um novo destino) ou **Encerrar Sem Entrega**.
- Se houve recusa, aparece um campo pra registrar o ressarcimento do app (99/Uber) pelo retorno, caso haja.

**Encerrar e resultado**
- Confirme o valor a receber e finalize. O app mostra: km real rodado, tempo total, valor, R$/km bruto e — se você já tiver abastecimento registrado — o R$/km líquido (descontando combustível estimado).
- Se tiver veículo com combustível cadastrado, também mostra quanto você já rodou hoje e quanto ainda pode/deve rodar.
- Depois você pode editar endereço e nome de quem fez a coleta e a entrega.

## Abastecimento

- Toque em **Registrar Abastecimento**: informe KM, litros e valor pago.
- O app calcula quanto de autonomia esse abastecimento deu (bruto) e quanto é recomendado rodar (descontando a reserva de segurança do veículo).
- **Resumo de hoje**: autonomia posta hoje, km rodado hoje, saldo, e autonomia restante na última leitura.
- Cada abastecimento da lista pode ser **editado** ou **excluído** — o histórico de autonomia do veículo é recalculado automaticamente do zero quando isso acontece, pra nunca ficar com número torto.

## Histórico

- Filtros de período: **Hoje**, **7 dias**, **Mês**, **Tudo** ou **Período** (escolha datas De/Até).
- Cada corrida na lista pode ser expandida (toque) pra ver detalhes, e editada.

## Config

**Minha casa** — endereço usado no botão "🏠 Voltar para Casa" (tela inicial), que abre a rota no Google Maps.

**Meus destinos favoritos** — endereços que você usa com frequência, com rota rápida e opção de remover.

**Veículos cadastrados** — cadastre placa, apelido, tipo (moto/carro), consumo (km/l), reserva de segurança, capacidade do tanque (ativa aviso de autonomia baixa) e tipo de odômetro (mecânico com hectômetro ou digital em km inteiro). Dá pra editar tudo depois, exceto a placa.

**Conta e sincronização** — login opcional por email/senha. Sem conta, o app funciona 100% local. Com conta, os dados sincronizam com a nuvem (Firestore) automaticamente quando online, e você pode forçar com "Sincronizar Agora".

**Backup dos dados** — exporte um arquivo .json com tudo (corridas, abastecimentos, veículos, destinos), e restaure a partir de um arquivo depois, se precisar.

**Zona de risco** — apaga TODOS os dados deste aparelho. Exige digitar "APAGAR" pra liberar o botão. Use só ao terminar os testes, pra começar do zero com dados reais.

## Dicas importantes

- **Odômetro de 6 dígitos**: se o seu veículo é mecânico (a maioria das motos populares), o último dígito é o hectômetro (0,1 km) — digite os 6 números exatamente como aparecem no painel, sem vírgula. Se for digital, o app já sabe que é km inteiro (configurado no veículo).
- **Google Maps**: os botões de rota abrem o Maps já com o destino — o próprio Maps usa sua localização atual como ponto de partida.
- **Backup**: exporte de vez em quando, principalmente antes de trocar de aparelho.

# Agendia — Design e especificação funcional

Versão de projeto 01 · 22 de outubro de 2026

**Seu horário, sem complicação.**

Documento para revisão antes do desenvolvimento. Nome provisório, sem validação de marca ou domínio. O protótipo contém somente exemplos locais: não cria contas, não reserva serviços reais, não envia mensagens nem processa dinheiro. Projetar uma função não significa que ela já foi implementada.

## 1. Direção do produto

Uma plataforma para clientes, autônomos e pequenos estabelecimentos. Primeira operação focada em serviços de beleza de uma região, com atendimento no estabelecimento e em domicílio. A mesma identidade visual atende cliente, profissional e empresa, mas cada papel tem permissões e tarefas próprias.

Promessa: agendar com clareza, evitar conflitos e perder menos horários. A lista extensa de funcionalidades será construída em etapas; não será entregue inteira no primeiro lançamento.

## 2. Identidade e sistema visual

- Marca: Agendia, em letras minúsculas na interface; símbolo inicial de calendário com confirmação. Marca gráfica provisória, a ser refinada antes do lançamento.
- Tom: simples, humano e profissional. Preferir “Escolha seu horário” a mensagens técnicas.
- Tema claro: fundo #F6F8F7, superfícies #FFFFFF, texto #18352E, texto secundário #5C7069, ação principal #17634C, divisórias #DCE6E0.
- Tema escuro: fundo #101B19, superfícies #182723, texto #E5F1EC, texto secundário #ACC3B9, ação principal #8BDDB7 com texto #13392B, divisórias #344B42.
- Tipografia: Inter ou fonte do sistema; texto de 14–16 px; campos móveis de pelo menos 16 px; títulos de 24–32 px.
- Espaçamento: escala 4, 8, 12, 16, 24 e 32 px. Controles arredondados em 8 px; cartões em 14 px.
- Ícones: família consistente de traços simples, sempre com rótulo acessível.
- Fotos: opcionais; iniciais como alternativa. Portfólio do trabalho separado da foto pessoal.
- Estados: disponível, selecionado, indisponível, carregando, vazio, erro recuperável, erro bloqueante e sucesso. Nunca depender apenas de cor.
- Acessibilidade: navegação por teclado, foco visível, rótulos para campos e ícones, áreas de toque de pelo menos 44 px, contraste verificado e suporte a texto ampliado e movimento reduzido.
- Responsividade: menu lateral no desktop; navegação compacta no celular. Reserva em uma coluna no celular e formulário + resumo no desktop.
- Mensagens propostas: “Esse horário acabou de ser reservado. Escolha outra opção.”; “Não conseguimos confirmar o pagamento ainda. Não pague novamente.”; “Alteração salva”; “Sua conexão caiu. Confira o status antes de repetir.”

## 3. Papéis e permissões

| Papel | Acesso previsto |
|---|---|
| Visitante | Catálogo, preços, disponibilidade e perfil público; autenticação mínima para confirmar. |
| Cliente | Próprias reservas, pagamentos, preferências, avaliações elegíveis e suporte. |
| Profissional autônomo | Próprios serviços, disponibilidade, clientes vinculados, reservas e recebimentos. |
| Profissional de equipe | Própria agenda e dados necessários aos atendimentos; demais acessos concedidos pelo proprietário. |
| Recepção | Agendar e remarcar pela empresa; acesso financeiro limitado por permissão. |
| Proprietário | Equipe, catálogo, políticas, assinatura, relatórios e permissões da empresa. |
| Suporte/administrador | Acesso mínimo, justificado e auditado; ferramentas de incidentes e denúncias, sem acesso irrestrito por padrão. |

Uma pessoa pode ser cliente e profissional. Trocar o modo de visualização não altera autorização. Cada empresa terá dados separados; o servidor valida acesso em toda operação.

## 4. Mapa das telas

| Área | Telas/estados |
|---|---|
| Entrada | Apresentação, entrar, criar conta, confirmar e-mail/telefone, recuperar acesso, escolher papel. |
| Primeiro uso | Tutorial curto e retomável; configurar perfil, serviços, horários e compartilhamento. |
| Descoberta | Categoria, profissional, preço, região, serviço presencial/domiciliar; resultados vazios e indisponibilidade. |
| Perfil público | Foto, descrição, serviços, especialidades, portfólio, redes sociais, região e avaliações. |
| Reserva | Serviço, adicionais, local, profissional, data/hora, identificação mínima, resumo, política, pagamento e confirmação. |
| Cliente | Próximos e anteriores; detalhes; remarcar; cancelar; avisar ausência; avaliar; suporte. |
| Agenda profissional | Dia/semana, busca de reserva, criação manual, bloqueios, status, detalhes e histórico de alterações. |
| Catálogo | Criar, editar, desativar serviço e adicional; preços, durações, categoria e compatibilidade. |
| Clientes/equipe | Histórico privado, profissionais, jornadas e permissões. |
| Configurações | Temas, notificações, horários, região, taxas, meios de pagamento, conta e privacidade. |
| Financeiro | Status do pagamento do serviço, estornos, taxas e repasses; assinatura do app em área separada. |
| Confiança | Avaliações, resposta, denúncia, bloqueio, protocolo e acompanhamento. |
| Suporte | Tutorial, dúvidas frequentes, abertura de chamado e acompanhamento. |
| Operação | Saúde dos serviços, alertas, fila de tentativas, backups e trilha de auditoria. |

O protótipo demonstra a navegação principal, catálogo com criação de serviço, seleção de adicionais, cálculo de total/duração, reserva em três etapas, cancelamento simulado, troca de papel e tema. Cadastro real, mapas, pagamentos, fotos, verificações e envio de notificações estão especificados, não implementados.

## 5. Fluxos principais

### Cliente

Abrir link do profissional → escolher serviço → selecionar adicionais compatíveis → escolher local → informar região/endereço quando necessário → ver horários compatíveis com duração → identificar-se → revisar valor, política e pagamento → confirmar → receber comprovante da reserva e instruções.

A confirmação de reserva e a confirmação de pagamento são estados distintos. Em reserva sujeita a sinal, explicar quando o horário fica garantido. Se a reserva expirar enquanto o pagamento está sendo processado, não confirmar sobre um horário ocupado: encaminhar restituição ou escolha de novo horário conforme regra aprovada.

### Profissional e recepção

Configurar catálogo e jornada → compartilhar link → acompanhar agenda → criar reserva recebida por telefone/mensagem → informar ao cliente política e eventual pagamento → registrar comparecimento → concluir atendimento → acompanhar pagamentos.

Reserva manual obedece à mesma regra de conflito. Cliente não recebe marketing por ter sido cadastrado pela recepção. Registro manual não significa que o profissional pode aceitar cobranças em nome do cliente sem autorização.

### Empresa

Cadastrar espaço e equipe → atribuir serviços e jornadas → configurar permissões → distribuir reservas → acompanhar operação e recebimentos. Atendimento não deve poder ser atribuído a alguém que não realiza o serviço.

## 6. Serviços, adicionais e preço

Cada serviço contém nome, descrição, categoria, duração, preço, local aceito, profissionais habilitados, intervalo de preparação, imagem opcional e situação ativo/inativo.

Cada adicional contém nome, descrição, preço, duração adicional, serviços compatíveis e situação. Primeiro lançamento: seleção opcional de cada adicional uma vez; quantidades e dependências ficam para evolução.

Fórmulas:

- Total = preço do serviço + adicionais escolhidos + deslocamento explicitamente informado.
- Tempo de atendimento = duração do serviço + duração dos adicionais.
- Tempo ocupado na agenda = atendimento + intervalos de preparação e deslocamento aplicáveis.

Exemplo ilustrativo: manicure R$ 35/45 min + decoração R$ 15/15 min + deslocamento R$ 15 = R$ 65 e 60 min de atendimento, mais tempo reservado para trajeto.

O cliente vê cada parcela antes de confirmar. Alteração futura do catálogo não muda o valor de reservas já aceitas. Alterações em uma reserva confirmada precisam de aceite quando mudarem preço ou condições. Desativar um serviço não apaga reservas nem histórico. Identificar claramente orçamento sob consulta; não inventar preço final.

## 7. Disponibilidade e conflito de horários

- Jornada semanal por profissional, fuso do local, pausas, folgas, bloqueios e exceções por data.
- Antecedência mínima e horizonte máximo de agendamento configuráveis.
- Validar intervalo inteiro; adicionais longos podem remover opções de horário.
- Reserva temporária sugerida de 5 minutos durante confirmação; duração final a validar.
- Bloqueio e confirmação atômicos no servidor para impedir concorrência entre clientes e recepção.
- Remarcação garante o novo horário antes de liberar o anterior, sem deixar duas reservas definitivas.
- Requisições repetidas usam uma identidade da operação para não duplicar reservas.
- Estado de conexão incerta exige consultar o resultado, sem repetir cegamente.
- Primeira versão domiciliar: regiões e tempos de deslocamento configurados manualmente. Cálculo automático por rota vem depois.
- Reservas recorrentes futuras verificam cada ocorrência; apresentar conflitos, sem substituir compromissos silenciosamente.

## 8. Estados e ciclo da reserva

Disponível → bloqueado temporariamente → aguardando confirmação/pagamento, se aplicável → confirmado → em atendimento → concluído.

Saídas alternativas: bloqueio expirado, cancelado pelo cliente, cancelado pelo profissional, não comparecimento. Remarcação preserva vínculo e histórico. Aguardando pagamento, pago, falhou, estorno pendente, estornado e contestado pertencem ao pagamento, não substituem o status do atendimento.

Cada transição registra autor, data/hora, motivo e valores afetados. Não comparecimento pode ser contestado. Avaliação não deve ser apagada ou impedida por mudança indevida de status sem possibilidade de revisão.

## 9. Cancelamento e taxas — decisão pendente

Regra explicitamente proposta pelo usuário e mantida apenas como referência provisória: gratuito até 10 horas após realizar a reserva; depois, 10% do total destinados ao profissional. Percentual configurável no futuro; não é comissão da plataforma.

A discussão posterior propôs usar antecedência até o atendimento, mas não definiu prazo substituto. Portanto, nenhuma regra definitiva de cobrança está aprovada para lançamento.

Definir antes de cobrar:

1. Cancelamento de reserva cujo atendimento começa antes das 10 horas.
2. Cancelamento com muitos dias de antecedência após o prazo provisório.
3. Remarcação, tolerância a erro, força maior e faltas.
4. Cancelamento pelo profissional e devolução de valores.
5. Base de cálculo da taxa, inclusive deslocamento não realizado.
6. Se os 10% são repasse bruto ou líquido das tarifas do processador.
7. Autorização de cobrança e meios de pagamento que permitem a operação.

A tela mostra prazo absoluto de cancelamento gratuito e valor exato da taxa antes da confirmação. A política aceita fica versionada na reserva. Nenhuma taxa muda retroativamente.

## 10. Pagamentos e assinaturas

Serviço: profissional define meios aceitos (Pix, dinheiro e cartão). Escolher o meio não comprova pagamento. Dinheiro requer registro de recebimento. Pix deve ser confirmado por integração, não por captura de tela. Cartão deve usar provedor, sem guardar número ou código de segurança no Agendia.

Cancelamento não pode descontar automaticamente dinheiro que nunca foi recebido. Sinal, autorização, repasse, estorno, contestação e tarifas dependem do provedor escolhido e das regras aprovadas. Antes de repetir uma operação, reconciliar seu resultado. Pagamentos e eventos recebidos devem ser idempotentes.

Assinatura da plataforma: plano mensal na primeira versão; preços e limite de profissionais ainda pendentes. Teste de 7 dias para usuários iniciais foi proposto; elegibilidade, necessidade de cartão e cobrança ao término ainda serão definidos. Não usar renovação surpresa. Mostrar próximo vencimento e cancelamento acessível.

Trimestral e anual ficam planejados. Cliente gratuito e profissional pagante são proposta de modelo, não tabela final aprovada. Não usar a taxa de cancelamento como receita da plataforma.

## 11. Comunicação

Eventos: nova reserva, confirmação, lembrete, remarcação, cancelamento, aviso de atraso, pagamento e resposta de suporte. Preferências de antecedência e canal por usuário. Começar com canais realmente integrados; não prometer WhatsApp, SMS ou push antes de contratados e testados.

Confirmações e lembretes independentes de publicidade. Avisos de falha de entrega registrados. Tentativas limitadas com espera progressiva e chave antirrepetição. Se a reserva mudar ou cancelar, invalidar lembretes antigos. Respeitar fuso horário e consentimentos. Aviso de atraso apresenta opções; não desloca toda a agenda sem aceite.

## 12. Perfis, identidade, idade e privacidade

Nome, contato, foto opcional, especialidade, apresentação, região, portfólio e redes sociais. Distinção entre “e-mail confirmado”, “identidade verificada” e “qualificação verificada”; nenhum selo equivale a garantia de qualidade.

Google é uma opção de login planejada; aceitar outros provedores de e-mail. Não pedir senha do Gmail. Vinculação e recuperação exigem fluxo seguro.

Público pretendido: a partir de 16 anos. Regras para participantes de 16–17 anos, responsáveis, contratação e recebimentos precisam de validação especializada e compatibilidade com provedores antes de ativar esse público. Isso não está resolvido apenas por um campo de data de nascimento.

CPF e verificação documental apenas quando necessários e por integração apropriada. Biometria facial obrigatória foi adiada. Não coletar documentos reais no protótipo. Especialidade declarada e comprovação documental devem ter rótulos distintos.

Localização por permissão ou endereço digitado; não exigir GPS continuamente. Endereço exato do cliente restrito ao atendimento autorizado; perfil público mostra região apropriada. Foto e redes sociais não devem expor informações privadas por padrão.

## 13. Avaliações, bloqueios e denúncias

Avaliações de profissionais por clientes: após atendimento elegível, com uma avaliação por reserva, direito de resposta, moderação e contestação. Publicação de notas exige dados reais e transparência; não apresentar notas fictícias como reputação.

Avaliação pública de clientes foi adiada. Profissional acessa histórico privado de presença/falta relacionado ao seu atendimento, com correção de erros.

Bloqueio limita novas reservas/interações, preservando canais necessários a estorno e atendimento de reservas vigentes. Denúncia registra categoria, texto, anexos apropriados, protocolo, responsável e resultado. Não suspender automaticamente apenas pelo número de denúncias. Suporte revisa casos relevantes.

## 14. Segurança e recuperação automática

Requisitos a implementar e verificar, sem promessa de sistema invulnerável:

- Isolamento entre empresas, autorização por papel, sessões seguras, proteção de credenciais e validação de entrada.
- Proteções contra abuso, limites de tentativas e trilha de auditoria.
- Dados mínimos, prazos de retenção definidos e fluxos para acesso, correção, exportação e exclusão conforme obrigações aplicáveis.
- Logs sem documentos, senhas, tokens ou dados completos de pagamento.
- Monitoramento de erro, latência, disponibilidade, filas e consistência de reserva/pagamento.
- Nova tentativa automática apenas para falhas recuperáveis e operações seguras, com limites e deduplicação.
- Reinício supervisionado quando suportado pela infraestrutura.
- Atualizações graduais; reversão apenas quando compatível com dados e migrações.
- Backups automáticos e testes periódicos de restauração em ambiente isolado. Frequência, retenção e objetivos de recuperação serão definidos com custo e infraestrutura.
- Pagamento incerto: consultar o provedor e reconciliar; nunca marcar “pago” por suposição.
- Incidente de segurança, perda/corrupção de dados ou cobrança incorreta: conter e alertar uma pessoa responsável.

O sistema não reescreve seu código, altera saldos ou restaura produção autonomamente para tentar corrigir uma falha. O responsável por incidentes e os canais de plantão precisam existir antes do uso comercial.

## 15. Sequência de entrega

| Etapa | Entrega |
|---|---|
| Design atual | Identidade, telas demonstrativas, fluxos e especificação funcional. |
| Primeira versão | Cadastro, papéis, perfil, catálogo, adicionais, agenda, disponibilidade, reservas manuais/online, remarcação, cancelamento, suporte, temas e trilha de alterações. |
| Integrações para lançamento | Canais de lembrete, identidade necessária, pagamento/assinatura se ativados, backups e alertas. Sem integrações prontas, limitar explicitamente o produto. |
| Evolução próxima | Recorrência, importação/exportação, lista de espera e recuperação de vagas, avaliações elegíveis. |
| Evolução avançada | Rotas por endereço, substituição entre profissionais com consentimento, novos segmentos, planos trimestrais/anuais. |
| Adiado | Facial obrigatório para todos, avaliações públicas de clientes e rede social interna. |

## 16. Critérios de aceite do futuro app

1. Duas pessoas tentando o mesmo horário não conseguem duas confirmações conflitantes.
2. Adicional altera total e duração, recalculando disponibilidade.
3. Trocar catálogo não altera o preço de reserva já confirmada.
4. Profissional só acessa dados autorizados; empresa A nunca acessa empresa B.
5. Cancelamento mostra condição e valor antes de confirmar; nenhum valor é cobrado sem regra e autorização aplicáveis.
6. Pagamento repetido ou evento duplicado não gera nova cobrança nem repasse.
7. Remarcar/cancelar invalida lembrete anterior.
8. Cliente sem GPS pode informar região/endereço manualmente.
9. Fluxo completo funciona em celular, teclado e temas claro/escuro.
10. Queda de conexão apresenta estado recuperável sem perder ou duplicar operação.
11. Exportação respeita escopo; restauração é testada antes de depender do backup.
12. Vagas vazias, catálogo vazio, conta bloqueada, pagamento pendente e atendimento indisponível têm mensagens e próximos passos.
13. Solicitação de suporte tem protocolo; denúncia não equivale a condenação automática.
14. Integrações indisponíveis são comunicadas; demonstrações nunca são tratadas como operações reais.

## 17. Decisões para a etapa de desenvolvimento

Nome definitivo e disponibilidade; cidade piloto; número de profissionais; responsável operacional; regras de idade; cancelamento final; valor e condições de assinatura; tarifas e repasses; canais de aviso; provedor de identidade/pagamento; política de dados; metas de disponibilidade e recuperação.

Nenhuma dessas decisões exige coletar dados reais durante a revisão do design.


# Investigação de Segurança em TV Box MXQ PRO

> Uma investigação independente sobre uma TV Box que instalava aplicativos sem minha solicitação. Um ThinkPad T440, Debian, ferramentas de rede e muitas perguntas depois, chegamos a um parecer de risco.

<p align="center">
  <strong>Risco elevado | Comprometimento não confirmado</strong>
</p>

## Sobre o projeto

Este projeto documenta uma investigação de segurança que realizei em uma TV Box comercializada como **SMAR1 PRO 4KHD**, identificada fisicamente como **MXQ PRO**.

Tudo começou quando percebi que o aparelho instalava ou apresentava novos aplicativos sem que eu tivesse solicitado. Além disso, a organização da interface mudava de tempos em tempos.

O que parecia ser apenas um problema com aplicativos acabou se transformando em uma oportunidade de estudar, na prática, redes, Android, Linux e segurança da informação.

## Objetivos

Investigar a procedência e o comportamento do equipamento, procurando identificar:

- Aplicativos com permissões excessivas.
- Mecanismos de instalação automática.
- Inconsistências no firmware e nas informações do Android.
- Serviços de rede potencialmente desconhecidos.
- Indícios de malware ou comprometimento.

## O que encontrei

Durante a investigação, identifiquei:

- Histórico de suspensão de homologação da Anatel relacionado à família de produtos MXQ PRO e a irregularidades no software instalado.
- Relatórios de fiscalização envolvendo unidades da mesma família, com aplicativos destinados ao acesso não autorizado a conteúdos de TV por assinatura.
- Aplicativos com permissões especiais para instalar fontes desconhecidas, sobrepor telas e modificar configurações do sistema.
- Relatos de instalação recorrente de aplicativos sem minha solicitação.
- Inconsistências entre a versão do Android apresentada e os identificadores de compilação, além de um patch de segurança declarado de 2019.
- Uma porta TCP aberta, na qual não foi possível identificar o serviço responsável.

Também encontrei uma correspondência entre o pacote `com.systemguard.android` e um indicador mencionado em uma investigação de outras TV Boxes. Essa correspondência foi tratada como pista, não como prova de infecção da minha unidade.

## Ferramentas utilizadas

| Ferramenta | Finalidade |
|---|---|
| Debian GNU/Linux | Ambiente de investigação |
| Nmap | Reconhecimento de portas TCP |
| ADB | Tentativa de acesso técnico ao Android |
| tcpdump | Tentativa de captura e análise de tráfego |
| Documentação da Anatel | Consulta de homologações e fiscalizações |

## Resultados e limitações

A varredura completa de portas TCP identificou uma porta aberta: `14035/tcp`, classificada pelo Nmap como `tcpwrapped`. Não consegui identificar o processo ou serviço responsável.

Também tentei estabelecer uma conexão ADB, mas não obtive acesso funcional ao dispositivo.

Durante um teste em uma rede isolada, desinstalei os aplicativos SystemGuard e Assistant. Após a reinicialização e o período de observação, eles não foram reinstalados automaticamente.

A tentativa de captura de tráfego com tcpdump não conseguiu registrar comunicações da TV Box.

Não consegui extrair os APKs para verificar hashes, assinaturas digitais ou realizar análise estática. Portanto, não foi possível confirmar tecnicamente a presença de malware.

## Parecer final

Classifiquei o equipamento como:

**RISCO ELEVADO, COMPROMETIMENTO NÃO CONFIRMADO.**

As evidências levantadas não permitem afirmar categoricamente que a TV Box estava infectada. Entretanto, as inconsistências do firmware, o histórico documental, as permissões encontradas e os comportamentos relatados não permitiram estabelecer confiança suficiente no equipamento.

Minha recomendação foi não utilizá-lo na rede doméstica principal e substituí-lo por um dispositivo com procedência e suporte verificáveis.

## O que aprendi

Mais do que investigar um equipamento, este projeto me permitiu experimentar etapas reais de uma investigação de segurança:

- Formular hipóteses a partir de comportamentos observados.
- Examinar permissões e componentes de um sistema Android.
- Utilizar ferramentas de reconhecimento de rede.
- Consultar documentação regulatória.
- Registrar evidências e limitações.
- Diferenciar suspeitas, indícios e conclusões comprovadas.

Uma das principais lições foi entender que não encontrar provas de malware não significa que um equipamento seja seguro. E que reconhecer os limites de uma investigação também faz parte do trabalho.

## Estrutura do repositório

O projeto está organizado em três áreas principais:

- [Documentação e relatório completo](docs/README.md)
- [Metodologia da investigação](metodologia/README.md)
- [Catálogo de evidências visuais](evidencias/README.md)
- **[Missão TV Box - Guia Completo de Investigação de Segurança (PDF)](Manual_Missao_TVBox_Investigacao_Seguranca_Iniciante_ARCADE.pdf)**

O relatório completo está disponível em [PDF](docs/Relatorio_Investigacao_TVBox_MXQ_a.pdf).

## Aviso

Este é um estudo independente, realizado em equipamento de minha propriedade, com finalidade educacional e de aprendizado em segurança da informação.

O conteúdo não constitui laudo pericial, certificação de segurança ou manifestação oficial da Anatel.

---

**Investigação conduzida por Clériston Albino**

*Entre códigos, café e bugs, construindo meu próximo nível.*

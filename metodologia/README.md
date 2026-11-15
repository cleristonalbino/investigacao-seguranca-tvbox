
# Metodologia da investigação

## 1. Abordagem

Conduzi a investigação por etapas, começando pela observação do equipamento e avançando para a análise das permissões, do firmware e do comportamento de rede.

Procurei preservar o funcionamento do aparelho e evitar alterações desnecessárias durante a coleta de informações.

O trabalho foi organizado em etapas complementares.

## 2. Ambiente de investigação

Utilizei os seguintes recursos:

- **Notebook:** Lenovo ThinkPad T440.
- **Sistema operacional:** Debian GNU/Linux.
- **TV Box:** SMAR1 PRO 4KHD, identificada fisicamente como MXQ PRO.
- **Nmap:** reconhecimento de portas e tentativa de identificação de serviços.
- **ADB:** tentativa de comunicação com o Android.
- **tcpdump:** tentativa de captura de tráfego de rede.

## 3. Inspeção do Android

Inicialmente, consultei as informações apresentadas pelo próprio sistema, incluindo:

- Modelo e informações de compilação.
- Versão do Android informada pela interface.
- Versão do kernel.
- Nível de atualização de segurança.
- Opções de desenvolvedor.

Também examinei permissões especiais concedidas aos aplicativos, dando atenção à instalação de aplicativos desconhecidos, sobreposição de telas, modificação de configurações e acesso de utilização.

Essa etapa ajudou a identificar componentes que mereciam investigação adicional.

## 4. Reconhecimento de rede com Nmap

Conectei a TV Box à rede e identifiquei seu endereço IP local.

Executei inicialmente:

```bash
nmap -sV 192.168.0.100
```

O resultado mostrou as 1.000 portas TCP mais comuns como fechadas.

Em seguida, ampliei a análise:

```bash
nmap -p- 192.168.0.100
```

A varredura completa identificou uma porta TCP aberta:

- `14035/tcp`: serviço não identificado.

Realizei então tentativas adicionais de identificação:

```bash
nmap -sV -p 14035 192.168.0.100
```

```bash
nmap -sV --version-all --reason -p 14035 192.168.0.100
```

O Nmap classificou o serviço como `tcpwrapped`, mas não conseguiu identificar o processo responsável.

A presença de uma porta aberta foi tratada como um ponto de investigação, não como prova de malware.

## 5. Tentativas de acesso com ADB

Instalei o Android Debug Bridge no Debian e tentei estabelecer comunicação com a TV Box.

Foram realizadas tentativas utilizando as portas 5555 e 14035.

As conexões não foram estabelecidas e o comando `adb devices` não apresentou dispositivos disponíveis.

Também avaliei a possibilidade de conexão física, mas não dispunha de um cabo de dados USB adequado.

Consequentemente, não consegui extrair os aplicativos instalados para análise dos arquivos APK, assinaturas ou hashes.

## 6. Tentativas de captura de tráfego

Utilizei o tcpdump para tentar observar as comunicações de rede da TV Box.

Inicialmente, tentei criar um ponto de acesso Wi-Fi pelo ThinkPad, mas o equipamento não conseguiu localizar a rede criada.

As capturas realizadas registraram tráfego local do próprio Debian, não comunicações da TV Box.

Posteriormente, utilizei o hotspot do smartphone, conectado exclusivamente aos dados móveis, para realizar uma observação em rede separada da rede doméstica.

## 7. Teste comportamental em rede isolada

Com a TV Box conectada ao hotspot do smartphone, observei seu comportamento em repouso e após uma reinicialização.

Os aplicativos SystemGuard e Assistant, previamente desinstalados, não reapareceram automaticamente durante o período observado.

Também não percebi consumo relevante de dados móveis.

Esse resultado não comprova ausência de comunicação externa ou de mecanismos de reinstalação, mas permitiu registrar o comportamento observado nas condições do teste.

## 8. Consulta documental

Consultei registros e documentos públicos da Anatel por meio do sistema SEI.

O objetivo foi compreender o histórico regulatório relacionado à família de equipamentos MXQ PRO e confrontar os documentos encontrados com as características observadas na minha unidade.

As correspondências documentais foram tratadas como contexto relevante, sem presumir que todas as unidades fiscalizadas fossem tecnicamente idênticas à minha.

## 9. Interpretação e limitações

Durante toda a investigação, procurei separar:

- Evidências diretamente observadas.
- Informações obtidas em documentação pública.
- Hipóteses que ainda precisavam de confirmação.
- Limitações técnicas que impediram determinados testes.

Uma porta aberta não comprova infecção. Uma permissão sensível não comprova comportamento malicioso. Da mesma forma, não encontrar evidências de malware não significa que o equipamento seja seguro.

## 10. Encerramento

A investigação foi encerrada com a classificação:

**Risco elevado, comprometimento não confirmado.**

As evidências levantadas justificaram a recomendação de não utilizar o equipamento na rede doméstica principal.

As limitações de acesso ao Android e de análise dos aplicativos impediram uma confirmação técnica de malware.

O objetivo desta documentação é apresentar os procedimentos realizados, os resultados obtidos e os limites do que foi possível concluir.

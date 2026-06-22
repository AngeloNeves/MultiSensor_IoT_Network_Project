# Guia de Início Rápido e Operação do Sistema de Monitorização Doméstica

Este documento fornece instruções sobre como iniciar e verificar os componentes essenciais do seu sistema de monitorização doméstica, incluindo o broker MQTT (Mosquitto) e o Node-RED, bem como aceder ao dashboard.

## 1. Pré-requisitos

Certifique-se de que tem os seguintes componentes instalados e configurados:

*   **Mosquitto MQTT Broker:** Instalado e configurado com SSL/TLS (conforme as instruções anteriores).
*   **Node.js e npm:** Necessários para o Node-RED.
*   **Node-RED:** Instalado globalmente via npm.
*   **Certificados SSL/TLS:** Os ficheiros `ca.crt`, `server.crt` e `server.key` devem estar no diretório `C:/Program Files/mosquitto/certs/` (ou onde os configurou).

## 2. Iniciar o Mosquitto MQTT Broker

O Mosquitto deve ser configurado para iniciar automaticamente como um serviço do Windows. No entanto, pode verificar o seu estado e iniciá-lo manualmente se necessário.

### 2.1. Verificar o Estado do Serviço Mosquitto

1.  Abra o **Gestor de Tarefas** (Ctrl+Shift+Esc).
2.  Vá para o separador **Serviços**.
3.  Procure por `Mosquitto Broker`.
4.  Verifique a coluna **Estado**. Deverá estar `Em execução`.

### 2.2. Iniciar/Reiniciar o Serviço Mosquitto (se necessário)

Se o serviço não estiver em execução ou precisar de ser reiniciado:

1.  Abra o **Prompt de Comando** ou **PowerShell como Administrador**.
2.  Para iniciar o serviço:
    ```bash
    net start mosquitto
    ```
3.  Para parar o serviço:
    ```bash
    net stop mosquitto
    ```
4.  Para reiniciar o serviço:
    ```bash
    net stop mosquitto
    net start mosquitto
    ```
    Ou, mais simplesmente, pode fazê-lo através do Gestor de Tarefas, clicando com o botão direito no serviço e selecionando "Iniciar" ou "Reiniciar".

## 3. Iniciar o Node-RED

O Node-RED é a interface onde os seus flows estão configurados.

1.  Abra o **Prompt de Comando** ou **PowerShell**.
2.  Navegue até ao diretório onde guarda os seus ficheiros de configuração do Node-RED (se tiver um diretório específico, caso contrário, pode iniciar a partir de qualquer diretório onde o Node-RED esteja acessível via PATH).
3.  Execute o comando para iniciar o Node-RED:
    ```bash
    node-red
    ```
4.  Aguarde até ver mensagens como `[info] Server now running at http://127.0.0.1:1880/` (ou o endereço IP do seu computador). Isso indica que o Node-RED está a funcionar.

    *   **Nota:** O Node-RED irá ocupar esta janela de terminal enquanto estiver em execução. Para o manter a correr em segundo plano (especialmente em sistemas Linux/macOS) pode usar ferramentas como `pm2` ou configurá-lo como um serviço. Para Windows, pode simplesmente manter a janela aberta ou explorar ferramentas como `nssm` para o executar como serviço.

## 4. Aceder ao Node-RED Dashboard

O dashboard é a sua interface visual para monitorizar os sensores.

1.  Certifique-se de que o Node-RED está em execução (ver passo 3).
2.  Abra o seu navegador web preferido.
3.  Introduza o seguinte endereço na barra de URL:
    ```
    http://localhost:1880/ui
    ```
    *   **Nota:** Se o Node-RED estiver a correr noutro computador na sua rede, substitua `localhost` pelo endereço IP desse computador (ex: `http://192.168.1.100:1880/ui`).

## 5. Testar os Sensores (Opcional, mas Recomendado)

Para garantir que tudo está a comunicar corretamente, pode usar os comandos `mosquitto_pub` para simular as mensagens dos sensores.

1.  Consulte o ficheiro `MQTT_Topics_and_Commands.md` no seu repositório Git para obter a lista completa de comandos de teste para cada sensor.
2.  Execute os comandos num terminal separado (não o terminal onde o Node-RED está a correr).
3.  Observe o seu dashboard em `http://localhost:1880/ui` para confirmar que os valores dos sensores são atualizados.

## 6. Resolução de Problemas Comuns

*   **Node-RED não inicia:**
    *   Verifique se o Node.js está instalado corretamente (`node -v` e `npm -v`).
    *   Verifique se o Node-RED está instalado globalmente (`node-red -v`). Se não, execute `npm install -g node-red`.
    *   Verifique se a porta `1880` não está a ser usada por outra aplicação.
*   **Dashboard não carrega ou não mostra dados:**
    *   Certifique-se de que o Node-RED está a correr.
    *   Verifique a consola do navegador (F12) para erros.
    *   Verifique os logs do Node-RED no terminal para mensagens de erro.
    *   Confirme que o broker MQTT está a correr (ver passo 2).
    *   Verifique as configurações dos nós `MQTT In` no Node-RED para garantir que os tópicos e o servidor MQTT estão corretos.
*   **Mosquitto não inicia:**
    *   Verifique os logs do Mosquitto (geralmente em `C:\Program Files\mosquitto\mosquitto.log` ou similar) para mensagens de erro.
    *   Confirme que o ficheiro de configuração `mosquitto.conf` está correto e que os caminhos dos certificados estão válidos.
    *   Verifique se a porta `8883` (ou a porta que configurou) não está a ser usada por outra aplicação.

---

Este guia será um recurso valioso! Depois de o criar, não se esqueça de o adicionar, fazer commit e fazer push para o seu repositório Git.

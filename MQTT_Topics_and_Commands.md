# Documentação MQTT para o Sistema de Monitorização Doméstica

Este documento detalha os tópicos MQTT utilizados e os comandos `mosquitto_pub` para testar cada sensor no sistema.

## Configuração do `mosquitto_pub`

Assuma que o `mosquitto_pub.exe` está no diretório atual e que o `ca.crt` está em "C:/Program Files/mosquitto/certs/ca.crt". Ajuste os caminhos conforme necessário.

**Parâmetros Comuns:**
*   `-h localhost`: Host do broker MQTT.
*   `-p 8883`: Porta SSL/TLS do broker.
*   `--cafile "C:/Program Files/mosquitto/certs/ca.crt"`: Caminho para o certificado da Certificate Authority.
*   `-t "tópico"`: O tópico MQTT.
*   `-m "mensagem_json"`: A mensagem em formato JSON.

---

## Sensores e Comandos de Teste

### 1. Sensor de Temperatura
*   **Tópico:** `home/environment/temperature`
*   **Formato da Mensagem:** `{"temperatura": VALOR}`

    *   **Exemplo (23.5°C):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/environment/temperature" -m "{\"temperatura\": 23.5}"
        ```

### 2. Sensor de Humidade
*   **Tópico:** `home/environment/humidity`
*   **Formato da Mensagem:** `{"humidade": VALOR}`

    *   **Exemplo (60%):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/environment/humidity" -m "{\"humidade\": 60}"
        ```

### 3. Sensor de Porta/Janela
*   **Tópico:** `home/security/door_window`
*   **Formato da Mensagem:** `{"estado": "aberta"}` ou `{"estado": "fechada"}`

    *   **Exemplo (Aberta):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/security/door_window" -m "{\"estado\": \"aberta\"}"
        ```
    *   **Exemplo (Fechada):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/security/door_window" -m "{\"estado\": \"fechada\"}"
        ```

### 4. Sensor de Inundação
*   **Tópico:** `home/environment/flood`
*   **Formato da Mensagem:** `{"estado": "Alerta"}` ou `{"estado": "normal"}`

    *   **Exemplo (Alerta):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/environment/flood" -m "{\"estado\": \"Alerta\"}"
        ```
    *   **Exemplo (Normal):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/environment/flood" -m "{\"estado\": \"normal\"}"
        ```

### 5. Sensor de Movimento
*   **Tópico:** `home/security/motion`
*   **Formato da Mensagem:** `{"detecao": "movimento detetado"}` ou `{"detecao": "sem movimento"}`

    *   **Exemplo (Movimento Detetado):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/security/motion" -m "{\"detecao\": \"movimento detetado\"}"
        ```
    *   **Exemplo (Sem Movimento):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/security/motion" -m "{\"detecao\": \"sem movimento\"}"
        ```

### 6. Sensor de Fumo
*   **Tópico:** `home/security/smoke`
*   **Formato da Mensagem:** `{"estado": "Fumo Detetado"}` ou `{"estado": "Normal"}`

    *   **Exemplo (Fumo Detetado):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/security/smoke" -m "{\"estado\": \"Fumo Detetado\"}"
        ```
    *   **Exemplo (Normal):**
        ```bash
        ./mosquitto_pub.exe -h localhost -p 8883 --cafile "C:/Program Files/mosquitto/certs/ca.crt" -t "home/security/smoke" -m "{\"estado\": \"Normal\"}"
        ```
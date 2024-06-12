 
# Missão Prática | Nível 5 | Mundo 4

### Objetivo

Este projeto esta dividido em duas fases que são :

 - Fase 1, consiste em um sistema para simulação, coleta e visualização de dados de dispositivos IoT. O projeto inclui um código Python que simula um sensor IoT, um servidor Node.js para receber e transmitir os dados, e uma interface web para visualizar esses dados em tempo real.
 
 - Fase 2 , tem o objetivo de migrar a aplicação local para a nuvem, utilizando os serviços do Azure para hospedar a aplicação e gerenciar a infraestrutura.


obs: todo projeto segue a especificação : https://sway.cloud.microsoft/s/pAU9GmfP8IF2OLSg/embed

## Fase 1: Configuração Inicial e Simulação utilizando IoT

### Configuração do Azure IoT Hub

1. **Criar um Azure IoT Hub**:
   - Acesse o portal do Azure e crie um novo IoT Hub.
   - Anote o nome do IoT Hub e a chave de conexão.

![image](images/azure.hub.IoT.png)

2. **Registrar um dispositivo no IoT Hub**:
   - No IoT Hub, registre um novo dispositivo e anote a string de conexão do dispositivo.

3. **Adicionar um grupo de consumidores**:
   - Adicione um grupo de consumidores ao IoT Hub para permitir a leitura de eventos.

### Configuração do Código Python (Simulador de Sensor)

#### Objetivo

O código Python simula um sensor IoT que envia dados de temperatura e umidade para o Azure IoT Hub.
    
![image](images/emulador%20python.png)
 
#### Configuração

1. **Instalar Dependências**:
   - Instalação da biblioteca `azure-iot-device` e `python-dotenv`:
     ```sh
     pip install azure-iot-device python-dotenv
     ```

2. **Criação de um arquivo `.env`** no diretório do seu script Python com a string de conexão do 

    ![image](images/ponto_env_python.png)

dispositivo:

  obtenha sua connect string pelo cloud shell
   ```sh
  az iot hub show-connection-string --hub-name <MyHubName> --policy-name service
   ```
e cole em

   ```sh
   CONNECTION_STRING= <MyconnectString>
   ```

3. **Executar o Script Python (simulador do sensor de temperatura)**:
   
   python sensor.py

   
   ```sh
   npm start ou pelo vscode ou apenas dando um double click no arquivo python
   ```

   ![image](images/ativando_emulador_sensor_temp_umidade.png)
    

### Configuração do Servidor Node.js

#### Objetivo

O servidor Node.js recebe os dados do IoT Hub e os transmite via WebSocket para a interface web.

#### Configuração

1. **Instalar Dependências**:
   - Instale as dependências necessárias:
     ```sh
     npm install express http ws dotenv @azure/event-hubs
     ```

2. **Criar um arquivo `.env`** no diretório do servidor com a string de conexão do IoT Hub e o grupo de consumidores:
   ```plaintext
   IotHubConnectionString= YOUR_IOT_HUB_NAME
   EventHubConsumerGroup= YOUR_CONSUMER_GROUP_NAME
   ```

3. **Servidor Node.js (`server.js`)**:
   ```sh
   Este código configura um servidor web que serve arquivos estáticos e 
   redireciona todas as requisições para a raiz. Ele também configura um 
   WebSocket para transmitir dados recebidos vindos de 'Azure IoT Hub' para 
   todos o browse em tempo real.
   ```
4. **Executar o Servidor (o aplicativo web local)**:

### Interface Web

1. **Objetivo**:
   - A interface web se conecta ao servidor via WebSocket e exibe os dados de telemetria em tempo real.

    - Execute o arquivo 

    ![image](images/servidor_local_emacao.png)

2. **Verificar a Interface**:
   - Acesse `http://localhost:3000` no seu navegador e verifique se os dados de telemetria estão sendo exibidos corretamente.
   
   ![image](images/grafico_fase_1.png)

## Fase 2: Implementação na Nuvem e Integração com o Azure 

### Etapas 

1. **Migração para a Nuvem**:
    - Configuração de um App Service no Azure para hospedar a aplicação.
    - Configuração do repositório Git no Azure para gerenciamento de código.

2. **Configuração de Desdobramento (Deployment)**:
    - Configuração do desdobramento contínuo utilizando o Git para enviar as atualizações diretamente ao App Service.
    - Verificação das credenciais de publicação e configuração das mesmas no portal do Azure.

3. **Ativação de Emuladores Locais**:
    - **Emulador de Temperatura**: Ativar o emulador de temperatura localmente para simular os dados de entrada.
    - **Servidor Local**: Ativar o aplicativo do servidor local que emula o ambiente de produção.

4. **Desdobramento e Execução no Azure**:
    - Realizar o push do código para o repositório Git interno do Azure.
    - Executar o comando `npm start` no repositório hospedado no Azure para iniciar a aplicação.
    - Verificar o funcionamento da aplicação em produção, garantindo que ela esteja recebendo dados do emulador de temperatura e exibindo-os corretamente na interface web.

### Dificuldades e Soluções

1. **Problemas de Autenticação**:
    - Enfrentamos dificuldades com a autenticação ao tentar fazer o push para o repositório Git no Azure. Foram necessárias várias verificações e reconfigurações das credenciais de publicação.

2. **Configuração do SCM (Source Control Management)**:
    - Tivemos que habilitar a autenticação básica para SCM no portal do Azure, o que não estava ativado por padrão. Isso foi essencial para permitir o push do código para o repositório no Azure.

3. **Execução de Emuladores Locais**:
    - Garantir que os emuladores locais de temperatura e o servidor estavam corretamente configurados e funcionando antes de realizar o push para o Azure.

### Resultados Esperados
- A aplicação deveria estar configurada no Azure App Service com sucesso.
- As credenciais de publicação deveriam estar verificadas e configuradas corretamente.
- Após o push do código, o comando `npm start` deveria ser executado no repositório do Azure para iniciar a aplicação.
- A aplicação deveria ser testada no ambiente de produção, recebendo dados do emulador de temperatura e exibindo-os em tempo real na interface web.

### Resultados Alcançados
- Embora não tenha sido possível concluir o push devido a problemas de autenticação, todos os passos necessários foram identificados e documentados.
- As configurações e verificações realizadas prepararam o ambiente para uma futura tentativa de deploy.

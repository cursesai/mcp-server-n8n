# MCP Server + n8n

![Licença MIT](https://img.shields.io/badge/Licença-MIT-blue.svg)
![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-orange) 
![MCP Server](https://img.shields.io/badge/MCP%20Server-AI%20Tools-blue) 
![Docker](https://img.shields.io/badge/Docker-Container-blue) 
![Python](https://img.shields.io/badge/Python-3.x-green)

## Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Configuração do n8n](#configuração-do-n8n)
- [Criando um Workflow com AI Agent](#criando-um-workflow-com-ai-agent)
- [Testando as Ferramentas](#testando-as-ferramentas)
- [Estrutura de Diretórios e Persistência](#estrutura-de-diretórios-e-persistência)
- [Modificando o MCP Server](#modificando-o-mcp-server)
- [Considerações de Segurança](#considerações-de-segurança)
- [Documentação](#documentação)
- [Referências](#referências)


## Sobre o Projeto

Esta aplicação combina a ferramenta de automação n8n com o protocolo MCP Server para criar um ambiente de experimentação. A solução utiliza Docker para facilitar a instalação e configuração, permitindo testar facilmente os recursos do MCP Server através da interface visual do n8n.

**Componentes principais:**
- **n8n**: Plataforma de automação com interface visual
- **MCP Server**: Servidor que disponibiliza ferramentas para agentes de IA

Este projeto foi criado para fins educacionais e de experimentação.

## Pré-requisitos

Para utilizar esta aplicação, você precisará ter:

- **Docker** e **Docker Compose** instalados no seu computador
  - Windows: [Docker Desktop](https://www.docker.com/products/docker-desktop/)
  - Linux: doker.io, docker-compose e docker-buildx

## Instalação

### No Windows

1. Baixe e extraia o arquivo ZIP deste repositório ou clone-o usando Git:
   ```
   git clone https://github.com/curseai/mcp-server-n8n.git
   ```
2. Abra o Prompt de Comando ou PowerShell e navegue até a pasta do projeto:
   ```
   cd mcp-server-n8n
   ```
3. Inicie os containers Docker:
   ```
   docker-compose up -d
   ```
4. Para finalizar os containers Docker:
    ```
    docker-compose down
    ```

### No Linux

1. Baixe ou clone o repositório:
   ```
   git clone https://github.com/curseai/mcp-server-n8n.git
   ```
2. Navegue até a pasta do projeto:
   ```
   cd mcp-server-n8n
   ```
3. Inicie os containers Docker
   ```
   docker-compose up -d
   ```
4. Para finalizar os containers Docker:
    ```
    docker-compose down
    ```

> **Observação:** Ao finalizar a aplicação, os containers serão removidos. Contudo, os dados serão mantidos nos diretórios persistentes: `mcp_server`, que contém os arquivos Python responsáveis pela execução do MCP Server, e o diretório `n8n_data`, que contém os dados da aplicação n8n. Com isso, caso você deseje iniciar novamente a aplicação, os containers serão recriados com os dados armazenados na execução anterior. 



Quando a instalação for concluída, você verá uma mensagem informando que os containers foram iniciados. 
A aplicação estará disponível em: **http://localhost:5678**

## Configuração do n8n

### Acessando o n8n pela primeira vez

1. Abra seu navegador e acesse http://localhost:5678
2. Você verá a tela de boas-vindas do n8n com o formulário de criação de conta. 
3. Complete o formulário de cadastro:
   - Email: Coloque seu email
   - Nome: Seu nome
   - Senha: Uma senha segura
   - Confirmar senha: Repita a senha

4. Clique em "Next" para criar sua conta.

<img width="320" alt="img-01" src="https://github.com/user-attachments/assets/b2ce8503-3034-4b62-9302-33bd4dc4b9ec" />


5. O próximo formulário é apenas uma pesquisa e pode ser ignorado clicando em "Get Started"

<img width="320" alt="img-01" src="https://github.com/user-attachments/assets/0f40008e-44e0-48a6-a206-86eb51d715f8" />

6. A próxima tela vai oferecer a possibilidade de obtenção de uma chave de licença. Caso não deseje obter, basta clicar em "skip"

<img width="320" alt="img-01" src="https://github.com/user-attachments/assets/e96d06a4-24e5-4b25-9030-f34b0cdeb0dd" />

7. Após o cadastro, você será redirecionado para a página principal do n8n

## Criando um Workflow com AI Agent

### Criando um novo workflow

1. Na tela inicial do n8n, clique no botão "Create Workflow" no canto superior direito
2. Você será direcionado para o editor de workflows, onde verá uma tela em branco com uma grade

<img width="420" alt="img-04" src="https://github.com/user-attachments/assets/77dbbfcd-a41d-43df-bc2a-6122b9803341" />


3. Dê um nome para seu workflow, por exemplo: "Teste MCP Server" clicando em "My workflow" no canto superior esquerdo.

### Adicionando um AI Agent

1. Clique em "Add first step" para iniciar a montagem do workflow.
2. No painel esquerdo, você verá a barra de pesquisa "Search nodes..."

<img width="420" alt="img-04" src="https://github.com/user-attachments/assets/a4205089-e3c9-4bc8-ae4f-c080ce73b41a" />

3. Digite "AI Agent" na barra de pesquisa
4. Localize o nó "AI Agent" nos resultados da pesquisa
5. Clique e arraste o nó "AI Agent" para o centro da tela
6. O painel de configuração do "AI Agent" será exibido na sequência. Para testar o MCP Server, podemos deixar os parametros sem alteração. Em seguida, podemos fechar este painel clicando em "<- Back to canvas" no canto superior esquerdo da tela. 

<img width="420" alt="img-06" src="https://github.com/user-attachments/assets/ca2d90ce-b9b3-4d9e-8ab4-632a74332656" />


### Configurando o Modelo LLM (Chat Model)

1. Para adicionar um modelo LLM no AI Agent clique em "+ Chat Model"
2. Na aba lateral selecione o modelo na aba lateral. Pesquise o seu modelo LLM na barra de pesquisa "Search nodes..."
3. Selecione o modelo LLM que deseja usar (por exemplo: "OpenAI" ou "Anthropic")

<img width="320" alt="img-07" src="https://github.com/user-attachments/assets/6bcf3a96-9cb4-4c8b-8f8c-2cf276d8a3df" />


4. Após selecionar o modelo, você verá um campo "Credential to connect with" que mostra "Select Credential"

<img width="320" alt="img-07" src="https://github.com/user-attachments/assets/766bad87-5f47-45a8-9415-441030711acf" />

5. Clique em "Select Credential" em seguida clique "Create new credential" para abrir a janela de configuração de credenciais
6. Na janela de credenciais, você verá:
   - API Key: campo para inserir sua chave de API
   
<img width="420" alt="img-09" src="https://github.com/user-attachments/assets/779312bc-4583-4a5e-aeee-6a787dc6a2b1" />

   > **Observação**: Para obter uma API Key:
   > - Para OpenAI: Acesse [platform.openai.com](https://platform.openai.com), crie uma conta e gere uma API Key
   > - Para Anthropic: Acesse [console.anthropic.com](https://console.anthropic.com), crie uma conta e gere uma API Key

7. Insira sua API Key no campo correspondente
8. Clique em "Save" para salvar suas credenciais

9. De volta à configuração do AI Agent, você verá campos adicionais para ajustar os parâmetros do modelo:
   - Model: selecione o modelo específico (como "gpt-4o-mini" ou "claude-3.7-Sonnet")
10. Configure esses parâmetros conforme sua preferência
11. Clique em "<- Back to canvas" no canto superior esquerdo da tela para voltar ao workflow

### Configurando a Memória

1. Para adicionar uma memória no AI Agent clique em "+ Memory"
2. Na barra lateral clique no node "Simple Memory"

<img width="320" alt="img-10" src="https://github.com/user-attachments/assets/06f17176-47b7-46f5-93aa-6eba78919341" />


3. No campo "Context Window Length", defina o tamanho da janela de contexto (recomendado: 20)

<img width="320" alt="img-11" src="https://github.com/user-attachments/assets/a95486e6-29d1-4663-8e3f-fdeb8affc839" />

4. Clique em "<- Back to canvas" no canto superior esquerdo da tela para voltar ao workflow

### Configurando o MCP Client

1. Para adicionar um MCP Client no AI Agent clique em "+ Tools"

<img width="420" alt="img-12" src="https://github.com/user-attachments/assets/5230bf5d-c092-4711-9ae7-7ac70d4884e5" />

3. Na barra lateral, procure na barra de pesquisa "Search nodes..." por "MCP Client Tool" e selecione na lista de ferramentas disponíveis
5. Configure o MCP Client com os seguintes parâmetros:
   - **SSE Endpoint**: Digite exatamente `http://mcp_server:8000/sse`
   - **Authentication**: Como estamos em um ambiente local e isolado, podemos deixar o campo "Authentication" como "None".
   > **Atenção** Esta aplicação é para fins de experimentação e aprendizado. Para uso em produção você deve usar algum método de autenticação.

<img width="320" alt="img-13" src="https://github.com/user-attachments/assets/505649bc-95a4-4bb0-9bc7-9dd79073acfa" />


   - **Tools**: Clique no campo e selecione "All" para usar todas as ferramentas disponíveis
   > **Dica**: Se quiser verificar a conexão com o MCP Server, você pode selecionar "Selected" em vez de "All". Isso mostrará uma lista das ferramentas disponíveis. Se a lista aparecer, significa que a conexão está funcionando corretamente.
   
<img width="520" alt="img-14" src="https://github.com/user-attachments/assets/e1e746a5-b0b4-4822-8658-c984edb81dd0" />

6. Após configurar todos os parâmetros, clique em "<- Back to canvas" no canto superior esquerdo da tela para voltar ao workflow
7. Após voltar ao workflow, clique em "Save" no canto superiro direito para salvar as configurações realizadas no seu workflow.

## Testando as Ferramentas

Depois de configurar o AI Agent, você pode testar as ferramentas do MCP Server:

1. No painel de configuração do AI Agent, role até o final da página
2. Clique no botão "Open Chat" na parte inferior do painel de configuração

<img width="520" alt="img-15" src="https://github.com/user-attachments/assets/c3268cb5-443f-4f6b-b0a8-68aed94cd6c4" />

3. Uma janela de chat será aberta, semelhante a um chat de IA
4. No campo de texto na parte inferior do chat, experimente os seguintes comandos:
   - Digite `ping` e pressione Enter - o agente deve responder com "pong"
   - Digite `acho eu` e pressione Enter - o agente deve responder com "acho eu I love you!"

<img width="420" alt="img-16" src="https://github.com/user-attachments/assets/693be981-26cc-4ed0-a0ac-d4ed2c6f93f7" />


Esses comandos acionam as ferramentas disponibilizadas pelo MCP Server, demonstrando que a conexão entre o n8n e o MCP Server está funcionando corretamente.

## Estrutura de Diretórios e Persistência

Quando você executa a aplicação pela primeira vez, são criados dois diretórios importantes na pasta do projeto:

### Diretório `n8n_data`

Este diretório armazena todos os dados do n8n, incluindo:
- Seus workflows criados
- Credenciais configuradas
- Configurações da aplicação

O diretório `n8n_data` é essencial para manter suas configurações e workflows mesmo após reiniciar os containers.

### Diretório `mcp_server`

Este diretório contém os arquivos do MCP Server, incluindo:
- O ambiente virtual Python (pasta `.venv`)
- O arquivo `server.py` que contém o código do servidor MCP

Para acessar o arquivo `server.py`, navegue até a pasta do projeto e abra o diretório `mcp_server`. O arquivo está localizado na raiz deste diretório:

No Windows:
```
explorer mcp_server
```

No Linux:
```
ls -la mcp_server
```

Este arquivo contém o código Python que define as ferramentas disponibilizadas pelo MCP Server (atualmente `ping` e `echo`).

## Modificando o MCP Server

Você pode testar e implementar novas funcionalidades ao MCP Server modificando o arquivo `server.py`.

### Editando o arquivo `server.py`

1. Navegue até o diretório `mcp_server` na pasta do projeto
2. Abra o arquivo `server.py` com qualquer editor de texto (como Notepad, VSCode, etc.)
3. O arquivo contém um código Python que define o servidor MCP. No código abaixo podemos ver a definição das suas ferramentas que são usadas no n8n.
   ```python
   from mcp.server.fastmcp import FastMCP
    
   mcp = FastMCP('ping_server')

   @mcp.tool(name='ping')
   def ping() -> str:
       """
       A simple ping tool that returns a message.
       """
       return 'pong'

   @mcp.tool(name='echo')
   def echo(message: str) -> str:
       """
       An echo tool that returns the message sent to it.
       """
       return f"{message} I love you!"

   if __name__ == '__main__':
       mcp.run(transport='sse')
   ```
Além das `tools` é possível adicionar `resources` e `prompt`. Para mais informações consulte a [documentação oficial do MCP Server](https://modelcontextprotocol.io/)

### Aplicando as alterações

Após modificar o arquivo `server.py`, você precisa reiniciar os containers para que as alterações sejam reconhecidas pelo MCP Client no n8n:

1. Abra um terminal ou prompt de comando
2. Navegue até a pasta do projeto
3. Execute o comando:
   ```
   docker-compose restart
   ```

4. Aguarde até que ambos os containers sejam reiniciados
5. Volte ao n8n e teste sua nova ferramenta


## Considerações de Segurança

Esta aplicação foi desenvolvida para fins de experimentação e aprendizado, portanto:

- Não foram implementados procedimentos de autenticação no MCP Server
- Recomenda-se usar apenas em ambientes de teste isolados
- Não utilize em ambientes de produção sem implementar medidas de segurança adequadas

## Documentação

Para mais informações sobre o Model Context Protocol:

- [Documentação oficial do MCP](https://modelcontextprotocol.io/)


## Referências

- [Python SDK do Model Context Protocol](https://github.com/modelcontextprotocol/python-sdk)
- [Exemplos de servidores MCP](https://github.com/modelcontextprotocol/servers)


## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para mais detalhes.

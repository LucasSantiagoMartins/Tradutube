
# Arquitetura do Projeto TRADUTUBE

## 1. Arquitetura Geral

### 1.1 Frontend (Cliente)
- **Plataforma**: aplicativo móvel (Flutter)
- **Responsabilidade**:
  - Interface de usuário para inserção do URL do YouTube.
  - Opções para selecionar o idioma de tradução.
  - Exibição do status de conversão.
  - Exibição do áudio gerado.

### 1.2 Backend (API)
- **Framework**: C# com ASP.NET Core (para a Web API)
- **Responsabilidade**:
  - Receber o URL do vídeo.
  - Validar a URL do YouTube.
  - Recuperar o vídeo e suas legendas (se disponíveis).
  - Traduzir as legendas ou transcrever áudio (caso não haja legendas).
  - Gerar o áudio traduzido usando a tecnologia de TTS (ElevenLabs).
  - Armazenar o áudio gerado e fornecer o link para streaming.

### 1.3 Microservices
- **Microserviços para Transcrição e Tradução**: Usar APIs como **Whisper (OpenAI)** para transcrição de áudio (caso as legendas não estejam disponíveis) e **Google Translate** para tradução.
- **Microserviço de Text-to-Speech**: Integrar com serviços como **ElevenLabs**, **Google Cloud TTS** ou **Amazon Polly** para gerar o áudio com a voz realista.

### 1.4 Banco de Dados
- **Banco Relacional**: Usar PostgreSQL para armazenar dados como URLs processados, status, histórico de traduções e dados de usuário.
- **Armazenamento de Arquivos**: Usar AWS S3 ou Google Cloud Storage para armazenar os áudios gerados.

### 1.5 Queue System
- **RabbitMQ e Celery**: Usar para gerenciar a fila de processamento de vídeos, pois a transcrição e tradução podem demorar. Isso permite que os vídeos sejam processados de forma assíncrona.

---

## 2. Fluxo de Trabalho do TRADUTUBE

### 2.1 Recebimento do Vídeo
- O **usuário** fornece a **URL do vídeo do YouTube** no frontend.
- O backend valida se o link é válido e se o vídeo possui legendas disponíveis.

### 2.2 Recuperação das Legendas
- Caso o vídeo tenha legendas disponíveis, o sistema usa a **API do YouTube Data** para obter as legendas.
- Se as legendas não estiverem disponíveis, o sistema usa **Whisper** (OpenAI) ou outro serviço de **speech-to-text** para transcrever o áudio do vídeo em tempo real.

### 2.3 Tradução do Texto
- Uma vez que as legendas ou transcrição estão disponíveis, o texto é enviado para **ElevenLabs** para converter as legendas no idioma desejado.

### 2.4 Geração do Áudio
- O texto traduzido é então enviado para o serviço **Text-to-Speech (TTS)**, como **ElevenLabs** ou **Google TTS**, para gerar o áudio com uma voz realista.
- O áudio gerado é armazenado no sistema de arquivos (AWS S3, Google Cloud Storage) e um link para o arquivo é gerado.

### 2.5 Entrega ao Usuário
- O usuário pode então acessar o áudio gerado e ouvir a tradução do vídeo.
- O sistema oferece **streaming direto**.

---

## 3. Diagrama de Componentes

```
  +------------------+        +---------------------+
  |   Frontend       | <----> |    Web API Backend  |
  | (Web/Mobile)     |        | (C# ASP.NET Core)    |
  +------------------+        +----------+----------+
           |                           |
           v                           v
+------------------+       +-----------------------------+
| YouTube API      | <----> |  TTS Microservice           |
| (Para Legendas)  |       |  (ElevenLabs, Google TTS)   |
+------------------+       +-----------------------------+
           |
           v
+--------------------------+     +--------------------+
| Transcrição de Áudio     |     | Tradutor           |
| (Whisper/OpenAI API)     |     | (ElevenLabs)       |
+--------------------------+     +--------------------+
           |
           v
+-------------------------+
|  Sistema de Fila        |
|  (RabbitMQ, Celery)     |
+-------------------------+
           |
           v
 +-----------------------+
 | Banco de Dados        |
 | (PostgreSQL)    |
 +-----------------------+
           |
           v
 +-------------------------------+
 | Armazenamento de Áudio        |
 | (AWS S3/Google Cloud Storage) |
 +-------------------------------+
```

---

## 4. Funcionalidades Propostas

- **Cadastro de Usuário** (com autenticação via Google ou e-mail).
- **Subida de URL do YouTube** (usuário fornece o link do vídeo).
- **Verificação Automática de Legendas**.
- **Transcrição e Tradução**:
  - Caso o vídeo não tenha legendas, o sistema transcreve o áudio e traduz.
- **Processamento Assíncrono**:
  - As transcrições, traduções e conversões de TTS são realizadas em segundo plano usando **Celery** ou **RabbitMQ**.
- **Exibição de Progresso**:
  - O frontend exibe o status de processamento e a previsão de término.
- **Feedback ao Criador**:
  - Enviar notificações para os criadores ou usuários sobre o status de processamento.


## 5. Tecnologias

- **Frontend**: Flutter
- **Backend**: C# com **ASP.NET Core** para a API.
- **Banco de Dados**: PostgreSQL.
- **Armazenamento de Áudio**: AWS S3 ou Google Cloud Storage.
- **APIs de TTS**: ElevenLabs, Google Cloud TTS, Amazon Polly.
- **Transcrição de Áudio**: Whisper (OpenAI), Deepgram, AssemblyAI.
- **APIs de Tradução**: Google Translate, DeepL.

## 6. Considerações Finais

- **Escalabilidade**: Usar filas e microserviços permite escalar o sistema para lidar com grandes volumes de processamento de vídeo.
- **Desempenho**: A transcrição e tradução de vídeos podem consumir muitos recursos, então é fundamental usar sistemas de processamento assíncrono para não bloquear o sistema.
- **Customização**: Os usuários podem escolher a voz do TTS e o idioma de tradução, tornando a plataforma mais flexível.
- **Segurança**: Implementar autenticação segura para usuários (via Google OAuth) e usar HTTPS para todas as comunicações.

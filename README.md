# BOT-auth2-Dc

Bot Discord Backup OAuth2
Bot completo para backup de servidores Discord com autenticação OAuth2 e restauração de membros após incidentes de segurança.

📋 Características
Backup Seletivo: Escolha quais componentes incluir (canais, cargos, membros, emojis, etc.)
Backups Automáticos: Configure backups automáticos com intervalos pré-definidos (1 semana, 2 semanas, 3 semanas, 1 mês)
OAuth2 Integration: Coleta tokens OAuth2 para restaurar membros após raids/mass bans
Restauração Completa: Restaure servidores completos ou componentes específicos
Criptografia: Tokens OAuth2 são armazenados com criptografia AES-256
Interface em Português: Todos os comandos e mensagens em português brasileiro
⚡ Quick Start - Requisitos Críticos
Antes de instalar e usar o bot, certifique-se de atender aos seguintes requisitos:

🔴 CRÍTICO: Posição do Cargo do Bot
O cargo do bot DEVE estar na posição mais alta da hierarquia de cargos do servidor.

Após convidar o bot:

Vá em Configurações do Servidor → Cargos
Arraste o cargo do bot para o topo da lista (acima de todos os outros cargos)
Salve as alterações
Por quê? O bot precisa gerenciar cargos e canais que podem estar posicionados acima de outros cargos. Sem isso, a restauração de cargos/canais falhará.

🔐 Permissões Necessárias
Recomendado: Convide o bot com permissão de Administrator (simplifica a configuração).

Alternativa: Se não quiser dar Administrator, o bot precisa destas permissões:

Manage Guild (gerenciar servidor)
Manage Channels (gerenciar canais)
Manage Roles (gerenciar cargos)
Manage Nicknames (gerenciar apelidos)
Manage Emojis and Stickers (gerenciar emojis e stickers)
View Channel (ver canais)
Read Message History (ler informações dos canais)
Send Messages (enviar mensagens)
Embed Links (incorporar links)
⚙️ Comando de Configuração Inicial
Após o bot estar online, execute o comando de setup:

/setup tipo:automatic   (cria todos os canais na restauração)
ou
/setup tipo:manual      (configura apenas canais existentes + coleta OAuth2)
Para coletar tokens OAuth2 dos membros (necessário para restaurar membros após raids):

Use /setup tipo:manual
Selecione um canal para enviar a embed de autorização
Peça aos membros que cliquem no botão "Autorizar"
📖 Documentação Completa: Consulte docs/02-configuration.md para instruções detalhadas.

🚀 Requisitos
Node.js 20+
MongoDB 4.4+
Bot Discord criado no Discord Developer Portal
⚙️ Configuração
1. Criar Bot no Discord
Acesse Discord Developer Portal
Crie uma nova aplicação
Vá em "Bot" e crie um bot
Copie o token do bot
Em "OAuth2" → "URL Generator", configure:
Scopes: bot, guilds.join, identify
Permissões: Administrator (ou permissões específicas)
Configure o Redirect URI: https//seu-dominio.com/oauth2/callback (ou seu domínio)
2. Instalação
# Clone o repositório
```
git clone <repository-url>
cd discord-bot-backup-oauth2 ```

# Instale as dependências
``` npm install ```

# Configure as variáveis de ambiente
cp env.example .env
# Edite o .env com suas credenciais
3. Variáveis de Ambiente
Edite o arquivo .env:

``` BOT_TOKEN=seu-token-do-bot
CLIENT_ID=seu-client-id
CLIENT_SECRET=seu-client-secret
REDIRECT_URI=https//seu-dominio.com/oauth2/callback
DATABASE=mongodb://user:pass@localhost:27017/backup-bot
PORT=80
ADMIN_IDS=123456789,987654321
LOG_LEVEL=info ```
Nota: ENCRYPTION_KEY é opcional. Se não fornecida, o bot usará o CLIENT_SECRET como base.

🎮 Como Usar
Comandos Disponíveis
Backup
/backup criar [nome] - Criar um novo backup
/backup listar - Listar todos os backups
/backup info <backup_id> - Ver informações de um backup
/backup deletar <backup_id> - Deletar um backup
/backup autobackup - Configurar backups automáticos
Restauração
/restore iniciar <backup_id> [servidor_alvo] - Iniciar restauração
/restore status <restore_id> - Ver status da restauração
Configuração
/setup oauth2 - Gerar embed de autorização OAuth2
Utilidades
/ping - Verificar latência do bot
/help - Lista de comandos
Fluxo de Backup
Execute /backup criar [nome]
Selecione os componentes desejados
O backup será criado e armazenado no MongoDB
Fluxo de OAuth2
Execute /setup oauth2 em um canal
Clique no botão "Autorizar"
Autorize o bot no Discord
Seu token será armazenado com segurança
Backups Automáticos
Execute /backup autobackup
Selecione o intervalo (1 semana, 2 semanas, 3 semanas, 1 mês)
Selecione os componentes
Os backups serão criados automaticamente
🐳 Docker
# Subir containers
docker-compose up -d

# Ver logs
``` docker-compose logs -f ```

# Parar containers
``` docker-compose down ```
📝 Scripts
``` npm run dev      # Modo desenvolvimento
npm start        # Modo produção
npm test         # Executar testes
npm run migrate  # Aplicar migrations
npm run seed     # Popular banco com dados de exemplo ```
🔒 Segurança
Tokens OAuth2 são criptografados usando AES-256
Apenas administradores podem usar comandos de backup/restore
Logs de auditoria de todas as operações
Validação de entrada em todos os comandos
📚 Documentação
Consulte a pasta docs/ para documentação completa:

01-introduction.md - Introdução e visão geral
02-configuration.md - Configuração detalhada
03-running.md - Como usar o bot
04-deployment.md - Deploy em produção

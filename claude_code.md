### Claude Code

Comandos:
* claude -> Abre o claude no terminal
* exit -> Fecha a sessão
* /ide -> Mostra as IDEs conectadas com o claude
* /help -> Ajuda


CLAUDE.md -> Arquivo que o claude vai seguir como instruções para o projeto
* Ele vai seguir, más não é garantido que será todas as vezes
* A propria claude recomenda que se use só 1 arquivo CLAUDE.md afim de evitar alucinações

Forma de trabalhar com o CLAUDE.md
* Global -> ~/.claude/CLAUDE.md -> Uma config que vai valer para todos os projetos
* Projeto -> projeto/CLAUDE.md -> Uma config que é valida por todo o projeto
* Sub-Diretorio do projeto -> projeto/teste1/CLAUDE.md -> Uma config valida a aquele diretorio


Para o claude carregar essas infos, ele deve ser finalizado "/exit" e iniciado "claude" para carregar os .md do DIR



* /init <contexto opcional> -> Gera um informativo sobre o diretorio do projeto -> Ajuda o claude durante o desenvolvimento

O claude por padrão não tem permissões, vc vai dando as permissões para ele confirme o necessário

* /memory  -> Edita a memoria do claude (contexto)
	* project memory -> CLAUDE.md do projeto atual
	* user memory -> Oq vale para todos, independe do projeto

* Outra forma de gravar é:
#Ação que vc quer
* Se usar o # na frente de uma frase na CLI, ele pergunta onde se quer gravar


* /mcp -> Gerenciar os MCPs

* claude mcp -> Abre as opções de ações de mcp do claude
	* list -> Lista as conexões ativadas
* claude mcp remove <nome do mcp> -> Remove o MCP
* claude mcp add <nome do mcp> <comando de acesso ao mcp>

settings.local.json
* Esse é o arquivo de MCP do seu projeto
* Os .local vc não commit, os sem, vc commita para é para uso geral


Escrita e/ou planejamento
* São os modo de execução do claude, para vc alterar, use: shitf + tab durante o CLI
	* plan mode on -> Modo de planejamento
		* Refinamento de uma ideia com a ajuda do claude para após isso aplicar o plano definido
	* accept edits on -> Modo de pensar e fazer


Há uma fila de processamento no CLI, se tentar fazer algo enquanto está executando alguma tarefa, o atual só será executado após o termino da tarefa em processamento, isso vai gerando fila

* /permissions -> Permissões gerais dos arquivos / tarefas que o claude pode operar


### Compactação
* Quando a janela de contexto fica no limite, ele pega toda a conversa atual, converte para informações de longo prazo (Perdendo uma parte dessas infos) e limpando os tokens para mais usos

* /compact -> É basicamente isso, da para forçar as ações

É recomendado que tudo que for mexer tenha uma documentação para o claude sempre começar com o entendimento do projeto, quase como um RAG


### Diretorio .claude dentro do projeto
* .claude/commands
* Vc pode criar arquivos dentro dessa estrutura de diretorio para ele ter comandos personalizados do projetos

### hooks
* Vc cria gatilhos para serem obrigatoriamente executados
* Isso fica gravado no settings.local.json



--------------------------------------------

### oq é o cloud code
* É um agente que trabalha em loop -> Faz / revisa / entrega -> Repete
* É um agente que se entrega com várias ferramentas


---------------------------------------------

### Skills
* Templates de ações para o cloud executar ações repetitivas


---------------------------------------------
### Prompt e contexto
* Prompt -> Forma de requisitar coisas com IA
* Contexto -> Conteudo relacionado ao que se está fazendo

---------------------------------------------
### Alucinação
* Isso ocorre quando se vai perdendo o contexto e/ou quando se vai alterando o contexto demais, Ex: Consumiu todo o contexto e ele acaba limpando as informações mais antigas, se ele perder algo importante, as repostas podem ficar comprometidas, outro exemplo é, começar o prompt pedindo A e terminar em Z, sendo que no meio teve 5, pastel, cobra, carnaval e coisas do tipo, gera uma confusam que torna os modelos transformers inuteis pois não enxegam relação

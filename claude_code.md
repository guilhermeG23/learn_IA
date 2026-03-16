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


O CLAUDE.md é o arquivo padrão, más não necessariamente o obrigatorio, vc poderia criar qualquer arquivo de qualquer extensão para realizar a tarefa de ter um descritivo para sua IA, Ex: modelo.md, vc só precisa subir o agente / LLM e falar para carregar o "modelo.md" e pronto, sua IA entenderia oq o projeto tem que fazer.
P.S: Sempre configure este modelo da melhor forma possível


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

MCP
* É habilitar uma comunicação entre o claude com uma ferramenta, permitindo ele realizar ações diretas nessas ferramentas, Ex:
	* Crie uma VM ubuntu linux? -> Faz o virtualbox subir uma vm desse tipo


settings.local.json
* Esse é o arquivo de MCP do seu projeto
* Os .local vc não commit, os sem, vc commita para é para uso geral

Ex:
{
	"permissions": {
		"allow": [
			"Bash(kubectl get:*)"
		],
		"deny": [
			"Base(kubectl delete *)"
		]
	}
}



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


### Como da para trabalhar com ele?
* Via command line
* Via extensão em IDE
* Via web caso conectar a antropic no seu repositorio

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

----------------------------------------------
### Modelos
* Haiku ->  Modelo mais simples -> Custo baixo/inteligencia baixa
* Sonnet -> Modelo equibilibrado -> Capacidade com custo
* Opus -> Modelo com capacidade de pensamento -> Custo alto, qualidade

Vc consegue trocar de modelo no claude code com o comando:
* /model

----------------------------------------------
### Janela de Contexto
* É toda a "conversa" com a IA que tem limites "fisicos" (tokens), após atingir este limite, os dados mais antigos são limpos ou resumidos, para assim dar mais espaço para as novas entradas

----------------------------------------------
### SubAgentes
* Um agente geral (orquestrador) vai requisitar ações de agente especialistas (subagente), isso é:
	* Vc precisa de um 5/6 agentes especialistas e 1 orquestrador para isso, pode ser que saia mais barato e mais eficaz que somente pegar um modelo de inteligencia geral
	* É uma questão de planejamento e custos

----------------------------------------------
### Skills
* Templates de ações REPETIVEIS e que podem ser reaproveitadas em vários projetos ou várias execuções no mesmo projeto
* Onde as skills são colocadas:
	* .claude/skills/<diretorio da skill>/SKILL.md

--------------------------------------------
### Versão do claude code
claude -v

--------------------------------------------
### Verificar o consumo de contexto do projeto
/context

--------------------------------------------
Se estiver utilizando a versão com o IDE do VSCODE, vc pode ver o consumo de tokens pelas opções "/" -> "Model/Account & Usage..." 
Isso é mais barato que deixar uma aba no navegador só pra isso

---------------------------------------------
Para apontar arquivos de forma mais especifica, use @ no nome ou path do arquivo, Ex:
@index.php

---------------------------------------------
Opção Thinking -> Vc pode ligar / desligar o raciocinio aprofundado de algo caso deseje, isso pode economizar tokens, más pode diminuir a eficiencia da ferramenta

---------------------------------------------
A melhor forma de um IA entender oq queremos é com base em texto, de preferencia com detalhes suficientes sobre oq queremos, Ex:
* Documentos de PRD (Requisitos de projeto)
* Fluxogramas de etapas da ferramenta
* Entre ourtos
São excelentes dados a serem imputados dentro da IA para geração de codigo

---------------------------------------------
### Formas de economizar com a IA
* Usar coisas já prontas que satisfazem a necessidade, Ex: Arquivos de JS, CSS e demais, onde vc só quer que ele construa algo com base naquilo
* Usar configs já disponiveis
* Promtps mais precisos para atender a demanda
* Evitar de gerar TODO o projeto com a IA e somente usar a mesma para atender aos problemas mais custosos
* Caso for trabalhar com só alguns arquivos dentro de um projeto, aponte eles, isso evita do mesmo ter de gastar tokens para procurar, interpretar e demais -> Facilite e aponte oq vc quer usar 


---------------------------------------------
### Comandos
/add-dir -> Adicionar um diretorio para o projeto
/bug -> Reportar bugs para a anthropic
/clear -> limpar toda a conversa anterior e contexto -> Limpeza da sessão caso queria fazer outra ação
/compact -> Faz um resumo do conversado até o momento e gera um contexto (Más limpa faz o historico de conversa e contextos a não ser oq compactado)
/stats -> Mostra o uso da ferramenta
/export -> Exporta a conversa para o ctrl+c / ctrl+v (Copia para a area de memoria) ou em arquivo
/help -> Ajuda
/hooks -> Gatilhos com base em ações para acionar algo no sistema
/install-github-app -> Seta permissões para ações no github via o agente
/login -> Realizar login
/logout -> Finalizar sessão do usuário
/mcp -> Configurar servidores MCP
/memory -> Ações sobre o arquivo CLAUDE.md
/migrate-installer -> Migrar configurações já setadas de forma global a uma nova sessão
/model -> Setar o modelo de LLM da antropic
/permissions -> Permissões gerais sobre comandos, diretorios, onde ele afeta e demais
/pr-comments -> Pega os comentarios de PRs do GitHub
/release-notes -> Mostra o informativo da versão
/resume -> Resume a conversa atual
/review -> Revisão de PR
/status -> Status geral do agente e uso


---------------------------------------------
### MCP
* https://github.com/upstash/context7
Dar uma olhada nesse cara para a geração de contextos mais completos com base em descrições do usuário
* Usuário entra com a descr e chamada ele -> Ele gera um contexto mais completo / complexo -> Manda a IA processar



---------------------------------------------
### Sub-agentes
* Um agente especializado em algo totalmente a parte do agente principal e seu contexto e permite trabalhar de forma paralela
* O code não tem controle sobre a operação do sub, más consegue realizar comunicação em linguagem normal

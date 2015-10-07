# Introdução

 Electron te permite criar aplicações para desktop com JavaScript puro, por rodar em tempo de execução como APIs nativas do sistema operacional. Você pode vê-lo como uma variação do Node.js, pois ele esta focado em apliações de desktop em vez de servidores.

 Isto não significa que Electron está usando JavaScript para fazer a Interface Gráfica do Usuário (GUI, sigla em inglês). O Electron usa páginas da web como seu GUI, então você também pode vê-lo como um mini navegador Chromium controlado por JavaScript.

### Main Process

 No Electron, o processo que executa o `main` script do `package.json` é chamado de __main process__. O script que executa o main process por criar paginas web pode exibir uma GUI.

### Renderer Process

Uma vez que o Electron usa o Chromium para dispara paginas web, a arquitetura de multi-processo do Chromium também é usada. Cada pagina web em Electron é executada em seu proprio processo, que é chamado de __The renderer process__.

Em navegadores normais, paginas web geralmente são executadas em modo seguro e não são permitido o acesso aos recursos nativos, no entanto usuários de Electron podem usar APIs Node.js em paginas web, possibilitando interações de baixo nivel com o sistema operacional.

### Diferença entre Main Process e Renderer Process

O main process cria páginas web, criando instâncias `BrowserWindow`, cada instância do `BrowserWindow` executa a página web no seu proprio renderizador. Quando uma instância `BrowserWindow` é destruído, o renderer process correspondente é também terminada.

O main process adiministra todas as páginas web e seus renderer process correspondentes. Cada renderer process é isolado e só preocupa com a página web  em execução.

Nas paginas web, chamadas nativas do GUI relacionadas a APIs não é perminido porque a administração de recursos da GUI nativas em paginas da web é muito perigoso e vulneravel a vazamento. Se você quer executar operações de GUI em paginas web, o renderer process da pagina web deve se comunicar com o main process para pedir que ele execute essas operações.

No Electron, nos fornecemos o modulo [ipc](../api/ipc-renderer.md) para a comunicação entre o main process e o renderer process. Há também um modulo [remoto](../api/remote.md) para estilo de comunicação RPC.
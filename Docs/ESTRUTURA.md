# Estrutura do projeto

Árvore de pastas e arquivos gerada a partir do repositório de código (privado).
Mostra a organização do projeto sem expor o conteúdo dos arquivos. Diretórios de
build/publicação e arquivos locais são omitidos.

Gerado em 17/11/2026 13:05 por `scripts/gerar-estrutura.ps1`.

```
TradingBot/
├── backend/
│   ├── src/
│   │   ├── TradingBot.Api/
│   │   │   ├── Composicao/
│   │   │   │   ├── ComposicaoAutenticacao.cs
│   │   │   │   ├── ComposicaoEndpoints.cs
│   │   │   │   ├── ComposicaoPersistencia.cs
│   │   │   │   └── ComposicaoRobo.cs
│   │   │   ├── Infrastructure/
│   │   │   │   ├── Binance/
│   │   │   │   │   └── BinanceAPIClient.cs
│   │   │   │   ├── Configuracao/
│   │   │   │   │   ├── ConversorConfiguracao.cs
│   │   │   │   │   ├── CoordenadorMonitores.cs
│   │   │   │   │   ├── GerenciadorConfiguracaoAtiva.cs
│   │   │   │   │   ├── ProvedorClienteBinance.cs
│   │   │   │   │   ├── RespostaAcumulacao.cs
│   │   │   │   │   └── RespostaConfiguracao.cs
│   │   │   │   ├── Estado/
│   │   │   │   │   └── MemoriaDeEstadoMercado.cs
│   │   │   │   ├── MySql/
│   │   │   │   │   ├── Migracoes/
│   │   │   │   │   │   ├── 001_cria_tabelas.sql
│   │   │   │   │   │   ├── 002_criar_configuracao.sql
│   │   │   │   │   │   ├── 003_adiciona_barrado_sinais.sql
│   │   │   │   │   │   ├── 004_adiciona_conta.sql
│   │   │   │   │   │   ├── 005_carteira_por_conta.sql
│   │   │   │   │   │   └── 006_cria_decisoes.sql
│   │   │   │   │   ├── ComandosSql.cs
│   │   │   │   │   ├── FabricaConexaoMySql.cs
│   │   │   │   │   ├── InicializadorBancoMySql.cs
│   │   │   │   │   ├── RepositorioCarteiraMySql.cs
│   │   │   │   │   ├── RepositorioConfiguracaoMySql.cs
│   │   │   │   │   ├── RepositorioDecisoesMySql.cs
│   │   │   │   │   ├── RepositorioOperacoesMySql.cs
│   │   │   │   │   ├── RepositorioOrdensMySql.cs
│   │   │   │   │   ├── RepositorioSinaisMySql.cs
│   │   │   │   │   └── ServicoLimpezaDecisoes.cs
│   │   │   │   ├── Notificacao/
│   │   │   │   │   └── NotificadorConsole.cs
│   │   │   │   ├── Seguranca/
│   │   │   │   │   └── UsuarioAtual.cs
│   │   │   │   └── Serializacao/
│   │   │   │       └── ConversorDataUtc.cs
│   │   │   ├── Presentation/
│   │   │   │   ├── Console/
│   │   │   │   │   └── VisaoConsole.cs
│   │   │   │   └── RespostaSeries.cs
│   │   │   ├── Properties/
│   │   │   │   └── launchSettings.json
│   │   │   ├── appsettings- exemplo.json
│   │   │   ├── Program.cs
│   │   │   └── TradingBot.Api.csproj
│   │   └── TradingBot.Core/
│   │       ├── Config/
│   │       │   ├── ConfigAcumulacao.cs
│   │       │   ├── ConfigConta.cs
│   │       │   ├── ConfigCripto.cs
│   │       │   ├── ConfigEstrategia.cs
│   │       │   ├── ConfigMacd.cs
│   │       │   ├── ConfigRsi.cs
│   │       │   ├── ConfigSerie.cs
│   │       │   ├── ConfigSimulacao.cs
│   │       │   ├── ConfigTendencia.cs
│   │       │   ├── ConfiguracaoRobo.cs
│   │       │   ├── ConfiguracaoRoboSanitizador.cs
│   │       │   ├── ValidadorConfiguracao.cs
│   │       │   └── ValidadorLimites.cs
│   │       ├── Data/
│   │       │   ├── CarteiraSimulada.cs
│   │       │   ├── ContextoDecisao.cs
│   │       │   ├── DadosMercado.cs
│   │       │   ├── DesempenhoPorSerie.cs
│   │       │   ├── EstadoMoeda.cs
│   │       │   ├── KlinesData.cs
│   │       │   ├── LadoDecisao.cs
│   │       │   ├── LadoOrdem.cs
│   │       │   ├── ModoExecucao.cs
│   │       │   ├── Order.cs
│   │       │   ├── PontoMacd.cs
│   │       │   ├── PontoRsi.cs
│   │       │   ├── PosicaoPresumida.cs
│   │       │   ├── RegistroDecisao.cs
│   │       │   ├── RegistroSinal.cs
│   │       │   ├── RegraAvaliada.cs
│   │       │   ├── RelatorioDesempenho.cs
│   │       │   ├── ResultadoDecisao.cs
│   │       │   ├── ResultadoExecucao.cs
│   │       │   ├── ResultadoMacd.cs
│   │       │   ├── ResultadoRegra.cs
│   │       │   ├── ResultadoRsi.cs
│   │       │   ├── ResumoDesempenho.cs
│   │       │   ├── StatusOrdem.cs
│   │       │   ├── TipoMedia.cs
│   │       │   ├── TipoOrdem.cs
│   │       │   └── Vela.cs
│   │       ├── Decisao/
│   │       │   ├── Regras/
│   │       │   │   ├── RegraCompraArmada.cs
│   │       │   │   ├── RegraMacdHistogramaCaindo.cs
│   │       │   │   ├── RegraMacdHistogramaSubindo.cs
│   │       │   │   ├── RegraRsiAbaixoDoTopo.cs
│   │       │   │   ├── RegraRsiAcimaDoFundo.cs
│   │       │   │   └── RegraVendaArmada.cs
│   │       │   ├── AvaliadorDecisao.cs
│   │       │   └── FabricaAvaliadorDecisao.cs
│   │       ├── Indicators/
│   │       │   ├── CalculadoraSeries.cs
│   │       │   ├── EstrategiaMacd.cs
│   │       │   ├── EstrategiaMedia.cs
│   │       │   ├── EstrategiaRsi.cs
│   │       │   └── EstrategiaTendencia.cs
│   │       ├── Market/
│   │       │   ├── DetectorUrlMarketData.cs
│   │       │   ├── LimitadorTaxaBinance.cs
│   │       │   └── ServicoDadosMercado.cs
│   │       ├── Monitoring/
│   │       │   ├── AssinaturaDecisao.cs
│   │       │   ├── PlanejadorMonitores.cs
│   │       │   ├── ServicoMonitoramento.cs
│   │       │   └── ServicoPreco.cs
│   │       ├── Operacoes/
│   │       │   ├── CalculadoraTaxa.cs
│   │       │   ├── ExecutorOrdensSimulado.cs
│   │       │   └── MotorOperacoes.cs
│   │       ├── Ports/
│   │       │   ├── IBinanceAPIClient.cs
│   │       │   ├── IEstadoMercado.cs
│   │       │   ├── IEstrategiaMacd.cs
│   │       │   ├── IEstrategiaMedia.cs
│   │       │   ├── IEstrategiaRsi.cs
│   │       │   ├── IEstrategiaTendencia.cs
│   │       │   ├── IExecutorOrdens.cs
│   │       │   ├── IFornecedorConfiguracao.cs
│   │       │   ├── IMotorOperacoes.cs
│   │       │   ├── INotificador.cs
│   │       │   ├── IProvedorClienteBinance.cs
│   │       │   ├── IRegraDecisao.cs
│   │       │   ├── IRepositorioCarteira.cs
│   │       │   ├── IRepositorioConfiguracao.cs
│   │       │   ├── IRepositorioDecisoes.cs
│   │       │   ├── IRepositorioOperacoes.cs
│   │       │   ├── IRepositorioOrdens.cs
│   │       │   ├── IRepositorioSinais.cs
│   │       │   ├── IServicoDadosMercado.cs
│   │       │   └── IVisao.cs
│   │       ├── Relatorios/
│   │       │   ├── CalculadoraDesempenho.cs
│   │       │   └── CalculadoraLucroPresumido.cs
│   │       └── TradingBot.Core.csproj
│   ├── tests/
│   │   └── TradingBot.Tests/
│   │       ├── Fakes/
│   │       │   ├── BinanceAPIClientFake.cs
│   │       │   ├── ExecutorFake.cs
│   │       │   ├── FornecedorConfiguracaoFake.cs
│   │       │   ├── ProvedorClienteBinanceFake.cs
│   │       │   ├── RepositorioCarteiraFake.cs
│   │       │   └── RepositorioOperacoesFake.cs
│   │       ├── AssinaturaDecisaoTests.cs
│   │       ├── AvaliadorDecisaoTests.cs
│   │       ├── CalculadoraDesempenhoTests.cs
│   │       ├── CalculadoraLucroPresumidoTests.cs
│   │       ├── CalculadoraSeriesTests.cs
│   │       ├── CalculadoraTaxaTests.cs
│   │       ├── ConfiguracaoRoboTests.cs
│   │       ├── DetectorUrlMarketDataTests.cs
│   │       ├── EstrategiaMacdTests.cs
│   │       ├── EstrategiaMediaTests.cs
│   │       ├── EstrategiaRsiTests.cs
│   │       ├── EstrategiaTendenciaTests.cs
│   │       ├── KlinesDataTests.cs
│   │       ├── LimitadorTaxaBinanceTests.cs
│   │       ├── MotorOperacoesTests.cs
│   │       ├── ServicoDadosMercadoTests.cs
│   │       ├── TradingBot.Tests.csproj
│   │       └── ValidadorLimitesTests.cs
│   └── TradingBot.sln
├── docs/
│   ├── diagramas/
│   │   ├── multiusuario/
│   │   │   ├── autenticacao.drawio
│   │   │   ├── autenticacao.md
│   │   │   ├── componentes.drawio
│   │   │   ├── componentes.md
│   │   │   ├── fluxo-decisao.drawio
│   │   │   ├── fluxo-decisao.md
│   │   │   ├── nucleo-decisao.drawio
│   │   │   ├── nucleo-decisao.md
│   │   │   ├── README.md
│   │   │   ├── usuario-configuracao.drawio
│   │   │   └── usuario-configuracao.md
│   │   ├── componentes.drawio
│   │   ├── componentes.md
│   │   ├── compra.drawio
│   │   ├── decisao-regras.drawio
│   │   ├── decisao-regras.md
│   │   ├── dominio.drawio
│   │   ├── dominio.md
│   │   ├── maquina-estados.drawio
│   │   ├── maquina-estados.md
│   │   ├── ports.drawio
│   │   ├── ports.md
│   │   ├── README.md
│   │   └── venda.drawio
│   ├── ARCHITECTURE.md
│   ├── CONFIG.md
│   ├── DEPLOY.md
│   ├── MAPA-CODIGO.html
│   ├── MAPA-CODIGO.md
│   ├── PLANO_FILTRO_TENDENCIA.md
│   ├── PLANO_MULTIUSUARIO.md
│   ├── PLANO_OPERACOES.md
│   ├── PLANO_REFATORACAO.md
│   └── RUNNING.md
├── frontend/
│   ├── public/
│   │   ├── favicon.svg
│   │   └── silent-check-sso.html
│   ├── src/
│   │   ├── components/
│   │   │   ├── AutenticacaoMenu.tsx
│   │   │   ├── CardMoeda.tsx
│   │   │   ├── GraficoMoeda.tsx
│   │   │   ├── ListaOrdens.tsx
│   │   │   ├── ListaSinais.tsx
│   │   │   ├── MenuLateral.tsx
│   │   │   ├── NavegadorDecisoes.tsx
│   │   │   ├── PaginaConfiguracao.tsx
│   │   │   ├── PaginaDecisoes.tsx
│   │   │   ├── PaginaLogin.tsx
│   │   │   ├── PainelGanhos.tsx
│   │   │   ├── PainelOperacoes.tsx
│   │   │   └── Sparkline.tsx
│   │   ├── hooks/
│   │   │   ├── useEstadoMercado.ts
│   │   │   └── useSessao.ts
│   │   ├── services/
│   │   │   ├── apiEstado.ts
│   │   │   └── autenticacao.ts
│   │   ├── types/
│   │   │   ├── estado.ts
│   │   │   └── tradingview.ts
│   │   ├── utils/
│   │   │   ├── formatar.ts
│   │   │   └── tradingview.ts
│   │   ├── App.tsx
│   │   ├── index.css
│   │   ├── main.tsx
│   │   └── vite-env.d.ts
│   ├── .gitignore
│   ├── .oxlintrc.json
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   ├── README.md
│   ├── tsconfig.app.json
│   ├── tsconfig.json
│   ├── tsconfig.node.json
│   └── vite.config.ts
├── tools/
│   ├── backtest/
│   │   ├── lib/
│   │   │   ├── dados.mjs
│   │   │   ├── indicadores.mjs
│   │   │   ├── indicadores-robo.mjs
│   │   │   └── simulacao.mjs
│   │   ├── 4h-capital.mjs
│   │   ├── acumulacao-1d.mjs
│   │   ├── analise-sem-tendencia.mjs
│   │   ├── backtest.mjs
│   │   ├── btc-stack.mjs
│   │   ├── composto.mjs
│   │   ├── cross-sectional.mjs
│   │   ├── ema-sweep.mjs
│   │   ├── estrategias.mjs
│   │   ├── holdout-moeda.mjs
│   │   ├── ml.mjs
│   │   ├── README.md
│   │   ├── robo-5m-1ano.mjs
│   │   ├── robo-real.mjs
│   │   ├── sweep-velas.mjs
│   │   ├── trend-ma-vs-ema.mjs
│   │   ├── validar-candidatos.mjs
│   │   ├── walkforward.mjs
│   │   ├── walkforward-composto.mjs
│   │   └── walkforward-real.mjs
│   └── doc/
│       ├── gerar-mapa.mjs
│       └── README.md
├── .gitignore
├── AGENTS.md
├── gerar-mapa.bat
├── iniciar-dev.bat
├── publicar.bat
├── publicar.ps1
├── README.md
└── STATUS.md
```

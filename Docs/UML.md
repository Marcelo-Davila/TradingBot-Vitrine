# UML

Diagramas do TradingBot (Mermaid): componentes, contratos, classes do domínio e
a máquina de estados da posição. Mostram a estrutura, sem detalhar os
parâmetros de estratégia.

## Componentes (Ports & Adapters)

```mermaid
flowchart TB
    subgraph Core[TradingBot.Core — domínio]
        MON[ServicoMonitoramento]
        PRE[ServicoPreco]
        AVAL[AvaliadorDecisao]
        MOTOR[MotorOperacoes]
        DADOS[Serviço de dados de mercado]
        PORT[Ports]
        MON --> PORT
        PRE --> PORT
        MOTOR --> PORT
        MON --> DADOS
        PRE --> DADOS
        AVAL -.lê.-> MON
    end
    subgraph Api[TradingBot.Api — host]
        BIN[BinanceAPIClient]
        NOT[NotificadorConsole]
        MEM[MemoriaDeEstadoMercado]
        REP[Repositórios MySQL]
        EXE[ExecutorOrdensSimulado]
        AUTH[Autenticação OIDC e autorização]
        API[API REST]
        COORD[CoordenadorMonitores]
    end
    IDP[Provedor de identidade OIDC]
    EXCHANGE[Binance]
    DADOS --> BIN
    BIN --> EXCHANGE
    BIN -.IBinanceAPIClient.-> PORT
    NOT -.INotificador.-> PORT
    MEM -.IEstadoMercado.-> PORT
    REP -.IRepositorio*.-> PORT
    EXE -.IExecutorOrdens.-> PORT
    IDP --> AUTH
    DASH[Dashboard React] -->|sessão autenticada| API
    API --> AUTH
    COORD --> MON
    API --> MEM
    API --> REP
```

O backend valida a identidade delegada e limita cada consulta/configuração ao
usuário autenticado. O provedor externo mantém as credenciais de acesso; o
TradingBot não armazena senhas.

## Ports (contratos do domínio)

```mermaid
classDiagram
    class IBinanceAPIClient
    class IVisao
    class INotificador
    class IEstadoMercado
    class IRepositorioSinais
    class IRepositorioOrdens
    class IRepositorioCarteira
    class IRepositorioOperacoes
    class IRepositorioDecisoes
    class IRepositorioConfiguracao
    class IExecutorOrdens
    class IMotorOperacoes
    class IEstrategiaRsi
    class IEstrategiaMacd
    class IEstrategiaTendencia
    class IEstrategiaMedia
    class IRegraDecisao
    class IFornecedorConfiguracao
    class IServicoDadosMercado
```

## Domínio

```mermaid
classDiagram
    class CoordenadorMonitores {
        +reconciliar()
    }
    class ServicoMonitoramento {
        -posicao
        -compraArmada
        -vendaArmada
        +ExecutarAsync()
    }
    class ServicoPreco {
        +AtualizarAsync()
    }
    class ServicoDadosMercado {
        +ObterCandlesAsync()
        +ObterPrecoAsync()
    }
    class EstrategiaRsi {
        +Calcular()
    }
    class EstrategiaMacd {
        +Calcular()
    }
    class EstrategiaTendencia {
        +Calcular()
    }
    class EstrategiaMedia {
        +Calcular()
    }
    class FabricaAvaliadorDecisao {
        +Criar(config)
    }
    class AvaliadorDecisao {
        +Avaliar(contexto)
    }
    class IRegraDecisao {
        <<interface>>
        +Avaliar(contexto)
    }
    class RegraCompraArmada
    class RegraRsiAcimaDoFundo
    class RegraMacdHistogramaSubindo
    class RegraVendaArmada
    class RegraRsiAbaixoDoTopo
    class RegraMacdHistogramaCaindo
    class MotorOperacoes {
        +ProcessarSinalAsync()
    }
    class ExecutorOrdensSimulado {
        +ExecutarAsync()
    }
    class CalculadoraTaxa
    class CalculadoraDesempenho {
        +Calcular()
    }
    class GerenciadorConfiguracaoAtiva {
        +ConfiguracaoAtual
    }
    class ValidadorConfiguracao {
        +Validar()
    }
    class ConfiguracaoRoboSanitizador {
        +Sanitizar()
    }

    CoordenadorMonitores --> ServicoMonitoramento : cria/para
    CoordenadorMonitores --> GerenciadorConfiguracaoAtiva : lê
    ServicoMonitoramento --> EstrategiaRsi
    ServicoMonitoramento --> ServicoDadosMercado : consulta compartilhada
    ServicoDadosMercado --> IBinanceAPIClient : controla chamadas externas
    ServicoMonitoramento --> EstrategiaMacd
    ServicoMonitoramento --> EstrategiaTendencia
    ServicoMonitoramento --> EstrategiaMedia
    ServicoMonitoramento --> FabricaAvaliadorDecisao
    FabricaAvaliadorDecisao --> AvaliadorDecisao : monta
    AvaliadorDecisao --> IRegraDecisao : avalia
    IRegraDecisao <|.. RegraCompraArmada
    IRegraDecisao <|.. RegraRsiAcimaDoFundo
    IRegraDecisao <|.. RegraMacdHistogramaSubindo
    IRegraDecisao <|.. RegraVendaArmada
    IRegraDecisao <|.. RegraRsiAbaixoDoTopo
    IRegraDecisao <|.. RegraMacdHistogramaCaindo
    ServicoMonitoramento --> MotorOperacoes : sinal
    MotorOperacoes --> ExecutorOrdensSimulado
    MotorOperacoes --> CalculadoraTaxa
    GerenciadorConfiguracaoAtiva --> ValidadorConfiguracao
    GerenciadorConfiguracaoAtiva --> ConfiguracaoRoboSanitizador
```

## Máquina de estados da posição

```mermaid
stateDiagram-v2
    [*] --> Parado
    Parado --> Long: COMPRAR
    Parado --> Short: VENDER (somente com short habilitado)
    Long --> Parado: VENDER (long-only: apenas zera)
    Long --> Short: VENDER (com short: inverte)
    Short --> Long: COMPRAR (com short: inverte)
    Short --> Parado: COMPRAR (long-only)
    note right of Parado
        VENDER quando já está parado é ignorado
        no modo long-only
    end note
```

## Decisão por regras

```mermaid
flowchart LR
    CTX[ContextoDecisao<br/>RSI, MACD, preço, tendência, posição]
    CTX --> RC[Regras de compra]
    CTX --> RV[Regras de venda]
    RC --> AV{AvaliadorDecisao}
    RV --> AV
    AV -->|todas atendidas| C[COMPRAR]
    AV -->|todas atendidas| V[VENDER]
    AV -->|caso contrário| M[MANTER<br/>com a 1ª pendência]
    C --> J[Justificativa]
    V --> J
```

## Acesso autenticado

```mermaid
sequenceDiagram
    participant U as Usuário
    participant F as Dashboard
    participant I as Provedor OIDC
    participant A as API
    participant D as Dados

    U->>F: inicia sessão
    F->>I: autenticação delegada
    I-->>F: token
    F->>A: requisição autenticada
    A->>I: valida token
    I-->>A: identidade confirmada
    A->>D: consulta no escopo do usuário
    D-->>F: resposta autorizada
```

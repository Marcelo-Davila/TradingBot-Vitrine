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
        PORT[Ports]
        MON --> PORT
        PRE --> PORT
        MOTOR --> PORT
        AVAL -.lê.-> MON
    end
    subgraph Api[TradingBot.Api — host]
        BIN[BinanceAPIClient]
        NOT[NotificadorConsole]
        MEM[MemoriaDeEstadoMercado]
        REP[Repositórios MySQL]
        EXE[ExecutorOrdensSimulado]
        API[API REST]
        COORD[CoordenadorMonitores]
    end
    BIN -.IBinanceAPIClient.-> PORT
    NOT -.INotificador.-> PORT
    MEM -.IEstadoMercado.-> PORT
    REP -.IRepositorio*.-> PORT
    EXE -.IExecutorOrdens.-> PORT
    COORD --> MON
    API --> MEM
    API --> REP
    DASH[Dashboard React] --> API
```

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

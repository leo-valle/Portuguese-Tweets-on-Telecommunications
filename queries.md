# Search Terms and Queries Used for Data Collection

This document presents the terms, expressions, and identifiers used to construct queries for collecting posts from the X (Twitter) platform. The terms are organized into groups to facilitate query identification and the maintenance of data collection strategies.

## 1. General Terms Related to Failures

General expressions used to identify posts reporting problems with connectivity, signal, calls, or the unavailability of telecommunications services.

```python
TERMOS_FALHA = [
    "internet caiu",
    "sem internet",
    "internet morta",
    "internet caindo",
    "internet lenta",
    "4g morto",
    "5g bugado",
    "4g sumiu",
    "sem dados móveis",
    "não carrega nada",
    "sem sinal",
    "sem rede",
    "fora do ar",
    "caiu geral",
    "parou tudo",
    "sem serviço",
    "nada funciona",
    "sumiu o sinal",
    "apagou tudo",
    "zero sinal",
    "off total",
    "não pega sinal",
    "celular não pega",
    "não tem sinal",
    "ficou sem internet",
    "internet não voltou",
    "sinal fica caindo",
    "não completa ligação",
    "não completa chamada",
    "ligo e fica mudo",
    "ligo e não chama",
    "chamada caindo",
    "chamada fica caindo",
    "ligação caindo",
    "ligação fica caindo",
    "conexão fica caindo",
    "velocidade baixa",
    "velocidade lenta",
    "não carrega página",
    "telefone não funciona"
]
```

## 2. Telecommunications Operators and Identifiers

The following telecommunications operators were considered, including spelling variations, commercial names, and identifiers used on the X platform.

```python
OPERADORAS = {
    "Oi": [
        "Oi",
        "oi",
        "OI",
        "@oi_oficial",
        "@DigaOi"
    ],

    "NIO": [
        "NIO",
        "nio",
        "Nio",
        "@NioInternet"
    ],

    "Brisanet": [
        "Brisanet",
        "brisanet",
        "BRISANET",
        "@brisanettelecom",
        "@brisanet_ofc"
    ],

    "Algar": [
        "Algar",
        "algar",
        "ALGAR",
        "@AlgarTelecom"
    ],

    "GIGA": [
        "Giga Mais",
        "GiGA",
        "Giga+",
        "@gigamaisfibra"
    ],

    "LIGGA": [
        "Ligga",
        "Ligga Telecom",
        "Copel Telecom",
        "@liggatelecom",
        "@ligga_vc",
        "@copeltelecom"
    ],

    "UNIFIQUE": [
        "Unifique",
        "unifique",
        "UNIFIQUE",
        "@unifique"
    ],

    "PROXXIMA": [
        "Proxxima",
        "@proxxima"
    ],

    "VIASAT": [
        "Viasat",
        "viasat",
        "VIASAT",
        "@Viasat_Brasil"
    ],

    "AGE": [
        "Age Telecom",
        "operadora Age",
        "operadora age",
        "@AgeTelecom"
    ]
}
```

## 3. Category-Specific Terms

### 3.1. Connectivity

Terms related to the unavailability, instability, or interruption of Internet connections and mobile data services.

```python
TERMOS_CONECTIVIDADE = [
    "sem internet",
    "internet caiu",
    "internet morta",
    "internet caindo",
    "internet lenta",
    "sem dados móveis",
    "dados não funcionam",
    "dados móveis caíram",
    "não carrega nada",
    "não carrega página",
    "página não abre",
    "internet não voltou",
    "internet instável",
    "conexão fica caindo"
]
```

### 3.2. Signal

Expressions related to the absence, loss, or instability of mobile network signals.

```python
TERMOS_SINAL = [
    "sem sinal",
    "sem rede",
    "zero sinal",
    "sinal fraco",
    "sumiu o sinal",
    "sinal caiu",
    "sinal sumiu",
    "perdeu sinal",
    "sinal fica caindo",
    "sinal instável",
    "oscilando sinal",
    "não pega sinal",
    "celular não pega",
    "não tem sinal"
]
```

### 3.3. Access Technology

Terms specifically associated with mobile access technologies, such as 3G, 4G, and 5G.

```python
TERMOS_TECNOLOGIA = [
    "4g morto",
    "4g caiu",
    "4g sumiu",
    "4g não funciona",
    "4g lento",
    "5g bugado",
    "5g caiu",
    "5g não funciona",
    "5g instável",
    "3g lento",
    "3g não funciona",
    "voltou pro 3g"
]
```

### 3.4. Connection Speed

Expressions used to identify reports related to low connection speeds or slow Internet performance.

```python
TERMOS_VELOCIDADE = [
    "velocidade baixa",
    "velocidade lenta",
    "conexão lenta",
    "lentidão absurda",
    "muito lento",
    "banda baixa",
    "velocidade horrível"
]
```

### 3.5. Calls

Terms related to making and maintaining telephone calls.

```python
TERMOS_CHAMADAS = [
    "não completa ligação",
    "não completa chamada",
    "chamada caindo",
    "chamada fica caindo",
    "ligação caindo",
    "ligação fica caindo",
    "ligo e fica mudo",
    "ligo e não chama",
    "ligação muda",
    "chamada cai",
    "ligação não entra",
    "não consigo ligar"
]
```

### 3.6. Service Unavailability

Expressions indicating broader service interruptions or network outages affecting telecommunications operators.

```python
TERMOS_SERVICOS = [
    "fora do ar",
    "caiu geral",
    "parou tudo",
    "apagão",
    "nada funciona",
    "sem serviço",
    "tudo parado",
    "operadora caiu",
    "rede caiu",
    "tudo fora"
]
```

### 3.7. Applications and Services

Terms related to the functioning of applications that depend on connectivity, particularly messaging services and video calls.

```python
TERMOS_APPS_SERVICOS = [
    "whatsapp não funciona",
    "whats caiu",
    "whatsapp lento",
    "não envia mensagem",
    "mensagem não sai",
    "não faz chamada de vídeo",
    "videochamada não funciona"
]
```

## 4. Query Organization

The queries were structured by combining terms related to failures with the names and identifiers of the telecommunications operators considered in the data collection process.

Organizing the terms into categories makes it possible to identify different types of problems affecting telecommunications services, while the general terms broaden the coverage of the queries.

**Note:** Some expressions appear in more than one group because they can be used both in general queries and in queries targeting specific categories. Spelling variations and capitalization have also been preserved according to the original configuration.

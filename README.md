## 📊 Request Flow Diagram

```mermaid
flowchart LR
    A[Client Request] --> B[BaseRoute: route matching]
    B --> C[JwtSecurity: token validation]
    C --> D[Service Layer: HttpClient / EdgeService]
    D --> E[SqlBaseMethod: DB query]
    E --> DB[[SQLite DB]]
    D --> F[FormulaFlatterUtility: flatten formulas]
    F --> G[ArithmeticUtility: evaluate expressions]
    E --> H[ResponseMessage: build response]
    G --> H --> I[Client Response]

    C --> J[Logger: logging]
    E --> J
    F --> J
    G --> J
    D --> J

## 🧩 Application Architecture Diagram

The following diagram represents the layered architecture of the application, including configuration, utilities, HTTP APIs, security, database access, and response handling:

```mermaid
graph LR

subgraph Config_Layer
    ConfigurationHelper
    Constnts
end

subgraph Utility_Layer
    ArithmeticUtility
    FormulaFlatterUtility
    Validators
    TimeConversionUtil
end

subgraph API_HTTP
    BaseRoute
    HttpClient
end

subgraph Security_Layer
    JwtSecurity
end

subgraph JSON_Parsing
    JsonParser
end

subgraph Logging
    Logger
    FileUtils
    ErrorCodes
end

subgraph DB_Layer
    SqlBaseMethod
    TableInitializer
end

subgraph Response_Exception
    ResponseMessage
    NoDaraFoundFromEsException
end

BaseRoute --> JwtSecurity
BaseRoute --> HttpClient
HttpClient --> ConfigurationHelper
HttpClient --> Logger
HttpClient --> ResponseMessage
JwtSecurity --> JsonParser
ArithmeticUtility --> Constnts
FormulaFlatterUtility --> Constnts
SqlBaseMethod --> Logger
SqlBaseMethod --> ConfigurationHelper
TableInitializer --> SqlBaseMethod
FileUtils --> Logger

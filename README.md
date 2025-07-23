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

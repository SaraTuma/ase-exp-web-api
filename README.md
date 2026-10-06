# Banking Experience API - Web / Internet Banking (SOAP)

API da camada **Experience** (canal web/internet banking) do projeto de Mobile & Internet Banking do Standard Bank Angola, desenvolvida em **MuleSoft** com protocolo **SOAP**.

Denominada **ASE**.


Esta API expõe as funcionalidades do portal de internet banking, reaproveitando as operações base do canal mobile e acrescentando funcionalidades próprias de web.

```
[Portal Web] → [Experience Web API] → [Process API] → [System API] → [PostgreSQL]
                       ▲
                  (este projeto)
```

## Operações disponíveis

### Reaproveitadas do canal mobile

| Operação | Descrição |
|---|---|
| `viewDashboard` | Ecrã inicial: contas, saldos e últimos movimentos |
| `makeTransfer` | Realiza uma transferência imediata |
| `viewStatement` | Extrato da conta, categorizado |
| `viewSpendingInsights` | Insights de gastos |
| `blockOrUnblockCard` | Bloqueia/desbloqueia um cartão |

### Exclusivas do canal web

| Operação | Descrição |
|---|---|
| `scheduleTransfer` | Agenda uma transferência única ou recorrente |
| `exportStatement` | Exporta o extrato em PDF ou CSV |
| `addBeneficiary` | Regista um beneficiário favorito |
| `listBeneficiaries` | Lista os beneficiários do cliente |
| `removeBeneficiary` | Remove um beneficiário |

## Tecnologias

- MuleSoft (Mule Runtime 4.x)
- APIkit for SOAP (`mule-soapkit-module`)
- Web Service Consumer (consumo do Process API)
- Object Store (persistência de agendamentos e beneficiários)
- Anypoint Studio

## Pré-requisitos

- Anypoint Studio instalado
- Process API publicada no Exchange (ou em execução localmente)
- Conta Anypoint Platform (mesma organização do projeto)

## Como executar localmente

1. Clone este repositório.
2. Abra o projeto no Anypoint Studio.
3. Confirme que o `Web Service Consumer` aponta para o endereço correto da Process API.
4. Clique com o botão direito no projeto → `Run As > Mule Application`.
5. O WSDL fica disponível em:
   ```
   http://localhost:8082/InternetBankingExperienceAPI/BankingExperiencePort?wsdl
   ```
   > Nota: porta `8082` (diferente da mobile, `8081`), para permitir rodar as duas Experience APIs ao mesmo tempo em ambiente local.

## Testando

Recomenda-se o uso do **SoapUI**: `File > New SOAP Project`, colando a URL do WSDL (com `?wsdl`) em "Initial WSDL" - todas as operações são importadas automaticamente com requests de exemplo.

## Estrutura do projeto

```
src/main/
├── mule/                     # Flows do APIkit for SOAP (api-main + sub-flows)
├── resources/
│   ├── wsdl/
│   │   └── banking-experience-web-api.wsdl
│   ├── Schemas/
│   │   ├── common-types.xsd           # tipos compartilhados com o mobile
│   │   └── web/
│   │       └── web-experience-types.xsd
│   └── config-*.yaml
```

## Equipa

Projeto académico/prático - equipa de 3 pessoas, Anypoint Platform (mesma organização).
Responsável por esta API: **Sara Tuma**

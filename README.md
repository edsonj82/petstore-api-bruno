# PetStore API Automation - Bruno Framework 🚀

Este repositório contém a suite de automação de testes de API para a **Swagger PetStore**, desenvolvida utilizando o **Bruno API** (plataforma opensource, local-first para desenvolvimento e testes de APIs). 

O projeto foi estruturado seguindo as melhores práticas de Engenharia de Qualidade, isolando cenários de sucesso de validações estritas de exceções de contrato (tipagem, obrigatoriedade e limites).

---

## 🛠️ Tecnologias e Ferramentas

* **Bruno API Client**: Execução de requisições e gerenciamento de coleções (`.bru`).
* **Bru CLI**: Execução automatizada via linha de comando (ideal para pipelines CI/CD).
* **AJV (Another JSON Schema Validator)**: Validação estrita de contratos de dados em JavaScript.
* **JavaScript (ES6+)**: Scripts de pré-requisito e asserções funcionais.

---

## 📂 Estrutura do Projeto e Cenários de Testes

A arquitetura das coleções foi modularizada por domínios de negócio e dividida sob a ótica de desvios de contrato de dados:

```bash
📂 PETSTORE API
├── 📂 environments            # Variáveis de ambiente (Local, Dev, Prod)
├── 📂 PET                     # Gerenciamento do ciclo de vida dos pets
│   ├── 📂 contract-success    # Fluxos felizes (200 OK, 201 Created) e Schemas válidos
│   └── 📂 contract-exceptions # Inputs inválidos, IDs vazios, Status incorretos
└── 📂 STORE                   # Gerenciamento de pedidos e inventário
    ├── 📂 contract-success    # Compras efetuadas com sucesso e Schemas íntegros
    └── 📂 contract-exceptions # Quantidades inválidas, datas corrompidas, IDs nulos
```

## 🧪 Cobertura de Cenários Detalhada
### 🐶 Domínio: PET
* **contract-success:** Criação de Pet, Atualização (via PUT e Form Data), Busca por ID, Filtro por Status/Tags e Deleção limpa.

* **contract-exceptions:** Validações de payload com ID empty, ID invalid, Status empty e comportamento do servidor ao buscar IDs já deletados.

### 🛒 Domínio: STORE
* **contract-success:** Criação de pedidos, Busca de pedidos por ID, Consulta dinâmica de inventário por status e deleção de ordens de compra.

* **contract-exceptions:** Validações de payloads corrompidos incluindo Quantity Invalid, ShipDate Invalid, StoreId Invalid e Complete Invalid.

## 🚀 Como Executar os Testes
* **Pré-requisitos:** 
1. Certifique-se de ter o Node.js instalado na sua máquina e o CLI global do Bruno:
```bash
npm install -g @usebruno/cli
```

2. Clonando o Repositório:
```bash
git clone [https://github.com/seu-usuario/petstore-bruno-automation.git](https://github.com/seu-usuario/petstore-bruno-automation.git)
cd petstore-bruno-automation
```

3. Executando a Suite de Testes via CLI
Para rodar todos os testes integrados mapeados na pasta raiz apontando para o ambiente configurado:
```bash
bru run --env <nome-do-seu-ambiente>
```

4. Para rodar de forma isolada apenas a pasta de exceções de contrato do domínio Pet:
```bash
bru run PET/contract-exceptions --env <nome-do-seu-ambiente>
```

## 📊 Relatórios e Asserções Técnicas
Cada arquivo de teste executa asserções organizadas em 4 pilares cruciais:

* **Verificação de Infraestrutura:** Tempo de resposta do servidor inferior a 1500ms e presença correta do header Cache-Control.

* **Código de Status HTTP:** Respostas semânticas (200 OK para fluxos felizes, 400 Bad Request ou 404 Not Found para cenários controlados de exceção).

* **Validação de Tipo do Content-Type:** Garantia de tratamento do formato (application/json ou text/plain quando aplicável).

* **Contrato Estrito:** Compilação via biblioteca AJV garantindo que propriedades novas ou ausentes quebrem o teste em caso de alteração no backend (additionalProperties: false).

Se precisar ajustar os comandos de execução de acordo com o nome exato do arquivo `.env` salvo na sua pasta `environments`, basta alterar a flag `--env`.

Este projeto reflete a aplicação de padrões avançados de QA Engineering, focado na criação de pipelines de CI/CD rápidos e resilientes.

---
## 👨‍💻 Autor

**Edson José dos Santos**  
SDET (Software Development Engineer in Test) & Performance Enthusiast
# 📦 Estoque Pro

**Estoque Pro** é um sistema web de **gerenciamento de estoque** desenvolvido com **Lovable** e integrado ao **Supabase**, voltado para o controle de produtos, categorias, fornecedores e movimentações de entrada e saída.  
O objetivo é oferecer uma solução simples, moderna e eficiente para o acompanhamento de inventário em tempo real.

🔗 **Acesse o sistema online:** [daniels-stock-manager.lovable.app](https://daniels-stock-manager.lovable.app)

---

## 🚀 Funcionalidades principais

- 📋 **Cadastro de produtos** com marca, tipo, preço, custo e quantidade em estoque  
- 🧾 **Controle de movimentações** (entrada e saída de estoque)  
- 🏷️ **Gestão de categorias e fornecedores**  
- 💰 **Cálculo automático de margem de lucro**  
- 📊 **Visualização geral do estoque** com indicadores e estatísticas  
- 🕒 **Histórico de atualizações** e movimentações  
- 🔐 **Integração com Supabase** para autenticação e persistência de dados  

---

## 🧩 Tecnologias utilizadas

| Camada | Tecnologia | Descrição |
|:--|:--|:--|
| Frontend | **Lovable** | Plataforma no-code/low-code para criação de aplicações web responsivas |
| Backend / Banco de Dados | **Supabase** | Backend as a Service com autenticação, banco de dados PostgreSQL e API REST |
| Banco de Dados | **PostgreSQL** | Base relacional utilizada pelo Supabase |
| Autenticação | **Supabase Auth** | Gerenciamento de usuários e permissões |
| Hospedagem | **Lovable Hosting** | Deploy automatizado e integração contínua |

---

## ⚙️ Estrutura de Dados (principais tabelas)

O Supabase foi modelado com base nas seguintes entidades principais:

- **produto**  
  `id`, `marca`, `tipo`, `preco_unitario`, `custo`, `obs`, `id_categoria`, `id_fornecedor`, `codigo`, `quantidade_estoque`, `data_criacao`, `data_atualizacao`

- **categorias**  
  `id`, `nome`

- **fornecedor**  
  `id`, `nome`, `contato`, `email`, `telefone`, `cnpj`

- **movimentacao_estoque**  
  `id`, `id_produto`, `tipo_movimentacao` (entrada/saída), `quantidade`, `data_movimentacao`, `observacao`

---

## 🧠 Regras de Negócio

- A **quantidade em estoque** é atualizada automaticamente conforme movimentações.  
- Não é permitido registrar uma **saída** maior do que o estoque disponível.  
- O sistema calcula a **margem de lucro** de cada produto com base em:  
  ```
  margem_lucro = ((preco_unitario - custo) / custo) * 100
  ```
- Cada produto pertence a uma **categoria** e a um **fornecedor**.  

---

## 🧭 Como executar o projeto localmente (modo desenvolvedor)

> ⚠️ O Lovable é uma plataforma hospedada, então o desenvolvimento local é opcional.  
> Você pode conectar seu Supabase e visualizar tudo direto no painel.

### 1️⃣ Clone este repositório
```bash
git clone https://github.com/SEU_USUARIO/daniels-stock-manager.git
cd daniels-stock-manager
```

### 2️⃣ Configure o Supabase
Crie um projeto no [Supabase](https://supabase.com) e copie suas chaves de API.

Crie um arquivo `.env` (se aplicável):
```
SUPABASE_URL=https://xyzcompany.supabase.co
SUPABASE_ANON_KEY=seu_anon_key
```

### 3️⃣ Conecte no Lovable
- Acesse o [Lovable](https://lovable.app)  
- Importe o projeto ou conecte ao seu repositório GitHub  
- Configure as variáveis de ambiente com os dados do Supabase  
- Publique o app diretamente pelo painel

---

## 📊 Demonstração

Acesse o app funcional:  
👉 [https://daniels-stock-manager.lovable.app](https://daniels-stock-manager.lovable.app)

---

## 💡 Melhorias Futuras

- 📈 Gráficos de desempenho de vendas e reposição  
- 🔔 Notificações automáticas de estoque baixo  
- 📦 Relatórios exportáveis (PDF/Excel)  
- 👥 Permissões por usuário (admin / colaborador)  
- 📱 Aplicativo mobile integrado  

---

## 🤝 Contribuindo

Sinta-se à vontade para sugerir melhorias ou abrir PRs!

1. Faça um fork do projeto  
2. Crie uma branch para sua feature  
   ```bash
   git checkout -b feature/nova-funcionalidade
   ```
3. Faça commit das alterações  
   ```bash
   git commit -m "Adiciona nova funcionalidade"
   ```
4. Envie para o repositório remoto  
   ```bash
   git push origin feature/nova-funcionalidade
   ```
5. Abra um Pull Request  

---

## 🧾 Licença

Este projeto é distribuído sob a licença **MIT**.  
Sinta-se livre para usar e adaptar conforme necessário.

---

# 📦 Modelo Lógico do Banco de Dados — Estoque Pro

O banco de dados foi projetado para o **gerenciamento de estoque** com controle de produtos, categorias, fornecedores e movimentações.  
Desenvolvido utilizando **Supabase (PostgreSQL)** e integrado ao **Lovable App**.

---

## 🧱 Estrutura do Banco de Dados

### **Tabela: produto**
| Campo | Tipo | Descrição |
|--------|------|------------|
| id | int8 (PK) | Identificador único do produto |
| marca | varchar | Marca ou fabricante |
| tipo | varchar | Tipo ou modelo do produto |
| preco_unitario | float8 | Valor de venda unitário |
| custo | float8 | Custo do produto |
| obs | varchar | Observações |
| id_categoria | int8 (FK) | Relaciona à tabela categorias |
| id_fornecedor | int8 (FK) | Relaciona à tabela fornecedor |
| codigo | text | Código interno ou de barras |
| quantidade_estoque | int8 | Quantidade em estoque |
| data_criacao | timestamptz | Data de criação |
| data_atualizacao | timestamptz | Data da última atualização |

---

### **Tabela: categorias**
| Campo | Tipo | Descrição |
|--------|------|------------|
| id | int8 (PK) | Identificador da categoria |
| nome | text | Nome da categoria |

---

### **Tabela: fornecedor**
| Campo | Tipo | Descrição |
|--------|------|------------|
| id | int8 (PK) | Identificador do fornecedor |
| nome | varchar | Nome do fornecedor |
| contato | varchar | Nome do contato |
| email | text | E-mail de contato |
| telefone | varchar | Telefone |
| cnpj | varchar | CNPJ da empresa |
| endereco | text | Endereço físico |

---

### **Tabela: entradas_estoque**
| Campo | Tipo | Descrição |
|--------|------|------------|
| id | int8 (PK) | Identificador da entrada |
| id_produto | int8 (FK) | Produto relacionado |
| id_fornecedor | int8 (FK) | Fornecedor da entrada |
| quantidade | int8 | Quantidade recebida |
| preco_custo | float8 | Custo unitário |
| data_entrada | date | Data da entrada |

---

### **Tabela: saidas_estoque**
| Campo | Tipo | Descrição |
|--------|------|------------|
| id | int8 (PK) | Identificador da saída |
| id_produto | int8 (FK) | Produto retirado |
| quantidade | int8 | Quantidade retirada |
| data_saida | date | Data da saída |
| obs | varchar | Observações (motivo da saída) |

---

## 🔗 Diagrama de Relacionamentos (Resumo)

```
categorias (1) ───< (N) produto (1) >─── (N) fornecedor
│
└──────────────┬──────────────┘
               ▼
     entradas_estoque (N)
     saidas_estoque (N)
```

---

## ⚖️ Regras de Integridade

- Todas as chaves estrangeiras são validadas (integridade referencial).  
- Entradas incrementam e saídas decrementam a quantidade em estoque.  
- Margem de lucro = ((preco_unitario - custo) / custo) * 100.  
- Campos de data permitem auditoria e rastreabilidade.  

---

### 💡 Tecnologias Utilizadas
- **Supabase (PostgreSQL)** — Banco de dados e autenticação  
- **Lovable** — Interface visual e integração com Supabase  
- **SQL Functions** — Para cálculos de estoque e margem de lucro  

---

> Documentação do modelo lógico do projeto **[Estoque Pro](https://daniels-stock-manager.lovable.app/)**.

# 🤖 Agente SQL Inteligente para E-commerce

Sistema completo que permite **consultas em linguagem natural** sobre um banco de dados de e-commerce, convertendo perguntas humanas em **SQL seguro**, com **validação, cache, fallback, visualizações automáticas e API REST**.

Projeto desenhado com **arquitetura limpa**, múltiplos **LLM Providers intercambiáveis** e foco em **robustez, escalabilidade e uso real em produção**.

---

## 🚀 Principais Funcionalidades

- 🧠 **NL → SQL** usando Inteligência Artificial
- 🔁 **Múltiplos LLMs** (Gemini, OpenAI, Claude, Ollama) com fallback automático
- 🔒 **Validação rigorosa de SQL** (somente SELECT)
- ⚡ **Cache avançado** (LRU + TTL + métricas)
- 📊 **Sugestão automática de visualizações**
- 🧾 **Logging estruturado e métricas**
- 🌐 **API REST completa**
- 🛡️ **Rate limiting**
- 🧪 **Fallback rule-based quando IA indisponível**
- 🧩 Arquitetura **plugável e extensível**

---

## 🧠 Arquitetura

O projeto segue o princípio de **separação total de responsabilidades**.

```text
app_final.py
 └── services/
      └── nl_to_sql.py
           └── llm/
                ├── router.py
                ├── base.py
                └── providers/
                     ├── gemini.py
                     ├── openai.py
                     ├── claude.py
                     └── ollama.py
🔹 Responsabilidades
Responsabilidade
Camada
App
API, HTTP, cache, logging, validação
Router
Escolha automática do LLM
Provider
Gerar SQL puro
Validator
Garantir SQL seguro
Database
Executar queries
Visualization
Sugerir gráficos
⚠️ O app não conhece SDKs de IA.
Toda a inteligência está encapsulada nos providers.
🔌 LLM Providers Suportados
Provider
Status
Google Gemini
✅
OpenAI
✅
Claude (Anthropic)
✅
Ollama (local)
✅
Fallback automático caso um provider falhe.
🛠️ Tecnologias Utilizadas
Python 3.10+
Flask
SQLite
Google Gemini SDK
OpenAI SDK
Anthropic SDK
Ollama
Flask-Limiter
Flask-CORS
dotenv
⚙️ Configuração
1️⃣ Clone o repositório
Copiar código
Bash
git clone https://github.com/seu-usuario/agente-sql-ecommerce.git
cd agente-sql-ecommerce
2️⃣ Crie o ambiente virtual
Copiar código
Bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
3️⃣ Instale as dependências
Copiar código
Bash
pip install -r requirements.txt
4️⃣ Configure o .env
Copiar código
Env
GEMINI_API_KEY=xxxxxxxx
OPENAI_API_KEY=xxxxxxxx
ANTHROPIC_API_KEY=xxxxxxxx

FLASK_PORT=5000
FLASK_DEBUG=True

CACHE_MAX_SIZE=100
CACHE_TTL_HOURS=24
VALIDATION_LEVEL=moderate
▶️ Executando o Projeto
Copiar código
Bash
python app_final.py
Acesse:
Copiar código

http://127.0.0.1:5000
📡 Endpoints Principais
🔹 Status do sistema
Copiar código
Http
GET /api/status
🔹 Executar consulta NL → SQL
Copiar código
Http
POST /api/query
Content-Type: application/json

{
  "pergunta": "Total de vendas hoje"
}
🔹 Dashboard em tempo real
Copiar código
Http
GET /api/dashboard
🔹 Schema do banco
Copiar código
Http
GET /api/schema
🔹 Estatísticas de uso
Copiar código
Http
GET /api/stats
🔹 Health Check
Copiar código
Http
GET /api/health
💬 Exemplos de Perguntas
Total de vendas hoje
Produtos com estoque baixo
Top 5 produtos mais vendidos
Vendas por mês nos últimos 6 meses
Clientes que mais compraram
Ticket médio dos clientes
Produtos nunca vendidos
Clientes inativos há mais de 30 dias
🔐 Segurança
Apenas SELECT permitido
SQL validado antes da execução
Rate limiting por IP
Sanitização defensiva de respostas de IA
📊 Cache & Performance
Cache LRU com TTL
Métricas de hit rate
Evicção automática
Limpeza de entradas expiradas
🧪 Fallback Inteligente
Se nenhum LLM estiver disponível:
Sistema aplica regras determinísticas
Nunca quebra a API
Retorna resposta controlada
📈 Casos de Uso
BI conversacional
Dashboards executivos
Análise de vendas e estoque
Atendimento interno (CS, comercial)
MVP para SaaS de analytics
Ensino de SQL assistido por IA
🧩 Extensibilidade
Adicionar um novo LLM é simples:
Copiar código
Python
class MeuProvider(LLMProvider):
    name = "MEU_LLM"
    def generate(self, prompt: str) -> str:
        return sql
Registrar no Router e pronto.
📜 Licença
MIT License.
👤 Autor
Dione Castro Alves
Consultor Tecnológico | Desenvolvedor Full Stack | Especialista em IA
Founder — InNovaIdeia Assessoria em Tecnologia ®
⭐ Se este projeto te ajudou
Deixe uma ⭐ no repositório — isso ajuda muito!
Copiar código

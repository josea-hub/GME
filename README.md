# GME
GME: Gestão de material do estoque
# SGMS — Sistema de Gestão de Materiais e Serviços

Aplicação web responsiva e acessível para controle de inventário, registro de movimentações por setor, alertas automáticos de estoque mínimo e exportação de relatórios gerenciais em Excel (`.xlsx`), com persistência em nuvem e isolamento de dados por unidade.

---

## 🔗 Acesso ao Sistema (Ambiente de Demonstração)

* **Aplicação Online (Servidor Público/Estático via Netlify):** `[COLE_AQUI_O_SEU_LINK_DO_NETLIFY]`
* **Repositório do Código-Fonte:** Disponível neste diretório (`index.html` e estrutura SQL)

---

## 🏛️ Cenário Institucional de Simulação

O sistema adota uma arquitetura hierárquica (**Instituição → Unidade/Campus → Setor/Departamento**) projetada para atender órgãos públicos, instituições de ensino e equipes técnicas de manutenção. O ambiente de testes está estruturado com o seguinte cenário modelo:

* **Instituição / Órgão:** Instituição Pública / Órgão Modelo
* **Unidade / Estabelecimento:** Unidade Sede – Campus Central
* **Setores Cadastrados:** Manutenção Predial, Almoxarifado Central e Tecnologia da Informação (TI)

---

## 🧪 Roteiro Passo a Passo para Simulação (Avaliação)

### 1. Acesso ao Painel Administrativo (Credencial de Demonstração)
Para agilizar a avaliação sem a necessidade de aguardar aprovação manual de um novo cadastro, utilize a conta pré-aprovada abaixo:
* **E-mail:** `avaliador@instituicao.edu.br`
* **Senha:** `123456`

### 2. Cadastro de Materiais (Entrada de Estoque)
1. Acesse a aba **"Estoque Atual (Entrada)"**.
2. Preencha os dados de um item de consumo (ex.: *Cabo de Rede Cat6*, unidade *metro*, saldo inicial *100*, estoque mínimo *20*) e clique em **+ Adicionar Material**.
3. O item será exibido imediatamente na tabela de inventário da unidade.

### 3. Registro de Retirada e Baixa Automática (Saída)
1. Acesse a aba **"Registar Retirada (Saída)"**.
2. Selecione o material cadastrado, escolha o **Setor de Destino** (ex.: *Manutenção Predial*), informe a quantidade utilizada (ex.: *85*) e confirme o lançamento.
3. **Resultado esperado:** O banco de dados realiza a baixa automática do saldo (reduzindo para *15*) e exibe o **alerta visual de estoque mínimo** no topo da tela.

### 4. Estorno Automático e Controle de Permissão
1. Na tabela de histórico de movimentações, clique em **"Excluir"** no lançamento recém-registrado.
2. **Resultado esperado:** Um gatilho no banco de dados (*SQL Trigger*) executa o estorno automático, devolvendo a quantidade retirada ao saldo real do estoque.

### 5. Fluxo de Cadastro de Novo Servidor / Colaborador (Opcional)
1. Clique em **"Sair"** no cabeçalho e selecione **"Criar conta / Solicitar acesso"** na tela inicial.
2. Vincule o cadastro à instituição, unidade e setor desejados.
3. Por segurança, novos cadastros iniciam com status **Pendente** e só acessam o sistema após aprovação na aba **"Aprovar Usuários (Mestre)"**.

### 6. Acessibilidade e Exportação de Relatórios
* **Recursos Visuais:** Utilize a barra superior para testar o ajuste dinâmico de fonte (**`A-`**, **`A`**, **`A+`**) e o **Modo Alto Contraste** (padrão WCAG).
* **Relatório Gerencial:** Clique em **"Baixar Excel (`.xlsx`)"** para gerar uma planilha contendo exclusivamente o estoque e o histórico isolados da unidade ativa.

---

## 🛠️ Arquitetura e Tecnologias Utilizadas

* **Front-end:** HTML5 Semântico, Tailwind CSS, JavaScript (ES6+) e SheetJS (`xlsx`).
* **Back-end & Banco de Dados (BaaS):** Supabase (PostgreSQL, Autenticação, *SQL Triggers* para integridade de saldo e políticas *Row Level Security — RLS* para isolamento multi-unidades).
* **Acessibilidade:** Controles persistentes de tipografia e alto contraste (`localStorage`), indicadores não dependentes exclusivamente de cor e navegação via teclado/leitores de tela (atributos ARIA).
* **Hospedagem:** Servidor web estático gratuito com HTTPS (Netlify).

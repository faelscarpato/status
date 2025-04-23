# Projeto Status: Controle de Absenteísmo e Status de Máquinas

Este projeto é uma aplicação web simples para monitorar a presença/absenteísmo de funcionários e o status operacional de máquinas, utilizando Supabase como backend para persistência de dados.

## Descrição

A aplicação consiste em três páginas principais:

1.  **Dashboard:** Exibe um resumo visual dos dados de absenteísmo e o status das máquinas para uma data selecionada. Inclui cards de resumo e gráficos.
2.  **Absenteísmo:** Permite registrar a presença, faltas (justificadas/não justificadas), férias, licenças, etc., dos funcionários. Os dados são salvos no Supabase. Oferece filtros por nome, status e período (mês/ano), um resumo visual com gráfico e a opção de exportar os dados filtrados para CSV.
3.  **Status Máquinas:** Permite registrar o status diário das máquinas (molde, ciclo padrão, ciclo atual, observações). Os dados são salvos no Supabase. A página também permite gerar uma imagem da tabela com os registros adicionados *na sessão atual* para compartilhamento rápido.

## Funcionalidades

* **Persistência de Dados:** Utiliza o [Supabase](https://supabase.com/) (backend como serviço open-source) para armazenar e recuperar os dados de absenteísmo e status das máquinas.
* **Interface Responsiva:** Design adaptável para funcionar em desktops e dispositivos móveis, utilizando [Tailwind CSS](https://tailwindcss.com/).
* **Navegação Consistente:** Menu de navegação com painel lateral responsivo para fácil acesso às diferentes seções.
* **Controle de Absenteísmo:**
    * Formulário para adicionar registros diários.
    * Filtros avançados por nome, status e mês/ano.
    * Resumo visual com contagens e gráfico de barras.
    * Exportação dos dados filtrados para formato CSV.
    * Exclusão de registros individuais (com confirmação).
* **Status de Máquinas:**
    * Formulário para adicionar registros diários de status.
    * Exclusão de registros individuais (com confirmação).
    * Geração de imagem (PNG) da tabela com os registros adicionados na sessão atual, utilizando [html2canvas](https://html2canvas.hertzen.com/).
* **Dashboard:**
    * Seleção de data para visualização.
    * Resumo rápido do absenteísmo do dia (cards e gráfico de pizza) utilizando [Chart.js](https://www.chartjs.org/).
    * Tabela com o status das máquinas registrado para o dia selecionado.
* **Feedback Visual:** Indicador de carregamento (spinner) e alertas customizados para sucesso e erro.

## Tecnologias Utilizadas

* **Frontend:** HTML5, CSS3, JavaScript (ES6+)
* **Estilização:** Tailwind CSS v3
* **Backend & Banco de Dados:** Supabase (PostgreSQL)
* **Bibliotecas JavaScript:**
    * `supabase-js`: Cliente oficial do Supabase para interagir com o backend.
    * `chart.js`: Para criação dos gráficos na dashboard e na página de absenteísmo.
    * `html2canvas`: Para gerar a imagem da tabela na página de status das máquinas.

## Configuração e Instalação

1.  **Clone o Repositório:**
    ```bash
    git clone [https://github.com/faelscarpato/status.git](https://github.com/faelscarpato/status.git)
    cd status
    ```

2.  **Crie um Projeto Supabase:**
    * Vá para [supabase.com](https://supabase.com/) e crie uma conta gratuita (se ainda não tiver).
    * Crie um novo projeto.

3.  **Crie as Tabelas no Supabase:**
    * Dentro do seu projeto Supabase, vá para o "SQL Editor".
    * Execute o SQL fornecido nos arquivos `sql_create_table_registros_presenca.sql` e `sql_create_table_status_maquinas.sql` (ou copie os comandos SQL das respostas anteriores) para criar as tabelas `registros_presenca` e `status_maquinas`.
    * **Importante:** Certifique-se de criar as **Políticas de Acesso (RLS Policies)** necessárias para permitir que a aplicação leia e escreva nas tabelas. Exemplos de políticas públicas estão incluídos nos scripts SQL. Adapte conforme sua necessidade.

4.  **Configure as Credenciais Supabase:**
    * No seu projeto Supabase, vá em "Project Settings" > "API".
    * Copie a **URL do Projeto** e a **Chave `anon` public**.
    * Abra os arquivos HTML (`index.html`, `Absenteismo.html`, `status.html` - ajuste os nomes se forem diferentes) no seu editor de código.
    * Encontre as seguintes linhas no JavaScript de **cada arquivo** que interage com o Supabase:
        ```javascript
        const SUPABASE_URL = 'SUA_SUPABASE_URL';
        const SUPABASE_ANON_KEY = 'SUA_SUPABASE_ANON_KEY';
        ```
    * Substitua `'SUA_SUPABASE_URL'` e `'SUA_SUPABASE_ANON_KEY'` pelas suas credenciais reais.

5.  **Abra os Arquivos HTML:**
    * Abra os arquivos `.html` diretamente no seu navegador. Como é um projeto frontend puro (com chamadas para o Supabase), não há necessidade de um servidor web complexo para rodar localmente, mas usar uma extensão como "Live Server" no VS Code pode facilitar o desenvolvimento.

## Uso

* **Dashboard (`index.html`):** Selecione uma data para ver os resumos de absenteísmo e status das máquinas para aquele dia.
* **Absenteísmo (`Absenteismo.html`):** Use o formulário superior para adicionar novos registros. Utilize os filtros para pesquisar registros específicos. Exporte os dados filtrados ou imprima a tabela. Clique em "Remover" para excluir um registro.
* **Status Máquinas (`status.html`):** Preencha o formulário para adicionar o status de uma máquina para a data selecionada. Os registros adicionados aparecerão na tabela abaixo. Clique em "Gerar Imagem da Tabela" para criar um PNG dos dados visíveis na tabela da sessão atual. Clique em "Remover" para excluir um registro do banco de dados e da tabela visual.

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests.

## Licença

Distribuído sob a licença MIT. Veja `LICENSE` para mais informações.

# android-lista-de-compras

Aplicativo Android desenvolvido com Kotlin para gerenciar uma lista de compras, os usuários podem adicionar, visualizar e remover itens da lista de compras.

## 📲 Funcionalidades

- Adicionar itens à lista de compras.
- Exibir a lista de itens adicionados.
- Remover itens ao clicar no botão correspondente.
- Persistência de dados utilizando Room, garantindo que os itens sejam salvos mesmo após o app ser fechado.

---

## ▶️ Como executar o projeto

1. **Pré-requisitos:**
   - Android Studio instalado (recomendado: versão mais recente).
   - Emulador configurado (API 30+ recomendado) ou dispositivo físico conectado.

2. **Executando:**
   - Clone ou baixe este repositório.
   - Abra o projeto no Android Studio.
   - Configure um emulador ou conecte um dispositivo físico.
   - Execute o aplicativo pressionando `Shift + F10` ou clicando no botão ▶️.

---

## 📂 Estrutura do Projeto

### 🔵 **Data Layer**  
Responsável por gerenciar o banco de dados e fornecer acesso aos dados persistidos.

- **`ItemDao` (Data Access Object)**  
  Define as operações de banco de dados:  
  - Buscar todos os itens (`getAll()`)
  - Inserir um novo item (`insert()`)
  - Remover um item (`delete()`)

- **`ItemDatabase`**  
  Configura o banco de dados Room, listando as entidades e fornecendo acesso ao DAO.

---

### 🟢 **Model Layer**  
Define os modelos de dados utilizados pelo aplicativo.

- **`ItemModel`**  
  Representa um item na lista de compras.  
  - `id`: Identificador único gerado automaticamente.
  - `name`: Nome do item, inserido pelo usuário.

---

### 🟣 **ViewModel Layer**  
Responsável por fornecer os dados para a interface do usuário e gerenciar a lógica de negócios.

- **`ItemsViewModel`**  
  - Gerencia a lista de itens como um objeto `LiveData`.
  - Realiza operações de inserção e remoção em threads de I/O utilizando corrotinas.
  - Interage com o banco de dados Room para persistência.

- **`ItemsViewModelFactory`**  
  - Fábrica para criar instâncias de `ItemsViewModel`.

- **`ItemsAdapter`**  
  - Adapter para exibir a lista de itens no `RecyclerView`.
  - Gerencia as interações do usuário, como remoção de itens.

---

### 🔴 **View Layer**  
Responsável pela interface com o usuário.

- **`MainActivity`**  
  - Exibe a lista de compras em um `RecyclerView`.
  - Permite que o usuário adicione novos itens através de um `EditText` e botão.
  - Observa mudanças no `LiveData` gerenciado pelo `ItemsViewModel` para atualizar a interface.

---

## 🛠 Tecnologias Utilizadas

- **Kotlin**: Linguagem principal do projeto.
- **Room**: Biblioteca para persistência de dados.
- **MVVM**: Arquitetura para separação de responsabilidades.
- **RecyclerView**: Para exibição de listas.
- **Coroutines**: Para operações assíncronas.
- **LiveData**: Para monitorar e reagir a mudanças de dados.

---

## ⚙️ Funcionamento do Aplicativo

### 1. Inicialização
- O banco de dados Room é configurado e acessado através de `ItemDatabase`.
- A `MainActivity` inicializa o `ItemsViewModel` e configura o `RecyclerView` com o `ItemsAdapter`.
- A lista de itens é carregada do banco de dados e exibida na interface.

### 2. Adicionando Itens
- O usuário insere o nome de um item no campo de texto e clica no botão **"Adicionar"**.
- O item é salvo no banco de dados utilizando o método `addItem()` no `ItemsViewModel`.

### 3. Removendo Itens
- O usuário clica no botão correspondente ao item que deseja remover.
- O item é excluído do banco de dados utilizando o método `removeItem()` no `ItemsViewModel`.

### 4. Observando Mudanças
- A interface é automaticamente atualizada sempre que os dados no banco de dados mudam, graças ao uso de `LiveData`.

---

## 🎨 Layout

### Tela Inicial
- **Lista de Compras** exibida em um `RecyclerView`.
- Campo de texto para adicionar novos itens.
- Botão para confirmar a adição de itens.

### Exemplo no Emulador
![image](https://github.com/user-attachments/assets/0f789549-6241-461b-b83c-178aed4ed7dc)


---

## 🚀 Próximos Passos

- Implementar uma funcionalidade para editar itens.
- Adicionar suporte a múltiplas listas de compras.
- Melhorar o design da interface com Material Design.
- Implementar testes unitários para o ViewModel e DAO.

# Operações de Atualização e Remoção (Update e Delete)

Este módulo descreve a implementação e o funcionamento das operações de atualização (`Update`) e remoção (`Delete`) para o gerenciamento de maquiagens no sistema.

---

## 1. Atualização de Maquiagem (Update)

A operação de atualização permite modificar os atributos de um produto de maquiagem existente com base no seu identificador exclusivo (ID).

### Endpoints
* **Método HTTP:** `PUT` ou `PATCH`
* **Caminho:** `/api/maquiagem/{id}`

### Parâmetros de Requisição
* **id** (na URL): Identificador único da maquiagem.

### Corpo da Requisição (JSON)
```json
{
  "nome": "Base Líquida Matte - Atualizada",
  "marca": "Marca Exemplo",
  "preco": 59.90,
  "estoque": 120,
  "categoria": "Rosto"
}
```

### Respostas Esperadas
* **200 OK:** Produto atualizado com sucesso. Retorna o objeto modificado.
* **400 Bad Request:** Dados de entrada inválidos ou falha na validação do formato.
* **404 Not Found:** Registro de maquiagem não encontrado para o ID fornecido.

---

## 2. Remoção de Maquiagem (Delete)

A operação de remoção exclui permanentemente (ou desativa, no caso de exclusão lógica) um registro de maquiagem do sistema.

### Endpoints
* **Método HTTP:** `DELETE`
* **Caminho:** `/api/maquiagem/{id}`

### Parâmetros de Requisição
* **id** (na URL): Identificador único da maquiagem a ser removida.

### Respostas Esperadas
* **204 No Content:** Remoção realizada com sucesso. Nenhum conteúdo é retornado no corpo.
* **404 Not Found:** Registro de maquiagem não encontrado para o ID fornecido.

---

## Regras de Negócio e Validações

* **Validação de Preço:** O preço atualizado não pode ser negativo ou igual a zero.
* **Integridade de Estoque:** A quantidade em estoque deve ser um número inteiro maior ou igual a zero.
* **Exclusão Lógica vs Física:** Dependendo da configuração do ambiente, o método `DELETE` aplicará exclusão lógica (campo `ativo = false`) para preservar o histórico de vendas.

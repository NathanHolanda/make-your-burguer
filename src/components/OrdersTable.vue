<template>
  <div class="container">
    <table>
      <thead>
        <tr>
          <th>Nº</th>
          <th>Cliente</th>
          <th>Pão</th>
          <th>Carne</th>
          <th>Adicionais</th>
          <th>Status</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>1</td>
          <td>Maria</td>
          <td>Tradicional</td>
          <td>Maminha</td>
          <td>
            <ul>
              <li>Salame</li>
              <li>Tomate</li>
            </ul>
          </td>
          <td>
            <select v-model="status">
              <option value="Solicitado">Solicitado</option>
              <option value="Em produção">Em produção</option>
              <option value="Finalizado">Finalizado</option>
            </select>
          </td>
          <td><button class="cancel">Cancelar</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.container {
    width: 100%;
    display: flex;
    justify-content: center;
}

table{
    border-collapse: collapse;
}

th{
    border-bottom: 3px solid #222;
}

th, td {
    text-align: left;
    padding: 10px 50px 10px 5px;
}

li {
    list-style-type: none;
    padding: 5px 0;
}

.cancel{
    cursor: pointer;
    background-color: #222;
    color: #fcba03;
    padding: 5px 20px;
    transition: 0.2s;
}

.cancel:hover{
    opacity: 0.8;
}
</style>
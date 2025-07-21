Diretriz obrigatória: Todos os parâmetros de função devem ter tipos explícitos declarados. Não confie na inferência de tipos para parâmetros. Exemplo:

```ts
function calcularArea(largura: number, altura: number): number {
  return largura * altura;
}
```

Diretriz obrigatória: Todas as interfaces devem ser nomeadas com prefixo "I" maiúsculo. Use interfaces em vez de types para definir contratos de objetos. Exemplo:

```ts
interface IUsuario {
  id: number;
  nome: string;
  email: string;
  ativo: boolean;
}

function criarUsuario(dados: IUsuario): IUsuario {
  return dados;
}
```

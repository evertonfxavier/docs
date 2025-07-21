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

Diretriz obrigatória: Use enums para valores constantes relacionados. Prefira string enums sobre numeric enums para melhor legibilidade. Exemplo:

```ts
enum StatusPedido {
  PENDENTE = "pendente",
  PROCESSANDO = "processando",
  CONCLUIDO = "concluido",
  CANCELADO = "cancelado",
}

function atualizarStatus(status: StatusPedido): void {
  console.log(`Status atualizado para: ${status}`);
}
```

Diretriz obrigatória: Sempre defina tipos de retorno explícitos em funções. Isso melhora a documentação e evita mudanças não intencionais. Exemplo:

```ts
function buscarUsuarioPorId(id: number): Promise<IUsuario | null> {
  return fetch(`/api/usuarios/${id}`).then((response) => response.json());
}
```

Diretriz obrigatória: Use union types para valores que podem ser de tipos diferentes. Evite usar `any` ou `unknown` desnecessariamente. Exemplo:

```ts
type StatusResposta = "sucesso" | "erro" | "carregando";

interface IResposta {
  status: StatusResposta;
  dados?: any;
  mensagem?: string;
}
```

Diretriz obrigatória: Implemente validação de tipos em runtime para dados externos usando type guards. Exemplo:

```ts
function isUsuario(obj: any): obj is IUsuario {
  return (
    obj &&
    typeof obj.id === "number" &&
    typeof obj.nome === "string" &&
    typeof obj.email === "string" &&
    typeof obj.ativo === "boolean"
  );
}

function processarDadosUsuario(dados: unknown): IUsuario | null {
  if (isUsuario(dados)) {
    return dados;
  }
  return null;
}
```

Diretriz obrigatória: Use readonly para propriedades que não devem ser modificadas após a criação. Prefira imutabilidade quando possível. Exemplo:

```ts
interface IConfiguracaoSistema {
  readonly versao: string;
  readonly ambiente: "desenvolvimento" | "producao";
  readonly limiteUsuarios: number;
}

const config: IConfiguracaoSistema = {
  versao: "1.0.0",
  ambiente: "producao",
  limiteUsuarios: 1000,
};
```

Diretriz obrigatória: Use generic types para criar componentes reutilizáveis. Sempre forneça constraints quando necessário. Exemplo:

```ts
interface IRepositorio<T extends { id: number }> {
  buscarPorId(id: number): Promise<T | null>;
  salvar(item: T): Promise<T>;
  deletar(id: number): Promise<boolean>;
}

class RepositorioUsuario implements IRepositorio<IUsuario> {
  async buscarPorId(id: number): Promise<IUsuario | null> {
    // implementação
    return null;
  }

  async salvar(usuario: IUsuario): Promise<IUsuario> {
    // implementação
    return usuario;
  }

  async deletar(id: number): Promise<boolean> {
    // implementação
    return true;
  }
}
```

Diretriz obrigatória: Use utility types do TypeScript para transformações de tipos. Evite duplicação de definições. Exemplo:

```ts
interface IUsuarioCompleto {
  id: number;
  nome: string;
  email: string;
  senha: string;
  perfil: string;
  ativo: boolean;
}

// Para criação (sem id)
type IUsuarioCreate = Omit<IUsuarioCompleto, "id">;

// Para atualização (campos opcionais)
type IUsuarioUpdate = Partial<
  Pick<IUsuarioCompleto, "nome" | "email" | "perfil" | "ativo">
>;

// Para resposta pública (sem senha)
type IUsuarioPublico = Omit<IUsuarioCompleto, "senha">;
```

Diretriz obrigatória: Organize imports de forma consistente. Agrupe por categoria e ordene alfabeticamente dentro de cada grupo. Exemplo:

```ts
// Bibliotecas externas
import express from "express";
import mongoose from "mongoose";

// Módulos internos do projeto
import { IUsuario } from "../interfaces/IUsuario";
import { RepositorioUsuario } from "../repositorios/RepositorioUsuario";
import { ValidationHelper } from "../utils/ValidationHelper";

// Imports relativos
import "./configuracao";
```

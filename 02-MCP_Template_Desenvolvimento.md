# Template para MCP de Desenvolvimento

Este documento fornece um template padronizado para a criação de Model Context Protocols (MCPs) na categoria de Desenvolvimento. Use este template como base para criar novos MCPs relacionados a padrões de código, arquitetura e implementação.

## Estrutura do Template

```markdown
# MCP-DEV-[NÚMERO]: [TÍTULO]

## 1. Resumo
[Breve descrição do padrão de desenvolvimento]

## 2. Motivação
[Por que este padrão de desenvolvimento é necessário]

## 3. Especificação
### 3.1 Padrões de Código
[Detalhes sobre convenções de codificação]

### 3.2 Arquitetura
[Princípios arquiteturais e padrões de design]

### 3.3 Ferramentas e Tecnologias
[Ferramentas e tecnologias recomendadas]

## 4. Implementação
[Guia passo a passo para implementar o padrão]

## 5. Exemplos
[Exemplos de código e implementações]

## 6. Considerações
[Casos especiais e limitações]

## 7. Referências
[Fontes e documentos relacionados]

## 8. Metadados
- **Autor**: [Nome]
- **Versão**: [Número]
- **Data de Criação**: [Data]
- **Última Atualização**: [Data]
- **Status**: [Status]
- **Aprovado por**: [Nome]
```

## Instruções de Uso

1. Copie o template acima para um novo arquivo
2. Substitua os campos entre colchetes com o conteúdo apropriado
3. Atribua um número sequencial único para o MCP
4. Preencha todas as seções com detalhes relevantes
5. Inclua exemplos práticos e casos de uso
6. Submeta para revisão seguindo o processo definido no Guia de Implementação de MCPs

## Exemplo de MCP de Desenvolvimento

```markdown
# MCP-DEV-001: Padrões de Codificação JavaScript/TypeScript

## 1. Resumo
Este MCP define os padrões de codificação para JavaScript e TypeScript no Sistema TEKTRIO. Ele estabelece convenções de nomenclatura, formatação, estrutura de arquivos e práticas recomendadas para garantir código consistente, legível e manutenível em todo o sistema.

## 2. Motivação
A consistência no código é essencial para facilitar a colaboração, reduzir erros e simplificar a manutenção. Com múltiplos desenvolvedores e agentes trabalhando no Sistema TEKTRIO, é crucial ter padrões claros que todos possam seguir. Este MCP visa eliminar debates sobre estilo e permitir que a equipe se concentre na qualidade e funcionalidade do código.

## 3. Especificação
### 3.1 Padrões de Código
#### 3.1.1 Nomenclatura
- **Variáveis e Funções**: camelCase (ex: `getUserData`)
- **Classes**: PascalCase (ex: `UserManager`)
- **Constantes**: UPPER_SNAKE_CASE (ex: `MAX_RETRY_COUNT`)
- **Interfaces**: PascalCase com prefixo I (ex: `IUserData`)
- **Tipos**: PascalCase (ex: `UserType`)
- **Arquivos**: kebab-case (ex: `user-manager.ts`)

#### 3.1.2 Formatação
- Indentação: 2 espaços
- Comprimento máximo de linha: 100 caracteres
- Uso de ponto e vírgula no final das declarações
- Uso de aspas simples para strings
- Espaço após palavras-chave (if, for, while, etc.)
- Espaço antes e depois de operadores (=, +, -, etc.)

#### 3.1.3 Estrutura de Arquivos
- Um componente/classe por arquivo
- Imports agrupados e ordenados: bibliotecas externas primeiro, seguidas por imports internos
- Exports no final do arquivo

### 3.2 Arquitetura
#### 3.2.1 Princípios
- Preferir composição sobre herança
- Seguir princípios SOLID
- Implementar padrões de design apropriados
- Manter componentes pequenos e focados

#### 3.2.2 Organização de Código
- Estrutura de pastas por funcionalidade
- Separação clara entre lógica de negócio e interface do usuário
- Uso de barris (index.ts) para exportações

### 3.3 Ferramentas e Tecnologias
- ESLint para linting
- Prettier para formatação
- TypeScript para tipagem estática
- Jest para testes unitários
- Husky para hooks de pre-commit

## 4. Implementação
1. Configure ESLint e Prettier no projeto:
   ```bash
   npm install --save-dev eslint prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-config-prettier eslint-plugin-prettier
   ```

2. Crie os arquivos de configuração:
   - `.eslintrc.js`
   - `.prettierrc`

3. Configure o Husky para verificar o código antes de commits:
   ```bash
   npm install --save-dev husky lint-staged
   ```

4. Adicione scripts no package.json:
   ```json
   "scripts": {
     "lint": "eslint 'src/**/*.{js,ts,tsx}'",
     "format": "prettier --write 'src/**/*.{js,ts,tsx}'",
     "prepare": "husky install"
   }
   ```

5. Integre com o Cursor IDE:
   - Configure o Cursor para usar ESLint e Prettier
   - Habilite formatação automática ao salvar

## 5. Exemplos
### 5.1 Exemplo de Código Bem Formatado
```typescript
// Constantes
const MAX_RETRY_COUNT = 3;

// Interface
interface IUserData {
  id: string;
  name: string;
  email: string;
  isActive: boolean;
}

// Classe
class UserManager {
  private users: IUserData[] = [];

  constructor(initialUsers: IUserData[] = []) {
    this.users = initialUsers;
  }

  public getUserById(id: string): IUserData | undefined {
    return this.users.find((user) => user.id === id);
  }

  public addUser(userData: Omit<IUserData, 'id'>): IUserData {
    const newUser = {
      id: this.generateId(),
      ...userData,
    };
    
    this.users.push(newUser);
    return newUser;
  }

  private generateId(): string {
    return Math.random().toString(36).substring(2, 9);
  }
}

// Função
function formatUserName(user: IUserData): string {
  return user.name.toUpperCase();
}

export { UserManager, formatUserName };
export type { IUserData };
```

## 6. Considerações
- Estes padrões devem ser aplicados a todo novo código, mas a refatoração de código legado pode ser gradual
- Em casos excepcionais onde os padrões não podem ser seguidos, documentar a razão com comentários
- Revisões de código devem verificar a conformidade com estes padrões

## 7. Referências
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [ESLint Documentation](https://eslint.org/docs/user-guide/)
- [Prettier Documentation](https://prettier.io/docs/en/)

## 8. Metadados
- **Autor**: Equipe TEKTRIO
- **Versão**: 1.0.0
- **Data de Criação**: 07/04/2025
- **Última Atualização**: 07/04/2025
- **Status**: Aprovado
- **Aprovado por**: Agente Especialista Modular
```

## Dicas para Criação de MCPs de Desenvolvimento Eficazes

1. **Seja específico**: Forneça detalhes concretos, não apenas diretrizes gerais
2. **Inclua exemplos**: Exemplos de código real ajudam a esclarecer as expectativas
3. **Explique o porquê**: Justifique as decisões para ajudar na compreensão e adoção
4. **Considere o contexto**: Adapte as recomendações ao contexto específico do Sistema TEKTRIO
5. **Mantenha atualizado**: Revise e atualize regularmente para refletir as melhores práticas atuais

## Próximos Passos

Após criar um MCP de Desenvolvimento usando este template:

1. Submeta para revisão por pares
2. Incorpore o feedback recebido
3. Obtenha aprovação formal
4. Publique no repositório de documentação
5. Comunique à equipe
6. Monitore a adoção e eficácia
7. Atualize conforme necessário
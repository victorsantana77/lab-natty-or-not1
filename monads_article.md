# λ Monads

Monads são um conceito central na programação funcional e têm origem na teoria da categoria, especificamente em linguagens de programação como Haskell. Em termos simples, uma monad é uma estrutura de dados que representa uma sequência de computações ou operações encapsuladas. Elas são úteis para lidar com efeitos colaterais, como entrada/saída, exceções, estado mutável, etc., de uma maneira pura e funcional.

Na prática, monads fornecem uma maneira de encadear operações sequenciais em um contexto específico, garantindo que as operações subsequentes só sejam executadas se as anteriores forem bem-sucedidas. Elas também garantem que o contexto do efeito colateral seja devidamente manipulado, sem quebrar as propriedades de pureza funcional.

Por exemplo, em Haskell, a Monad Maybe é comumente usada para lidar com computações que podem falhar. A Monad IO é usada para lidar com entrada/saída de forma segura e controlada. Em linguagens de programação imperativas, como JavaScript, as Promises podem ser consideradas uma forma de monads para lidar com computações assíncronas.

Em resumo, monads são uma abstração poderosa que permite lidar com efeitos colaterais de uma maneira segura e com composição elegante de código.

### Code example in Python:

```Python
class Maybe:
    def __init__(self, value):
        self.value = value

    def bind(self, func):
        if self.value is None:
            return Maybe(None)
        else:
            return func(self.value)

    def __repr__(self):
        return f'Maybe({self.value})'

# Funções de exemplo para demonstrar o uso da Monad Maybe
def safe_divide(x):
    return Maybe(10 / x) if x != 0 else Maybe(None)

def add_one(x):
    return Maybe(x + 1)

# Uso da Monad Maybe para encadear operações de forma segura
result = Maybe(5).bind(safe_divide).bind(add_one)
print(result)  # Saída: Maybe(3.0)

result = Maybe(0).bind(safe_divide).bind(add_one)
print(result)  # Saída: Maybe(None)
```

## Tipos de Monads

**Maybe Monad**: Também conhecida como opcional ou talvez em algumas linguagens, é usada para representar cálculos que podem falhar, retornando um valor ou nada.

**List Monad**: Usada para representar cálculos não determinísticos ou não singulares, onde há múltiplos resultados possíveis. Ela encapsula uma lista de valores, permitindo operações sobre cada elemento da lista.

**State Monad**: Utilizada para representar cálculos que envolvem estado mutável. Ela encapsula uma função que recebe e retorna um estado.

**Reader Monad**: Usada para representar cálculos que dependem de um contexto compartilhado, mas imutável. Ela encapsula uma função que recebe esse contexto como entrada.

**Writer Monad**: Utilizada para adicionar informações adicionais a um cálculo sem alterar o resultado subjacente. Ela encapsula um valor e um log associado.

**Either Monad**: Similar ao Maybe Monad, mas mais geral, pois pode transportar informações sobre o tipo de erro que ocorreu em caso de falha.

**IO Monad**: Usada para representar cálculos que interagem com o mundo exterior, como entrada e saída. Ela encapsula uma ação que, quando executada, realiza operações de entrada/saída.

## Implementação de monads em linguagens funcionais.

### Haskell

```haskell
module Main where

import Control.Monad (ap)

-- Definindo a estrutura da monad Identity
newtype Identity a = Identity { runIdentity :: a }

-- Implementando a instância de Monad para Identity
instance Functor Identity where
    fmap f (Identity x) = Identity (f x)

instance Applicative Identity where
    pure = Identity
    (<*>) = ap

instance Monad Identity where
    return = pure
    (Identity x) >>= f = f x

-- Exemplo de uso da monad Identity
main :: IO ()
main = do
    let x = Identity 10
        y = x >>= \a -> Identity (a * 2)
        z = do
            a <- x
            b <- y
            return (a + b)
    print $ runIdentity z

```

### Rust

Em Rust, a estrutura Result é frequentemente comparada às monads de outras linguagens de programação funcionais, embora Rust não tenha monads como conceito nativo na linguagem. No entanto, Result pode ser vista como uma forma de monad, pois encapsula um valor que pode ser um sucesso (`Ok`) ou um erro (`Err`).

```rust
fn divide(x: i32, y: i32) -> Result<i32, &'static str> {
    if y == 0 {
        Err("Divisão por zero!")
    } else {
        Ok(x / y)
    }
}
    
fn calculate(x: i32, y: i32, z: i32) -> Result<i32, &'static str> {
        let result = divide(x, y)?;
        let final_result = divide(result, z)?;
        Ok(final_result)
    }


fn main() {
    // Exemplo de uso
    match calculate(10, 2, 0) {
        Ok(value) => println!("Resultado: {}", value),
        Err(err) => println!("Erro: {}", err),
    }
}
```
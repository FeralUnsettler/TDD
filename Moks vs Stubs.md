**Mocks** e **Stubs** são dois tipos diferentes de objetos usados em testes de software, especialmente em testes unitários e de integração. Ambos fazem parte das práticas de testes automatizados, como o **Desenvolvimento Orientado por Testes (TDD)**, e são amplamente utilizados para simular comportamentos e dependências no código. No entanto, eles possuem diferenças fundamentais em termos de finalidade e como são usados.

### **Mocks (Simulações)**

Um **Mock** é um objeto simulado que verifica se certas interações ocorrem durante o teste. Mocks são usados para verificar o comportamento do sistema, especialmente se o código que está sendo testado chama métodos de uma maneira específica ou na ordem correta.

#### **Características dos Mocks:**

1. **Foco na Interação:** Mocks se concentram na verificação de interações entre o objeto sob teste e suas dependências. Eles validam se métodos específicos foram chamados com determinados parâmetros, quantas vezes foram chamados, ou até mesmo em que ordem (Freeman & Pryce, 2009).

2. **Testes Baseados em Comportamento:** Mocks são utilizados principalmente para testes baseados em comportamento, onde o foco está em como o objeto sob teste se comporta e interage com seus colaboradores, ao invés do resultado final.

3. **Verificação Automática:** Mocks geralmente incluem lógica para verificar automaticamente se os métodos esperados foram chamados conforme esperado. Ferramentas como **Mockito** em Java, **Sinon** em JavaScript ou **unittest.mock** em Python são usadas para criar mocks.

4. **Feedback Detalhado:** Mocks oferecem feedback detalhado sobre como um método foi usado, o que é útil para entender falhas em testes baseados em comportamento.

#### **Exemplo de Uso de Mock:**

Em um sistema de pagamento, por exemplo, um mock pode ser usado para verificar se a classe de pagamento chama o método `processarPagamento` da classe `GatewayDePagamento` com o parâmetro correto:

```python
from unittest.mock import Mock

# Mock da classe GatewayDePagamento
gateway_mock = Mock()
gateway_mock.processarPagamento = Mock(return_value=True)

# Simula o uso do mock no código de pagamento
pagamento = Pagamento(gateway_mock)
pagamento.realizarPagamento(100)

# Verifica se o método foi chamado corretamente
gateway_mock.processarPagamento.assert_called_with(100)
```

### **Stubs**

Um **Stub** é um objeto simulado que fornece respostas predefinidas a chamadas durante um teste. Ele é usado principalmente para isolar o código que está sendo testado de suas dependências externas, garantindo que o teste se concentre apenas na lógica interna do objeto sob teste.

#### **Características dos Stubs:**

1. **Foco nos Dados de Retorno:** Stubs são usados para fornecer dados ou respostas pré-configuradas a métodos chamados durante um teste, sem se preocupar com a lógica interna ou as interações exatas.

2. **Testes Baseados em Estado:** Stubs são úteis em testes baseados em estado, onde o foco está nos resultados finais produzidos pelo objeto em teste, e não em como ele interage com suas dependências.

3. **Simples e Focado:** Ao contrário dos mocks, stubs não verificam automaticamente as interações. Eles são usados para garantir que o objeto testado receba o input esperado e forneça o output correto, isolando o comportamento de dependências externas.

4. **Menos Feedback sobre Interações:** Stubs não fornecem feedback detalhado sobre como os métodos são chamados, já que eles se concentram nos dados retornados, e não nas interações.

#### **Exemplo de Uso de Stub:**

Imagine que você esteja testando um método que calcula um desconto. Você pode usar um stub para fornecer uma resposta fixa da classe `ServiçoDeDesconto`:

```python
class StubServicoDeDesconto:
    def calcularDesconto(self, valor):
        return 10  # Resposta fixa para fins de teste

servico_stub = StubServicoDeDesconto()
pedido = Pedido(servico_stub)
resultado = pedido.calcularValorComDesconto(100)

assert resultado == 90  # Verifica o resultado com o desconto aplicado
```

### **Principais Diferenças entre Mocks e Stubs**

| **Aspecto**                   | **Mocks**                                                               | **Stubs**                                                             |
|-------------------------------|------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Propósito**                 | Verificar interações entre objetos                                      | Fornecer respostas fixas e predefinidas                              |
| **Tipo de Teste**             | Teste baseado em comportamento                                          | Teste baseado em estado                                              |
| **Verificação Automática**    | Sim, verifica automaticamente se as interações ocorreram conforme esperado | Não, foca apenas no fornecimento de dados predefinidos                |
| **Feedback**                  | Feedback detalhado sobre chamadas de métodos e parâmetros               | Sem feedback sobre interações, apenas resultados de dados de retorno  |
| **Complexidade**              | Normalmente mais complexo devido à lógica de verificação                | Mais simples, foca em fornecer respostas fixas                       |

### **Conclusão**

**Mocks** e **Stubs** são ferramentas poderosas usadas para testar diferentes aspectos de um sistema. Enquanto os **Mocks** são mais adequados para testes que verificam interações e comportamentos entre objetos, os **Stubs** são ideais para isolar dependências externas e testar os resultados finais. A escolha entre mocks e stubs depende do tipo de teste que se deseja realizar: um teste orientado a comportamento, onde as interações são críticas, ou um teste orientado a estado, focado no resultado final. 

### **Referências**

- Freeman, S., & Pryce, N. (2009). *Growing Object-Oriented Software, Guided by Tests*. Addison-Wesley Professional.
- Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*. Prentice Hall.

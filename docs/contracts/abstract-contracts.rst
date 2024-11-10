.. index:: ! contract;abstract, ! abstract contract

.. _abstract-contract:

******************
Contratos Abstratos
******************

Os contratos devem ser marcados como abstratos quando pelo menos uma de suas funções não for implementada
ou quando não fornecem argumentos para todos os construtores de seus contratos base. 
Mesmo que isso não aconteça, um contrato ainda pode ser marcado como abstrato,
como quando você não pretende que o contrato seja criado diretamente. 
Contratos abstratos são semelhantes a :ref:`interfaces`, mas uma interface é mais limitada no que pode declarar.

Um contrato abstrato é declarado usando a palavra-chave ``abstract``, como mostrado no exemplo a seguir. 
Note que este contrato precisa ser definido como abstrato, porque a função ``utterance()`` é declarada, 
mas nenhuma implementação foi fornecida (nenhum corpo de implementação ``{ }`` foi dado).

.. code-block:: solidity

    // SPDX-License-Identifier: GPL-3.0
    pragma solidity >=0.6.0 <0.9.0;

    abstract contract Feline {
        function utterance() public virtual returns (bytes32);
    }

Contratos abstratos como esse não podem ser instanciados diretamente. 
Isso também é verdade se um contrato abstrato implementar todas as funções definidas. 
O uso de um contrato abstrato como classe base é mostrado no exemplo a seguir:

.. code-block:: solidity

    // SPDX-License-Identifier: GPL-3.0
    pragma solidity >=0.6.0 <0.9.0;

    abstract contract Feline {
        function utterance() public pure virtual returns (bytes32);
    }

    contract Cat is Feline {
        function utterance() public pure override returns (bytes32) { return "miaow"; }
    }

Se um contrato herdar de um contrato abstrato e não implementa todas as funções não implementadas por meio de sobrescrita, 
ele também precisa ser marcado como abstrato.

Note que uma função sem implementação é diferente de um :ref:`Function Type <function_types>`,
embora sua sintaxe seja muito semelhante.

Exemplo de declaração de função sem implementação (uma declaração de função):

.. code-block:: solidity

    function foo(address) external returns (address);

Exemplo de declaração de uma variável cujo tipo é um tipo de função:

.. code-block:: solidity

    function(address) external returns (address) foo;


Contratos abstratos desacoplam a definição de um contrato de sua implementação,
proporcionando melhor extensibilidade, auto-documentação e facilitando padrões como o Template Method <https://en.wikipedia.org/wiki/Template_method_pattern>, 
além de remover duplicação de código. 
Contratos abstratos são úteis da mesma forma que definir métodos em uma interface é útil. 
É uma maneira do designer do contrato abstrato dizer "qualquer filho meu deve implementar este método".

.. nota::

  Contratos abstratos não podem sobrescrever uma função virtual implementada com uma função não implementada.

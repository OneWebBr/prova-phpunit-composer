# Prova para programadores PHP

O objetivo dessa prova é construir um projeto do zero com `composer` usando `PSR-4` e `PHPUnit` para testes unitários.

Os testes unitários usando PHPUnit devem validar uma determinada rota, retornando `true` ou `false`. A seguinte interface a ser seguida é:

```php

namespace App\Tests;

use PHPUnit\Framework\TestCase;

class ValidarRotaServiceTest extends TestCase 
{
    public function test_rotas_validas()
    {
        $service = new \App\ValidarRotaService();
        $this->assertTrue($service->isValida(['RS', 'RS']));
        $this->assertTrue($service->isValida(['RS', 'SC']));
        $this->assertTrue($service->isValida(['RS', 'SC', 'PR', 'SP']));
        $this->assertTrue($service->isValida(['RS', 'SC', 'RS']));
        $this->assertTrue($service->isValida(['AM', 'MT', 'GO']));
        $this->assertTrue($service->isValida(['PR', 'SC', 'RS']));
    }

    public function test_rotas_invalidas()
    {
        $service = new \App\ValidarRotaService();
        $this->assertFalse($service->isValida([]));
        $this->assertFalse($service->isValida(['RS']));
        $this->assertFalse($service->isValida(['RS', 'PR', 'SP', 'MG']));
        $this->assertFalse($service->isValida(['RS', 'SC', 'PR', 'SP', 'MS', 'MT', 'RO', 'AM', 'RR', 'TO']));
        $this->assertFalse($service->isValida(['RS', 'SC', 'PR', 'SP', 'AM', 'PA', 'MA']));
        $this->assertFalse($service->isValida(['PR', 'RS']));
    }
}
```

## Informações sobre validação de rota
A validação da rota é algo comum em sistemas de MDF-e, onde o cliente deverá informar uma rota válida do veículo entre estados.
Rotas validas são aquelas que:
- Ocorrem dentro do estado. Exemplo: `RS,RS`. Ocorre quando a origem e destino são no mesmo estado.
- Os estados devem ser vizinhos. Por exemplo, a rota `RS,SC,PR` é válida porque RS faz divisa com SC que por sua vez faz divisa com PR. A rota `RS,PR,SP` não é válida pois RS não faz divisa com PR.

## Execução dos testes

Deve ser possível executar os testes rodando `composer test`


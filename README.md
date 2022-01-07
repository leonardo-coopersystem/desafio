# Projeto de seleção Coopersystem (Angular 11+)
  
O teste consiste em criar uma mini aplicação em angular 11+ que simula um resgate personalizado de fundos de investimentos em ações.  
  
Serão avaliados:  
* Integração com api rest
* Navegação entre telas  
* Validação de formulários conforme regras de negócios  
* Padrões de codificação  
* Testes unitários
	
 
**Obs.:** Os layouts dos protótipos são só ilustrativos, podem usar os frameworks de estilo de sua preferência. (Ex.: Bootstrap)
  
### Protótipos   
[01 - Lista de investimentos](https://raw.githubusercontent.com/leonardo-coopersystem/avaliacao-coopersystem/master/prototipos-web/01%20-%20Lista%20de%20investimentos.png)   
[02 - Resgate personalizado](https://raw.githubusercontent.com/leonardo-coopersystem/avaliacao-coopersystem/master/prototipos-web/02%20-%20Resgate.png)   
[03 - Modal de confirmação](https://raw.githubusercontent.com/leonardo-coopersystem/avaliacao-coopersystem/master/prototipos-web/03%20-%20Modal%20sucesso.png)   
[04 - Modal de erro](https://raw.githubusercontent.com/leonardo-coopersystem/avaliacao-coopersystem/master/prototipos-web/04%20-%20Modal%20erro.png)   
  
  
### Fluxo de navegação  
* Lista de investimentos  
	* Executar uma chamada get no endereço [https://run.mocky.io/v3/7b2dfe42-37a3-4094-b7ce-8ee4f8012f30](https://run.mocky.io/v3/7b2dfe42-37a3-4094-b7ce-8ee4f8012f30)
	* Montar a  tela conforme o protótipo fazendo a integração com a resposta da execução do serviço acima.
	* Ao clicar em um plano que  não está em carência (indicadorCarencia = 'N'), navegar para próxima tela. 
*  Resgate personalizado  
	 * Montar a  tela conforme o protótipo usando as informações do investimento selecionado na tela anterior.
	 * Digitar os valores que deseja resgatar de cada ação e clicar em confirmar resgate
	 * Após clicar em confirmar resgate, exibir os modais de erro ou sucesso

### Regras 
* Lista de investimentos  
	* Fundos de investimentos em carência (indicadorCarencia = 'S') não pode realizar resgate, deve ficar desabilitado na lista de investimentos e não 
	permitir avançar para tela de resgate.  
  
* Resgate personalizado  
	* Realizar o cálculo do saldo da ação usando o campo percentual, que e o percentual que essa ação representa no valor total do investimento.
	* Valor a resgatar de cada ação não pode ser maior que saldo acumulado da mesma, deve ser exibido um alerta abaixo do input quando isso acontecer. 
	Ex (O valor a resgatar não pode ser maior que R$ 2.614,13) 
	* A cada interação nos inputs, deve ser atualizado o campo valor total do resgate.  
	* Colocar mascaras de moeda nos inputs de valor a resgatar, para não permitir a digitação de letras
	* Formatar campos de saldos. Ex (R$ 2.614,13)

### Cenário de teste

#### 01 - Clicar em confirmar sem preencher nenhum campo
- Clicar no investimento I
- Clicar em confirmar sem preencher nenhum valor
- **Resultado esperado:** Deve aparecer um modal pedido para o cliente preencher pelo menos um dos campos de valor a resgatar.


#### 02 - Clicar em confirmar com um dos campos a resgatar com valor invalido
- Clicar no investimento I
- Digitar um valor acima do disponível na primeira ação.

Ex: BBAS3 tem 11 mil de saldo acumulado, digitar 15 mil no campo valor a resgatar


- Digitar um valor abaixo do disponível na segunda ação.

Ex: VALE3 tem 8 mil de saldo acumulado, digitar 2 mil no campo valor a resgatar

- Clicar em confirmar

- **Resultado esperado:** Deve aparecer um modal alertando que foi digitado um ou mais valor acima do permitido, e exibir quais
ações estão com erro. [Ex: Modal de erro](https://raw.githubusercontent.com/leonardo-coopersystem/avaliacao-coopersystem/master/prototipos-web/04%20-%20Modal%20erro.png)   


#### 03 - Clicar em confirmar com todos os campos com valor validos
- Clicar no investimento I
- Digitar um valor abaixo ou igual ao disponível na primeira ação.

Ex: BBAS3 tem 11 mil de saldo acumulado, digitar 11 mil no campo valor a resgatar


- Digitar um valor abaixo ou igual ao disponível na segunda ação.

Ex: VALE3 tem 8 mil de saldo acumulado, digitar 2 mil no campo valor a resgatar

- Clicar em confirmar

- **Resultado esperado:** Deve aparecer um modal com a mensagem que o resgate foi efetuado com sucesso, e quando clicar em novo resgate, voltar para tela inicial. [Ex Modal de confirmação](https://raw.githubusercontent.com/leonardo-coopersystem/avaliacao-coopersystem/master/prototipos-web/03%20-%20Modal%20sucesso.png)


### Entrega
Enviar link do github com os testes para o email
leonardo.guedes@coopersystem.com.br

### Telefone para duvidas
61 9 8194-1274

### JSON

Caso o link do json não estiver disponível, pode usar este site para criar um novo endpoint

[https://www.mocky.io/](https://www.mocky.io/)

    {
		"response": {
			"status": "200",
			"data": {
			"listaInvestimentos": [
				{
				"nome": "INVESTIMENTO I",
				"objetivo": "Minha aposentadoria",
				"saldoTotal": 39321.29,
				"indicadorCarencia": "N",
				"acoes": [
					{
					"id": "1",
					"nome": "Banco do Brasil (BBAS3)",
					"percentual": 28.1
					},
					{
					"id": "2",
					"nome": "Vale (VALE3)",
					"percentual": 20.71
					},
					{
					"id": "3",
					"nome": "Petrobras (PETR4)",
					"percentual": 21.63
					},
					{
					"id": "4",
					"nome": "Cemig (CMIG3)",
					"percentual": 12.41
					},
					{
					"id": "5",
					"nome": "Oi (OIBR3)",
					"percentual": 17.15
					}
				]
				},
				{
				"nome": "INVESTIMENTO II",
				"objetivo": "Viajem dos sonhos",
				"saldoTotal": 7300,
				"indicadorCarencia": "N",
				"acoes": [
					{
					"id": "1",
					"nome": "Banco do Brasil (BBAS3)",
					"percentual": 35.81
					},
					{
					"id": "2",
					"nome": "Vale (VALE3)",
					"percentual": 26.42
					},
					{
					"id": "3",
					"nome": "Petrobras (PETR4)",
					"percentual": 37.77
					}
				]
				},
				{
				"nome": "INVESTIMENTO III",
				"objetivo": "Abrir meu próprio negócio",
				"saldoTotal": 26000,
				"indicadorCarencia": "N",
				"acoes": [
					{
					"id": "1",
					"nome": "Banco do Brasil (BBAS3)",
					"percentual": 41.1
					},
					{
					"id": "2",
					"nome": "Vale (VALE3)",
					"percentual": 22.43
					},
					{
					"id": "3",
					"nome": "Petrobras (PETR4)",
					"percentual": 26.12
					},
					{
					"id": "5",
					"nome": "OI (OIBR3)",
					"percentual": 10.35
					}
				]
				},
				{
				"nome": "INVESTIMENTO IV",
				"objetivo": "Investimento em carencia",
				"saldoTotal": 44000,
				"indicadorCarencia": "S",
				"acoes": [
					{
					"id": "1",
					"nome": "Banco do Brasil (BBAS3)",
					"percentual": 41.1
					},
					{
					"id": "2",
					"nome": "Vale (VALE3)",
					"percentual": 22.43
					},
					{
					"id": "3",
					"nome": "Petrobras (PETR4)",
					"percentual": 26.12
					},
					{
					"id": "5",
					"nome": "OI (OIBR3)",
					"percentual": 10.35
					}
				]
				}
			]
			}
		}
		}

### BOA SORTE! =)

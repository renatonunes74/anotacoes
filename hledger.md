[toc]

# Como usar
### Configuração para formatação brasileira
- No livro-razão:
	```
	;Irá linkar os tipos de contas
	account ativo       ; type:A
	account devendo     ; type:L
	account equidade    ; type:E
	account receita     ; type:R
	account despesa     ; type:X
	;Formatação em R$
	currency: R$ 1.000,00
	```

## Comandos úteis
### Gerais
- `-A`
	- Irá criar uma média / average dos dados

### Filtragem
- `--yearly`/`-Y`, `--monthly`/`-M`, `--daily`/`-D`
	- Filtrará os resultados por ano a ano, mes a mes, dia a dia...
- `-b 2023`
	- Filtrará por data especifica (podendo ser mais de uma (ex `-b 2023 -b 2024`))

#### Filtros mais usados
##### Filtragem de renda anual em porcentagem
```
hledger is -BtAY%
```

### Unidades
Cada compra pode possuir uma unidade, principalmente ações ou objetos

No livro-razão:
```
2023-06-02 investimento na BIGCO
	despesa:fii              2 "BIGCO" @ R$ 50
	ativo:nuinvest             
```
- Aonde foi especificado a compra de 2 ações da BIGCO por R$ 50 cada
	- @ -> valor da unidade
	- @@ -> valor no total
		- $\frac{valorTotal}{quantidade} = valorUnidade$
			- Calculado automaticamente pelo hledger

### Despesa sem data
Despesas que não tem data exata especificada mas ocorreram ou irão ocorrer

No livro-razão:
```
~2023
	(despesa:fii)              2 "BIGCO" @ R$ 50
```
No entanto isso não é automaticamente considerado no hledger, apenas quando o argumento `--budget` é passado
- Comando exemplo: `hledger bal -Yt --budget despesa`

### Orçamento previsto / Forecast budget
Orçamento previsto dado a partir de uma seleção periódica

#### Exemplo
- Salário a cada mês do ano de 2023
	- Para isso, terá de colocar no arquivo **novo** ou **mesmo arquivo** livro-razão
		```
		~ monthly from 2023
		receita:salario  R$ -2.500
		ativo:nubank
		```
	- Agora via terminal terá de usar `--forecast` para considerar o salario "gerado automaticamente"
		- Tal comando funciona no `hledger-web`, `hledger-ui` por exemplo
		- caso tenha criado um arquivo separado terá de considera-lo, usando o `-f arquivo.journal` na linha de comando
	- Comando exemplo: `hledger bal --forecast -f arquivo.journal -f livro-razão.journal` ou / e filtrar os resultados com `-YAB`

#### Quando poderia ser usado
- Despesas como ajuda de custo na alimentação de casa
- Despesas médicas / medicamentos
- Sálario

#### Links úteis
- [Minimal "forecast budget"](https://github.com/simonmichael/hledger/blob/master/examples/budgeting/forecast-budget-1.journal)

# Ferramentas complementares
- hledger-ui
	- Tui "geral" para o hledger
- hledger-iAdd
	- Tui para adicionar novos registros ao hledger
- hledger-web
	- Ferramenta gráfica que mostra os dados do hledger via navegador

# Links úteis
- [Guia básico do hledger](https://hledger.org/basics.html)
- [hledger manual - github](https://github.com/trygvis/hledger/blob/master/MANUAL.md)

## Budget
- [Links úteis para Budget](https://hledger.org/budgeting.html)
- [Orçamento e Previsão (Antigo -- 2018)](https://hledger.org/budgeting-and-forecasting.html)
- [Guia de Budget via hledger](https://github.com/plaintextaccounting/plaintextaccounting/wiki/budgeting)
- [Guia de Budget usando o estilo YNAB no hledger](https://github.com/zombor/hledger-envelope-budget)
## Plotagem
- [Plotagem do hledger via vega (hledger-vega)](https://github.com/xitian9/hledger-vega#getting-started)

## Tempo
- [timedot-vim](https://github.com/linuxcaffe/timedot-vim)
- [taskwarrior hook para timeclock do hledger](https://github.com/linuxcaffe/task-timelog-hook)

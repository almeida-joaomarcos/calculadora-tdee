# Calculadora TDEE — Java Swing

Aplicação desktop que calcula **gasto calórico diário (TDEE)**, **taxa metabólica basal (TMB)** e **macronutrientes** a partir de peso, altura, idade, sexo, nível de atividade e objetivo.

Projeto desenvolvido em **Java Swing** no Apache NetBeans, com foco em Programação Orientada a Objetos e validação de dados. É a versão original da calculadora que também ganhou uma [versão web](https://github.com/almeida-joaomarcos/tdee-web).

![Java](https://img.shields.io/badge/Java-17%2B-orange)
![Swing](https://img.shields.io/badge/UI-Java%20Swing-blue)
![NetBeans](https://img.shields.io/badge/IDE-Apache%20NetBeans-1B6AC6)
![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-green)

---

## Funcionalidades

- Cálculo da **TMB** pela equação de **Mifflin-St Jeor**, com ajuste por sexo
- **TDEE** com cinco fatores de atividade (1,2 a 1,9)
- Meta calórica para **emagrecimento (−500 kcal)**, **manutenção** ou **ganho de massa (+300 kcal)**
- Distribuição de **proteína, gordura e carboidrato** a partir de g/kg informados
- Validação de campos vazios e de valores não numéricos
- Aviso quando proteína + gordura ultrapassam a meta calórica
- Interface construída com o editor visual do NetBeans (`Nutricionista.form`)

## Como executar

### Pelo NetBeans (recomendado)

1. Abra o Apache NetBeans.
2. **File → Open Project** e selecione esta pasta.
3. Abra `src/Nutricionista.java` e pressione **Shift + F6** (Run File).

### Pela linha de comando (Ant)

```bash
ant run
```

> Requer JDK 17 ou superior. O projeto usa Ant; o `build.xml` é gerado pelo NetBeans.

## Fórmulas

**TMB — Mifflin-St Jeor**

```
Masculino:  (10 × peso) + (6,25 × altura) − (5 × idade) + 5
Feminino:   (10 × peso) + (6,25 × altura) − (5 × idade) − 161
Neutro:     (10 × peso) + (6,25 × altura) − (5 × idade) − 80
```

**TDEE**

```
TDEE = TMB × fator de atividade
```

| Nível | Fator |
| --- | --- |
| Sedentário | 1,2 |
| Levemente ativo | 1,375 |
| Moderadamente ativo | 1,55 |
| Muito ativo | 1,725 |
| Atleta | 1,9 |

**Macros**

```
Proteína (g)  = peso × g/kg   → 4 kcal/g
Gordura  (g)  = peso × g/kg   → 9 kcal/g
Carboidrato (g) = (meta − kcal de proteína e gordura) / 4
```

## Estrutura

```
calculadora-tdee-desktop/
├── src/
│   ├── Nutricionista.java   # lógica e interface
│   └── Nutricionista.form   # layout do editor do NetBeans
├── nbproject/               # configuração do projeto NetBeans
├── build.xml
└── manifest.mf
```

## Decisões técnicas

- **Mifflin-St Jeor** em vez de Harris-Benedict por apresentar melhor precisão em estudos com a população geral.
- A opção “Prefiro não informar” usa a média entre os ajustes masculino e feminino (−80), evitando exigir um dado que nem todo usuário quer fornecer.
- O cálculo de macros é feito por **g/kg de peso**, e não por percentual de calorias, porque a necessidade proteica acompanha a massa corporal.
- A interface exibe um alerta e interrompe o cálculo quando proteína + gordura já superam a meta calórica, evitando resultados impossíveis.

## Roadmap

- [x] Versão desktop em Java Swing
- [x] Versão web responsiva ([tdee-web](https://github.com/almeida-joaomarcos/tdee-web))
- [ ] Testes unitários da camada de cálculo (JUnit)
- [ ] Exportação do relatório em PDF
- [ ] Histórico de cálculos

## Aviso

Ferramenta **educativa**. Os resultados são estimativas e não substituem avaliação de nutricionista ou médico.

## Licença

MIT — veja [LICENSE](LICENSE).

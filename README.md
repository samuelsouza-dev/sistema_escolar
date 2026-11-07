<h1>
  <img src="https://cdn-icons-png.flaticon.com/512/906/906175.png" width="40" alt="">
  Sistema Para Controle Escolar
</h1>

Aplicação desktop em Java para o professor cadastrar alunos, lançar notas e faltas, consultar turmas e gerar boletins.

Projeto feito para fins acadêmicos (cadeira de Programação II).

## Funcionalidades

- **Login do professor:** o login é o nome e a senha é o CPF informados no cadastro.
- **Cadastro de alunos:** a matrícula é gerada automaticamente a partir do nome e do CPF.
- **Lançamento de notas e faltas:** por disciplina, com notas em quatro unidades.
- **Busca de turma:** lista o nome e a matrícula dos alunos de um ano e turma.
- **Boletim:** mostra as notas, a média, as faltas e a situação em cada disciplina.
- **Expulsão de aluno:** remove o aluno pela matrícula.

### Regras de aprovação

A média é calculada com as notas das quatro unidades.

| Situação | Condição |
| --- | --- |
| Rep.Falta | 20 faltas ou mais na disciplina |
| Reprovado | Média menor que 7,0 |
| Aprovado | Média igual ou maior que 7,0 |

### Opções disponíveis

- **Anos:** 1, 2 e 3
- **Turmas:** A, B, C e D
- **Disciplinas:** Português, Matemática, História, Geografia, Química, Física e Ed. Física

## Tecnologias

- <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" width="20" alt=""> Java 18
- Java Swing (interface gráfica, criada com o editor de telas do NetBeans)
- Maven

## Como executar

É necessário ter o JDK 18 ou mais recente instalado. Para usar a linha de comando, também é preciso ter o Maven.

Clone o repositório:

```bash
git clone https://github.com/samuelsouza-dev/sistema_escolar.git
```

```bash
cd sistema_escolar
```

### Pela linha de comando

Abra a interface gráfica, começando pela tela de login:

```bash
mvn compile exec:java "-Dexec.mainClass=com.mycompany.sistemaescolar.interfaceGUI.JFrameLogin"
```

> O comando `mvn compile exec:java`, sem indicar a classe, não abre a interface. Ele executa `SistemaEscolar`, uma demonstração que apenas imprime dados no console.

### Pelo NetBeans

1. Abra a pasta do projeto em **File > Open Project**.
2. Localize `JFrameLogin.java` no pacote `interfaceGUI`.
3. Clique com o botão direito no arquivo e escolha **Run File**.

## Primeiro acesso

1. Na tela de login, clique em **Cadastre-se** e cadastre um professor. Nenhum professor vem cadastrado, então faça isso antes de clicar em **Entrar**.
2. Entre usando o nome como login e o CPF como senha.
3. Use o menu principal para acessar as demais telas.

Para testar sem cadastrar alunos, use os dois que já vêm no sistema, ambos do 3º ano, turma B: `Diego Passos`, que já tem notas lançadas, e `Samuel Souza`. A busca pelo nome diferencia maiúsculas de minúsculas e exige o nome completo.

## Estrutura do projeto

```text
src/main/java/com/mycompany/sistemaescolar/
├── SistemaEscolar.java    # Demonstração no console
├── Escola.java            # Operações da escola (implementa IGestaoEscolar)
├── IGestaoEscolar.java    # Interface das operações da escola
├── Pessoa.java            # Classe base de Aluno e Professor
├── Aluno.java
├── Professor.java         # Lança notas e faltas
├── Disciplina.java        # Notas, faltas, média e situação
├── NotaException.java     # Exceção de nota inválida (ainda não utilizada)
├── bancodedados/          # Listas em memória e dados iniciais
│   ├── Alunos.java
│   └── Disciplinas.java
└── interfaceGUI/          # Telas em Swing (arquivos .java e .form)
```

## Limitações conhecidas

Por ser um projeto acadêmico, o sistema tem algumas limitações:

- **Sem persistência:** apesar do nome do pacote `bancodedados`, os dados ficam em memória e são perdidos ao fechar o programa.
- **Um único professor:** um novo cadastro substitui o anterior.
- **Segurança:** o CPF funciona como senha e é guardado em texto puro, portanto não use dados reais.
- **Validação de dados:**
  - Nome e CPF do aluno precisam ter pelo menos 3 caracteres, por causa da geração da matrícula.
  - Notas e faltas com valores não numéricos causam erro.
  - O intervalo das notas não é verificado.
- **Faltas:** cada lançamento substitui o valor anterior da disciplina, em vez de somar a ele.
- **Situação no boletim:** uma disciplina sem notas aparece como "Reprovado", pois sua média é 0.

<h2>Projeto 1º Semestre</h2>
<h4>cliente: FATEC SJC<h4>

<h2>Assistente de Estudos Athena</h2>
<img src="https://github.com/AugustoTSantos/PortifolioApis/blob/main/1Semestre/imagens/athena.jpg"/>

<br>

<h3>Visão do projeto</h3>
<p>Com o propósito de trazer para os estudantes em geral uma forma mais centralizada e organizada de cuidar da vida acadêmica e se manter atualizado em suas atividades, criamos a Athena - Assistente Pessoal de Estudos. O seu diferencial é reunir diversas ferramentas úteis em um único lugar e interatividade por voz.</p>

<br>

## 👩‍💼 O que a Athena pode fazer por você?
 
Abaixo estão listadas as funcionalidades oferecidas, com uma breve descrição de cada:

- Cronograma de aulas:
  armazena horários de aulas cadastrados pelo(a) estudante, para facilitar controle e organização de sua agenda;
  
- Calendário acadêmico:
  permite cadastro de datas de provas, trabalhos e qualquer ocasião importante para o estudante, com notificações prévias;
  
- Planos de estudos:
  a Athena fornece planos de estudos editáveis, de acordo com a meta do estudante;
  
- Notificações de estudos:
  alertas lembrando o(a) estudante que chegou a hora de estudar (via pop-up e e-mail);

- Cálculo de médias:
  permite o(a) estudante conferir de forma fácil como estão indo suas notas no semestre;
  
- Controle de faltas:
  para evitar uma reprovação, alerta o(a) estudante sobre quantas faltas ainda podem ser registradas (com contagem regressiva, de acordo com valor previamente cadastrado pelo(a) estudante);
  
- Dicas:
  dicas sobre como melhorar a efetividade dos estudos, concentração, absorção de conteúdo e organização;
  
- Metas de estudos e gráficos de desempenho:
  planejamento de horas a estudar semanal ou mensal, que auxilia no progresso, juntamente com visualização do desempenho através de gráficos.
<br>

<h3>Tecnologias Utilizadas</h3>

<details>
    <summary>Back</summary>
    <br>
    
- [Python](https://www.python.org/)
- [Pydub](https://github.com/jiaaro/pydub)
- [tkinter](https://docs.python.org/3/library/tkinter.html)
- [SpeechRecognition](https://pypi.org/project/SpeechRecognition/)
- [PyAudio](https://pypi.org/project/PyAudio/)
- [pyttsx3](https://pypi.org/project/pyttsx3/)
- [email.mime](https://docs.python.org/pt-br/3.7/library/email.mime.html)
- [gTTS](https://pypi.org/project/gTTS/)
- [playsound](https://pypi.org/project/playsound/)
</details>

<details>
    <summary>Banco</summary>
    <br>

- [SQLite](https://www.sqlite.org/index.html)
</details>

<details>
    <summary>Outras</summary>
    <br>

- [GitHub](https://github.com/)
- [Git](https://github.com/)
- [Discord](https://discord.com/)
</details>

<br>

<h2>Minhas Contribuições</h2>
<details>
<summary>Classe de Horarios</summary>

Muitas funções da Athena precisa de uma data para funcionarem, em questão tecnica fiquei encarregado dessa classe pois era meu primeiro contato com programação e englobava o que vimos durante o semestre.

```
import sqlite3
from sqlite3 import Error
def conexaobanco():
    caminho ="C:\\Users\\Famil\\OneDrive\\Área de Trabalho\\Fatec - 1 semestre\\banquinho\\Banco_Athena.db"
    con = None
    try:
        con = sqlite3.connect(caminho)
    except Error as ex:
        print(ex)
    return con

vcon = conexaobanco()
def inserir(conexao,sql):                 
    try:
        c = conexao.cursor()
        c.execute(sql)
        conexao.commit()  
        print('registro inserido')
    except Error as ex:
        print(ex)


semana = ["segunda", "terça", "quarta", "quinta", "sexta", "sabado"]
materias = []
dias_semana = []
horario_materia = []

try:
    while True:
        semana_dia = (str(input('dia da semana: ')).strip().split()[0].lower())
        if semana_dia not in semana:
            print(semana_dia)
            print("Parece que você digitou algo invalido, tente novamente !")
            continue
        if semana_dia != "sabado":
            x = semana_dia + "-feira"
            dias_semana.append(x)
        else:
            dias_semana.append(semana_dia)
        resp = str(input(f'Gostaria de cadastrar um novo dia da semana ? '
                            f'[SIM/NAO] : ')).upper().strip()[0]
        if resp == "S":
            continue
        if resp == "N":
            break
    print(dias_semana)
except ValueError:
    print('Valor digitado inválido, tente novamente !')
for posi, c in enumerate(dias_semana):
    while True:
        try:
            materia = input(f'Qual matéria gostaria de cadastrar para "{dias_semana[posi]}" ?: ').strip().lower()
            materias.append(materia)
            resp = str(input(f'Gostaria de cadastrar uma nova matéria para "{dias_semana[posi]}" ?: '
                                f'[SIM/NAO] : ')).upper().strip()[0]
            if resp == "S":
                continue
            if resp == "N":
                for pos, c in enumerate(materias):
                    horario_inicial = input(
                        f'Quando começa a aula da matéria: "{materias[pos]}" (hh:mm) ?: ').strip().replace(" ", ":")
                    horario_final = input(
                        f'Quando termina a aula da matéria: "{materias[pos]}" (hh:mm) ?: ').strip().replace(" ",
                                                                                                            ":")
                    horario_materia.append(f"{horario_inicial}-{horario_final}")
                    try:
                        with open("aulas.txt", "a") as arquivo:
                            arquivo.write(f'Dia: {dias_semana[posi]} '
                                            f'Aulas: {materias[pos]} = horario: {horario_materia[pos]} \n')
                            vsql = "INSERT INTO Horarios_ (DIASEMANA,MATERIA, HORARIO)VALUES('"+dias_semana[posi]+"','"+materias[pos]+"','"+horario_materia[pos]+"')"
                        inserir(vcon, vsql)
                    except Exception as error:
                        print('>> Arquivo não encontrado, tente novamente !')
                        print(error)
                materias.clear()
                break
        except Exception as error:
            print('>> Encontramos algum erro, por gentileza tente novamente')
            print(error)
        break
```

</details>
<br>
<details>
<summary>Backlog</summary>

Atuei como Scrum Master em parte do projeto, como no primeiro semestre o master e o PO eram o mesmo papel acabei também fazendo o backlog.

<img src="https://github.com/AugustoTSantos/PortifolioApis/blob/main/1Semestre/imagens/Screenshot_2.png">

</details>

<br>

<details>
<summary>Apresentação</summary>

Devido a pandemia a feira de solução foi feita pelo youtube, gravei e editei nossa <a>[Apresentação Final](https://www.youtube.com/watch?v=E_I9MvQs9BE)</a>, espero que gostem.

</details>

<br>

<h3>Aprendizados Efetivos</h3>

<h3 align="center"> Hard Skills </h3>

<table align="center">
    <tr>
      <th width="300px">Aprendizado</th>
      <th width="300px">Classificação</th>
    </tr>
    <tr>
      <td>Syntaxe Python</td>
      <td>sei fazer com consulta</td>
    </tr>
    <tr>
      <td>if</td>
      <td>sei fazer</td>
    </tr>
    <tr>
      <td>for</td>
      <td>sei fazer</td>
    </tr>
     <tr>
      <td>while</td>
      <td>sei fazer</td>
    </tr>
    <tr>
      <td>Array</td>
      <td>sei fazer com consulta</td>
    </tr>
    <tr>
      <td>Lista</td>
      <td>sei fazer</td>
    </tr>
</table>

<h3 align="center"> Soft Skills </h3>

<table align="center">
    <tr>
      <th width="300px">Habilidade</th>
      <th width="300px">Descrição</th>
    </tr>
    <tr>
      <td>Comunicação</td>
      <td>Precisei me comunicar com a equipe sobre situações e status de tarefas e com cliente sobre o produto.</td>
    </tr>
    <tr>
      <td>Resolução de Problemas</td>
      <td>Precisei entender e buscar formas de resolver problemas encontrados durante o projeto.</td>
    </tr>
    <tr>
      <td>Trabalho em Equipe</td>
      <td>Precisei entender e adaptar a forma de trabalho para colaborar com a equipe no desenvolimento do projeto.</td>
    </tr>
    <tr>
      <td>Gerir Reunião</td>
      <td>Como master era responsavel por organizar e gerir as reuniões da equipe.</td>
    </tr>
</table>

<br>

<h2>Sumário</h2>

* [Pagina Principal](https://github.com/AugustoTSantos/PortifolioApis/blob/main/README.md)
* [Projeto 2º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/2Semestre)
* [Projeto 3º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/3Semestre)
* [Projeto 4º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/4Semestre)
* [Projeto 5º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/5Semestre)
* [Projeto 6º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/6Semestre)

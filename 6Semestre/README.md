<h2>Projeto 6º Semestre</h2>
<h4>Cliente: Imagem</h4>

[repositório](https://github.com/GroupHextech/HEXTECH-API6sem)

<h2>HexAnalytics</h2>

<h3>Visão do projeto</h3>

<p>Em um mercado cada vez mais competitivo, entender as nuances dos desejos dos clientes torna-se crucial para o sucesso. Avaliações online, nesse contexto, representam um verdadeiro tesouro de insights, revelando a satisfação dos consumidores, suas expectativas e, às vezes, suas frustrações. Diante desse cenário, o desafio deste semestre é o desenvolvimento de um aplicativo inovador que, utilizando inteligência artificial, realize uma análise aprofundada desses comentários, classificando-os como positivos, neutros ou negativos. Ao integrar esses dados no banco de dados, será possível extrair insights valiosos que impulsionarão a tomada de decisões estratégicas e melhorarão a experiência do cliente.</p>

<p align="center">
  <img src="https://github.com/GroupHextech/HEXTECH-API6sem/blob/main/docs/images/Sprint4.gif" width="600">
</p>

<h3>Tecnologias Utilizadas</h3>

<details>
<summary>Front-End</summary>

* [React](https://pt-br.legacy.reactjs.org/)
* [HTML](https://www.w3schools.com/html/)
* [CSS](https://www.w3schools.com/css/)

</details>

<details>
<summary>Back-End</summary>

- [Python](https://www.python.org/)
- [Flask](https://flask.palletsprojects.com/en/3.0.x/)
- [Jupyter](https://jupyter.org/)
- [XGBoost](https://xgboost.readthedocs.io/en/stable/)
</details>

<details>
<summary>Database</summary>

- [MongoDB](https://www.mongodb.com/atlas)
- [Firebase](https://firebase.google.com/?hl=pt-br)
</details>

<details>
<summary>Meetings and Communication</summary>

- [Discord](https://discord.com/?msclkid=b4f5af84b8f811ecbd81c127a0ae68a7)
- [Whatsapp](https://www.whatsapp.com/)
- [Slack](https://slack.com/intl/pt-br/?msclkid=c00e628eb8f811ecaef374bb86d7f056)
</details>


<details>
    <summary>Outras</summary>
    <br>

- [GitHub](https://github.com/)
- [Git](https://github.com/)
</details>

<br>


<h2>Minhas Contribuições</h2>
<br>

<details>
    <summary>Tratamento de Dados</summary>
    <p>Para treinar um modelo de aprendizagem de maquina é preciso preparar o dado, ajudei a fazer os passos pelo qual a base de treino passa.</p>
    
```
  # Cria uma nova coluna para classificar entre comentários positivos(2), negativos(0) ou neutros(1) com base na nota:
dataset['feeling'] = np.where(dataset['overall_rating'] < 3, 0, np.where(dataset['overall_rating'] == 3, 1, 2))

# Mostra os primeiros registros do dataset
print("Primeiros registros do dataset:")
print(tabulate(dataset.head(10), headers='keys', tablefmt='pipe'))

# Criação da instância do lematizador e das stopwords
lemmatizer = WordNetLemmatizer()
stop_words = set(stopwords.words('portuguese'))

# Lista para armazenar os textos pré-processados
preprocessed_texts = []

# Itera sobre cada texto no dataset para pré-processamento
for text in dataset['review_text']:
    # Verifica se o texto é uma string
    if isinstance(text, str):
        # Converte para minúsculas
        text = text.lower()
        # Remove acentos
        text = ''.join(char for char in unicodedata.normalize('NFKD', text) if unicodedata.category(char) != 'Mn')
        # Remove números usando expressão regular
        text = re.sub(r'\d+', '', text)
        # Remove caracteres especiais (incluindo emojis)
        text = re.sub(r'[^\w\s]', '', text)
        # Remove pontuação
        text = text.translate(str.maketrans('', '', string.punctuation))
        # Remove espaços extras
        text = re.sub(r'\s+', ' ', text).strip()
        # Tokenização
        tokens = word_tokenize(text)
        # Lematização e remoção de stopwords
        tokens = [lemmatizer.lemmatize(word) for word in tokens if word.isalpha() and word.lower() not in stop_words]
        # Junta os tokens em texto novamente
        preprocessed_text = ' '.join(tokens)
        # Adiciona o texto pré-processado à lista
        preprocessed_texts.append(preprocessed_text)
    else:
        preprocessed_texts.append("")

# Substitui os textos originais pelos textos já preparados para análise
dataset['review_text'] = preprocessed_texts
```  
</details>

<details>
    <summary>Modelo XGBoost</summary>
    <p>O maior foco do projeto é a aprendizagem de maquina em analise de sentimentos, a equipe pesquisou e testou varios modelos e eu fiquei responsável pelo XGBoost, que acabou sendo usando na versão final.</p>
    
```
# Cria uma instância do modelo XGBoost
xgboost = xgb.XGBClassifier()

# Especifica o número de folds para a validação cruzada
num_folds = 5

#  Cria um objeto StratifiedKFold para garantir que as classes estejam balanceadas em cada divisão
kfold = StratifiedKFold(n_splits=num_folds, shuffle=True, random_state=42)

# Lista para armazenar as pontuações de acurácia de cada divisão (fold)
accuracy_scores = []

# Realiza a validação cruzada
for train_index, test_index in kfold.split(X_ngrams, Y):
    # Separa os dados em conjuntos de treino e teste para esta divisão
    X_train, X_test = X_ngrams[train_index], X_ngrams[test_index]
    Y_train, Y_test = Y[train_index], Y[test_index]

    # Calcula os pesos de amostra com base nas classes
    class_weights = np.zeros(len(Y_train))
    class_counts = np.bincount(Y_train)
    for i in range(len(class_counts)):
        class_weights[Y_train == i] = len(Y_train) / class_counts[i]
    
    # Treina o modelo XGBoost com pesos de amostra
    xgboost.fit(X_train, Y_train, sample_weight=class_weights)
```
</details>

<details>
    <summary>Projeto Mongo</summary>
    <p>Nesse semestre fomos introduzidos a bancos de dados não relacionais, eu fiquei encarregado de criar o projeto no Mongo Atlas e a pagina da wiki de como começar a usar a ferramenta.</p>
    
* [Wiki Mongo projeto](https://github.com/GroupHextech/HEXTECH-API6sem/wiki/Mongo)
    
</details>

<details>
    <summary>Conexão Back-Firebase</summary>
    <p>Fui responsável pela primeira versão da conexão com firebase e a aplicação, onde ele buscava as credenciais localmente e conectava com o cliente.</p>
    
```
    cred = credentials.Certificate(
        os.path.join(
            os.path.dirname(__file__),
            r"D:\\Codigos\\Fatec\\api6\\firebase\\hex-imagem-firebase-adminsdk-us6mv-b020efced9.json"
        )
    )

    firebase_app = firebase_admin.initialize_app(cred)

    def init_firestore():
        fclient = firestore.client(app=firebase_app)
        return fclient

    fbd = firestore.client()
```
</details>

<br>
<h2>Aprendizados Efetivos</h2>

<h3 align="center"> Hard Skills </h3>

<table align="center">
    <tr>
      <th width="300px">Aprendizado</th>
      <th width="300px">Classificação</th>
    </tr>
    <tr>
      <td>Estrutura Flask</td>
      <td>sei fazer</td>
    </tr>
    <tr>
      <td>Analise de Sentimentos</td>
      <td>sei fazer com consulta</td>
    </tr>
    <tr>
      <td>MongoDB</td>
      <td>sei fazer com consulta</td>
    </tr>
     <tr>
      <td>NOSql</td>
      <td>sei fazer com consulta</td>
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
      <td>Precisei me comunicar com a equipe sobre situações e status de tarefas.</td>
    </tr>
    <tr>
      <td>Resolução de Problemas</td>
      <td>Precisei entender e buscar formas de resolver problemas encontrados durante o projeto.</td>
    </tr>
    <tr>
      <td>Trabalho em Equipe</td>
      <td>Precisei entender e adaptar a forma de trabalho para colaborar com a equipe no desenvolimento do projeto.</td>
    </tr>
</table>


<br>

<h2>Sumário</h2>

* [Projeto 1º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/1Semestre)
* [Projeto 2º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/2Semestre)
* [Projeto 3º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/3Semestre)
* [Projeto 4º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/4Semestre)
* [Projeto 5º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/5Semestre)
* [Pagina Principal](https://github.com/AugustoTSantos/PortifolioApis/blob/main/README.md)

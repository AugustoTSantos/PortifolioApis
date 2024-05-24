<h2>Projeto 5º Semestre</h2>
<h4>Cliente: Oracle</h4>

<h2>Hextaurant</h2>

<h3>Visão do projeto</h3>

<p>Criamos uma plataforma online que permite aos proprietários de restaurantes gerenciar suas operações de forma eficiente e intuitiva. O objetivo é construir um sistema abrangente que ofereça recursos como painéis, gráficos, relatórios e funcionalidades para gerenciamento de pessoal, fornecedores e suprimentos.</p>

<br>

<p align="center">
  <img src="https://github.com/GroupHextech/HEXTECH-API5sem/blob/main/doc/Mockup/Project%20in%20Operation/ProjectOperationSprint4.gif" width="">
</p>

<br>

<h3>Tecnologias Utilizadas</h3>

<details>
<summary>Front-End</summary>

* [vue](https://vuejs.org/)
* [HTML](https://www.w3schools.com/css/)
* [CSS](https://www.w3schools.com/css/)

</details>

<details>
<summary>Back-End</summary>

- [Java](https://www.java.com/pt-BR/?msclkid=7faa842eb8f811ecab39772d4c1ae90b)

- [Spring boot](https://spring.io/projects/spring-boot)

</details>

<details>
<summary>Database</summary>

- [Oracle Autonomous Database](https://www.oracle.com/autonomous-database/)
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
- [Discord](https://discord.com/)
</details>

<br>


<h2>Minhas Contribuições</h2>
<br>

<details>
    <summary>Mapeamento bd</summary>
Contribui com a estrutura do nosso banco, com a padronização de nomes e sugestões para organização das tabelas.

<p align="center">
      <img src="https://github.com/AugustoTSantos/PortifolioApis/blob/main/5Semestre/imagens/logico_4sp.png" width="100%" height="100%">
</p>

</details>

<details>
    <summary>Estrutura Back-End</summary>
Nosso back-end foi feito em java spring boot e fiqeu responsavel pela estrutura e desenvolvimento.

<p align="center">
      <img src="https://github.com/AugustoTSantos/PortifolioApis/blob/main/5Semestre/imagens/estrutura.png" width="100%" height="100%">
</p>

</details>

<details>
    <summary>Deploy Back-End</summary>
Nesse semestre aprendememos e implementamos técnicas de devops, uma das minhas implementações foi o deploy abaixo feito com git actions, onde toda vez que pull era feito para branch main ele garantia que não havia erros e buildava a nova versão em um servidor web.

```
name: Deploy
on:
  pull_request:
    branches:
      - main
    types: [closed]
jobs:
  build:
    name: Build
    if: ${{ github.event.pull_request.merged }}
    runs-on: ubuntu-latest
    steps: 
    - name: Checkout code
      uses: actions/checkout@v2

    - name: SSH and Deploy
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.SSH_HOST }}
        username: ${{ secrets.SSH_USER }}
        key: ${{ secrets.SSH_KEY }}
        script: |
          cd /home/opc
          sh start_app.sh 
          cd /home/opc/api5-backend/cloudKitchen
          git checkout main
          git pull origin main
          mvn clean package
          cd target
          nohup java -jar cloudKitchen-0.0.1-SNAPSHOT.jar > application.log 2>&1 &
```

</details>

<details>
    <summary>Conexão Back com Banco</summary>
Nosso oracle estava hospedado na oracle cloud, então alguns passos precisam ser tomados para sua utilização na aplicação.

1 - baixar wallet

2 - escrever conexão
```
spring.datasource.driver-class-name=oracle.jdbc.OracleDriver
spring.datasource.url=jdbc:oracle:thin:@dcn3qawhewq5s68p_high?TNS_ADMIN=./wallet
spring.datasource.username=ADMIN
spring.datasource.password=Hextechapi5bd
spring.jpa.database-platform=org.hibernate.dialect.Oracle12cDialect

##Logging properties for UCP
#logging.level.root=trace
#logging.file.name=logs.log
#logging.level.oracle.ucp=trace
server.port = 8080

##Hibernate ddl auto (create, create-drop, validate, update)
spring.jpa.hibernate.ddl-auto = validate
```

</details>

<br>

<h2>Aprendizados Efetivos</h2>

* Conexão Oracle Cloud + Spring boot
* Deploy
* CI
* Versionamento de Branch
* Rastramento de Issues

<br>

<h2>Sumário</h2>

* [Projeto 1º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/1Semestre)
* [Projeto 2º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/2Semestre)
* [Projeto 3º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/3Semestre)
* [Projeto 4º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/4Semestre)
* [Pagina Principal](https://github.com/AugustoTSantos/PortifolioApis/blob/main/README.md)
* [Projeto 6º Semestre](https://github.com/AugustoTSantos/PortifolioApis/tree/main/6Semestre)

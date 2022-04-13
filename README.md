# how-projeto-v1
Ingestão e Transformação de Dados
Sobre:
A proposta era criar um serviço dentro da AWS que recebesse um arquivo .csv, ingerido através de código python ou via Pentaho que já gera o arquivo csv automaticamente através de Jobs e envia ao Bucket, todas as etapas seguem um fluxo automatizado, até o envio do e-mail indicando que a atividade do ETL foi finalizada e enviada ao bucket processado.

Overview da Estrutura

![image](https://user-images.githubusercontent.com/4244680/163167746-d4f35e84-6fe1-4a5b-85ca-11048bf50438.png)


Recursos utilizados

*Visual Studio Code
*PentahoPDI
*AWS S3
*Função Lambda
*AWS Glue - Crawler
*Amazon CloudWatch
*Job ETL 
*Amazon SNS

Fluxo do Trabalho

          Após o envio do arquivo de dados ao Bucket RAW (Dados Brutos), estes são  catalogados através do AWS Glue, neste caso foi criado uma função lambda (Amazon S3 trigger) para que inicie o  Crawler e catalogue os dados. Assim que o Crawler finalizar as definições da tabela uma segunda função lambda usando o  CloudWatch Events rule que inicia uma job no AWS Glue ETL para processar e em seguida enviar os dados para o Bucket processado, neste caso somente fiz a conversão do arquivo para o formato parquet no momento. Finalizando a job do ETL uma notificação é enviada por e-mail avisando sobre o sucesso da conversão, para isto foi configurado outra regra no CloudWatch que usa o serviço SNS ( Simple Notification Service) para realizar este envio. Abaixo segue telas que ilustram a execução, como projeto/melhoria futura farei outros tipos de conversão em outros projetos, e assim distribuir os dados em outros buckets afim de refinar ainda mais, além de disponibilizar este dados em ferramentas de visualização.

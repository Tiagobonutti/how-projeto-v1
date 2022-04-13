<h2>how-projeto-v1</h2>
<h1>Ingest&atilde;o e Transforma&ccedil;&atilde;o de Dados</h1>
Sobre:

A proposta era criar um servi&ccedil;o dentro da AWS que recebesse um arquivo .csv, ingerido atrav&eacute;s de c&oacute;digo python ou via
Pentaho que j&aacute; 
gera o arquivo csv automaticamente atrav&eacute;s de Jobs e envia ao Bucket, todas as etapas seguem um fluxo automatizado, at&eacute; o envio do e-mail indicando que a atividade do ETL foi finalizada e enviada ao bucket processado.

Overview da Estrutura
![image](https://user-images.githubusercontent.com/4244680/163167746-d4f35e84-6fe1-4a5b-85ca-11048bf50438.png)

<h0>Recursos utilizados</h0>
<br>*Visual Studio Code
<br>*PentahoPDI
<br>*AWS S3
<br>*Função Lambda
<br>*AWS Glue - Crawler
<br>*Amazon CloudWatch
<br>*Job ETL 
<br>*Amazon SNS</br>

<h0>Fluxo do Trabalho</h0>

Após o envio do arquivo de dados ao Bucket RAW (Dados Brutos), estes são  catalogados através do AWS Glue, neste caso foi criado uma função lambda (Amazon S3 trigger) para que inicie o  Crawler e catalogue os dados. Assim que o Crawler finalizar as definições da tabela uma segunda função lambda usando o  CloudWatch Events Rule inicia uma job no AWS Glue ETL para processar e em seguida enviar os dados para o Bucket processado, neste caso somente fiz a conversão do arquivo para o formato parquet no momento. Finalizando a job do ETL uma notificação é enviada por e-mail avisando sobre o sucesso da conversão, para isto foi configurado outra regra no CloudWatch que usa o serviço SNS (Simple Notification Service) para realizar este envio. Abaixo segue telas que ilustram a execução, como projeto/melhoria futura farei outros tipos de conversão em outros projetos, e assim distribuir os dados em outros buckets afim de refinar ainda mais, além de disponibilizar este dados em ferramentas de visualização.

<h0>S3 – RAW e Processado<h0>
![image](https://user-images.githubusercontent.com/4244680/163172939-59e6f995-9f53-4270-9378-e06bdaed0a61.png)

<h0>Eventos</h0>
![image](https://user-images.githubusercontent.com/4244680/163178173-7e5d9231-799a-4ee9-9ea0-838d91adc1aa.png)
![image](https://user-images.githubusercontent.com/4244680/163179366-8650bc1b-417d-4cc5-9a66-af727a9ff5fb.png)

<h0>Data Catalog com um crawler do AWS Glue</h0>
![image](https://user-images.githubusercontent.com/4244680/163179466-3722cb95-84f2-4fe0-a6a9-f0f56ac19602.png)
          
![image](https://user-images.githubusercontent.com/4244680/163179592-687a9f34-5edd-4f4f-abc3-5336aa7453b2.png)
![image](https://user-images.githubusercontent.com/4244680/163179840-52eb91bf-049b-4448-a943-9742ac53279a.png)

         
<h0>ETL com o AWS Glue</h0>
![image](https://user-images.githubusercontent.com/4244680/163179958-2dc40fee-7b89-4140-b6d2-bf2f23c1acaf.png)
![image](https://user-images.githubusercontent.com/4244680/163179981-30fe5ba1-c4d7-40fe-919f-23cb46040f3f.png)

<h0>Monitoramento e notificação com eventos do Amazon CloudWatch</h0>
![image](https://user-images.githubusercontent.com/4244680/163180141-d5b616a2-7902-44ae-aed2-31eefe3c7100.png)
![image](https://user-images.githubusercontent.com/4244680/163180683-8c0713d7-fcb9-4f91-b8a9-3511879a9de2.png)
          
<h0>Transformação concluída com sucesso, e notificação recebida.</h0>
![image](https://user-images.githubusercontent.com/4244680/163180786-b9b63632-14e7-49f4-b494-15503d31be92.png)

        

          





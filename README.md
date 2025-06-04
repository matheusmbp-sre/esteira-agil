# esteira-agil


Objetivo:

Criar alertas automáticos com CloudFormation para monitorar EC2, RDS, Lambda, S3  e outros serviços cores de forma rápida, padronizada e eficiente.

Fluxo Esteira:
- User: Seleciona Script
- CloudFormation: Executa Stack YML
- CloudWatch: Coleta e analisa métricas
- SNS: Envia Notificações



![image](https://github.com/user-attachments/assets/b748c58a-1deb-4995-9c59-daddf6d7cd63)

--------------------------------------------------------------------------------------------------------------------------------------------------------------

Configuração:

Obs: O exemplo abaixo é apenas para EC2, mas contempla para todos os serviços, mesmo procedimento.

1. Criar uma policy no IAM com as devidas permissões abaixo:

Nome: EC2-Monitoring-Stack-Policy

```{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "VisualEditor0",
"Effect": "Allow",
"Action": [
"lambda:CreateFunction",
"ec2:DescribeInstances",
"events:EnableRule",
"sns:DeleteTopic",
"events:PutRule",
"sns:Unsubscribe",
"iam:CreateRole",
"iam:PutRolePolicy",
"logs:CreateLogStream",
"iam:PassRole",
"sns:Publish",
"iam:DeleteRolePolicy",
"sns:Subscribe",
"sns:ConfirmSubscription",
"events:RemoveTargets",
"events:DisableRule",
"iam:GetRole",
"events:DescribeRule",
"sns:GetTopicAttributes",
"lambda:GetFunction",
"sns:CreateTopic",
"iam:DeleteRole",
"logs:CreateLogGroup",
"logs:PutLogEvents",
"events:PutTargets",
"events:DeleteRule",
"cloudwatch:PutMetricAlarm",
"sns:SetSubscriptionAttributes",
"lambda:AddPermission",
"lambda:RemovePermission"
],
"Resource": "*"
}
]
}
  
```
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2 - Criar uma role assumindo o serviço CloudFormation e linkar a politíca acima:

Nome: EC2-Monitoring-Stack-Role

```

{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "",
"Effect": "Allow",
"Principal": {
"Service": "cloudformation.amazonaws.com"
},
"Action": "sts:AssumeRole"
}
]
}
```
![image](https://github.com/user-attachments/assets/df6b8b3f-c920-4779-89ed-611ec3c8a6df)

![image-1](https://github.com/user-attachments/assets/31864d4a-bd90-4c32-b74f-686f0e4e11b2)

____________________________________________________________________________________________________________________________________________________________________________________________

3 - Copie o arquivo ec2-monitor-lambda-template-geral.yaml que está presente neste repo.

Obs: Usaremos esse arquivo para desmonstrar, mas poderia ser qualquer outro.

____________________________________________________________________________________________________________________________________________________________________________________________

4 - Criar uma stack no cloudformation > Choose an existing template > Upload a template file > Choose file

Obs: Clonem o repositório, para ter os arquivos localmente, ou façam a integração do github com AWS e usem a opção (Sync from Git)

![image-7](https://github.com/user-attachments/assets/de594f19-546b-42bb-b64e-4a8805bdcb97)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

5 - Selecione o arquivo na sua máquina criado no passo anterior.

![image-9](https://github.com/user-attachments/assets/7eafd73a-fdf2-451c-a469-74820afb441d)

_____________________________________________________________________________________________________________________________________________________________________________________________

6 - Na próxima página coloque o nome EC2-Monitoring-Stack.

Parameters:

CpuUtilizationThreshold : 80
SnsNotificationEmail : email de notificação
StatusCheckFailedThreshold : 1

![image-2](https://github.com/user-attachments/assets/0e478c15-ac6e-4d2b-9511-3d6cd0393064)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

7 - Na próxima página em Permissions, selecione a role do IAM com nome de EC2-Monitoring-Stack-Role

![image-3](https://github.com/user-attachments/assets/beb17322-08b2-4436-8ea8-9ac476d8dc13)

_____________________________________________________________________________________________________________________________________________________________________________________________


8 - Ainda na mesma página role até o final e selecione a caixa de Capabilities e clique em next.

![image-4](https://github.com/user-attachments/assets/d5db45f3-39f5-458c-978d-de4e0beb2037)


______________________________________________________________________________________________________________________________________________________________________________________________



9 - Na próxima página role até o final e clique em submit para criar a stack.


![image-5](https://github.com/user-attachments/assets/08ab8564-b6b6-4def-aed0-d497db8c5539)

______________________________________________________________________________________________________________________________________________________________________________________________


 10 - Um e-mail da AWS será enviado para aceite de subscribe, após aceitar aguarde de 10 a 15 minutos e valide no cloudwatch os alarmes criados:


![image-6](https://github.com/user-attachments/assets/4087c5ff-4a6a-419f-b01d-78a99a518132)

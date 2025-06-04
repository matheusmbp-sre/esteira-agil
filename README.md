# esteira-agil


Objetivo:

Criar alertas automáticos com CloudFormation para monitorar EC2, RDS, Lambda, S3  e outros serviços cores de forma rápida, padronizada e eficiente.
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

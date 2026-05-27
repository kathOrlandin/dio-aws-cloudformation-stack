# 🛠️ Implementando sua Primeira Stack com AWS CloudFormation

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white)
![IaC](https://img.shields.io/badge/IaC-Infra_as_Code-blue?style=for-the-badge)

Este repositório foi desenvolvido para o laboratório prático da **Digital Innovation One (DIO)**. O objetivo principal é consolidar os conceitos de **Infraestrutura como Código (IaC)** através da criação e execução de templates de automação utilizando o **AWS CloudFormation**.

---

## 🎯 Cenário e Objetivos do Desafio
* Compreender as vantagens de automatizar o provisionamento de recursos em nuvem em vez da criação manual.
* Desenvolver um template declarativo em formato **YAML** para a criação de uma Stack.
* Simular o provisionamento de uma instância Amazon EC2 integrada com regras básicas de segurança (Security Group).

---

## 📄 Código do Template de Infraestrutura (YAML)

Abaixo está o arquivo de configuração estruturado que descreve os recursos da nossa infraestrutura. Esse arquivo é enviado ao CloudFormation para que a AWS monte a infraestrutura de forma 100% automatizada:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'Primeira Stack CloudFormation - Provisionamento de EC2 automatizado - Lab DIO'

Resources:
  ServidorWebInstancia:
    Type: 'AWS::EC2::Instance'
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0c55b159cbfafe1f0  # ID padrão de referência para Amazon Linux
      SecurityGroups:
        - !Ref ServidorSecurityGroup
      Tags:
        - Key: Name
          Value: Servidor-Automatizado-CloudFormation

  ServidorSecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupDescription: 'Liberar portas padrao para o Servidor Web'
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0

Outputs:
  InstanciaID:
    Description: 'ID da Instancia EC2 que foi criada automaticamente'
    Value: !Ref ServidorWebInstancia
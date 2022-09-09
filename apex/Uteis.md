# Vários códigos úteis 

## Pegar o link da ORG

```bash
URL.getSalesforceBaseUrl().toExternalForm() + '/resto do link'
```

## Pegar o tipo de registro

Por nome de API
```bash
Schema.SObjectType. Objeto .getRecordTypeInfosByDeveloperName()
.get('Nome')
.getRecordTypeId();
```

## Acessar objetos

Por notação de ponto
```bash
Account Conta = [SELECT id,Name FROM Account LIMIT 1];
Conta.Name;
```

Por Get
```bash
Account Conta = [SELECT id,Name FROM Account LIMIT 1];
String campo = 'Name';
Conta.get(campo);
```
## Descobrir o tipo de um objeto

Usando o ID dele
```bash
ID idObjeto = (ID de algum registro);
String Objeto = '' + idObjeto.getsobjecttype();
```
Exemplo: Se o idObjeto tem o ID de um Lead, a variável Objeto vai ser "Lead"

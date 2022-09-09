# O que faz o codigo ?
Uma classe em batch processa uma lista de objetos em lote, o padrão de um batch é 200 objetos por vez


## Codigo
Modelo de uma classe batch padrão

```bash
global class ExemploBatch implements Database.Batchable<sObject> {
 
   global System.Iterable<sObject> start(Database.BatchableContext BC) {
       return objeto iteravel;
   }
 
   global void execute(Database.BatchableContext BC, List<sObject> scope) {
       //executa
    }
    
    
   global void finish(Database.BatchableContext BC) {
       //processo no final do batch
   }
}
```
## Chamar um batch
Ao chamar o batch, você pode opcionalmente passar o tamanho do lote para ser processado por vez, nesse caso 10.
```bash
Database.executeBatch(new ExemploBatch(),10);
```

## Passar parâmetros para o batchable
Você pode passar parâmetros através de um método construtor
OBS: O método construtor tem o mesmo nome da classe
Exemplo:
```bash
global class ExemploBatch implements Database.Batchable<sObject> {
  String nomeAntigo;
  String nomeNovo;
  
  public ExemploBatch(String nomeAntigo, String nomeNovo){
        this.nomeAntigo = nomeAntigo;
        this.nomeNovo = nomeNovo;
    }
 
   global System.Iterable<sObject> start(Database.BatchableContext BC) {
       return [SELECT id FROM Account WHERE FirstName = :nomeAntigo];
   }
 
   global void execute(Database.BatchableContext BC, List<Account> scope) {
       List<Account> contas = new List<Account>();
       For(Account c: scope){
          c.FirstName = nomeNovo;
          contas.add(c)
       }
       update c;
    }
    
    
   global void finish(Database.BatchableContext BC) {
       //processo no final do batch
   }
}
```
E para executar:

```bash
Database.executeBatch(new ExemploBatch('Conta1','Conta2'),10);
```
Este exemplo vai selecionar todas as contas chamadas "Conta1" e mudar o nome para "Conta2", separando o processamento em 10 contas por vez

### Você também pode passar uma lista para ser processada
Exemplo:
```bash
global class ExemploBatch implements Database.Batchable<sObject> {
  List<Account> contas = new List<Account>();
  
  public ExemploBatch(List<Account> contas){
        this.contas = contas;
    }
 
   global System.Iterable<sObject> start(Database.BatchableContext BC) {
       return contas;
   }
```

Atenção: No método execute, você vai trabalhar com a lista que ele recebe(scope) e não com a lista de contas.

## Links Úteis

Documentação: https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_batch_interface.htm

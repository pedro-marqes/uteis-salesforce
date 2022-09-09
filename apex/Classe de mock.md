# O que faz o codigo ?

Classe de mock para fazer classe de testes para callouts


## Codigo

Código para a classe de mock

```bash
@isTest
global class nomeDoMock implements HttpCalloutMock{
    
    global HTTPResponse respond(HTTPRequest req) {        
        //resposta 
        HttpResponse res = new HttpResponse();
        res.setHeader('Content-Type', 'application/json');
        res.setBody('{"example":"test"}');
        res.setStatusCode(200);
        return res;
    }
}

```

Chamar a classe de mock na classe de testes
```bash
Test.setMock(HttpCalloutMock.class, new nomeDoMock());
```

## Links Úteis

Documentação: https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_classes_restful_http_testing_httpcalloutmock.htm

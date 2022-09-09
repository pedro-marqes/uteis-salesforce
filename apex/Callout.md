# O que faz o codigo ?

Faz requisição para uma API

## Codigo

Lembrar de sempre executar em uma classe com a anotação ```@Future(Callout=true)```

```bash
HttpRequest httpRequest = new HttpRequest();
httpRequest.setMethod('GET');
httpRequest.setEndpoint(RequestURL);
httpRequest.setHeader('Content-Type', 'application/json');
httpRequest.setHeader('accept', 'application/json');
httpRequest.setBody(JSON.serialize(Classe com o Json));
httpRequest.setTimeout(120000);
            
HttpResponse httpResponse = new Http().send(httpRequest);
//event.BeeIntegration__ResponseBody__c = httpResponse.getBody();
CobrancaResponse response;
if (
  httpResponse.getStatusCode() > 199 &&
  httpResponse.getStatusCode() < 300
) {
  //event.BeeIntegration__Status__c = 'SUCCESS';
  response = (classe) System.JSON.deserialize(httpResponse.getBody(), classe.class);
}
```
## Exemplo de classes para o JSON

```bash
// Classe para enviar um JSON para a API
public class CobrancaTO {
        public integer codigoEmpresa;
        public String tipoAdiantamento;
        public double valor;
        public String observacao;
        public String dataEntrada;
        public String dataVencimento;
        public integer codigoFormaCobranca;
        public integer codigoEmpresaFC;
        public String codigoNaturezaReceitaDespesa;
        public String codigoCliente;
        public String documento;
    }
    
    //Classes para receber o JSON da api
    public class CobrancaResponse{
        String timestamp;
        Boolean sucess;
        BoletoTO data;
    }
    
    public class BoletoTO{
        String codigoTipoFatura;
        Integer numeroFatura;
        String boleto;
        String qrCode;
        String copiaCola;
    }

```

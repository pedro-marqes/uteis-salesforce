# O que faz o codigo ?

Converter Base64 em um PDF   

## Codigo


```bash
Attachment attach = new Attachment();
attach.contentType = 'application/pdf';
attach.name = 'Nome do arquivo.pdf';
attach.parentId = Id do registro pai;
attach.body = EncodingUtil.base64Decode(Base 64 para converter);
insert attach;
```

## Links Úteis

Classe de decodificação: https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_classes_restful_encodingUtil.htm

Classe de Attachment: https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_attachment.htm

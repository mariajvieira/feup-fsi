# CTF Week #10 (Classical Encryption)

## Cipher
We were given the following cipher:

```
 />/+=:%~:~=(/]%~>$/.(~_%$.~:~=]/>/(~$~>/(]/_~$~~=^%[~:~>_=._/]//_|/&~&|/^~_&/_=^.:=/_]~_=.$&~_|~&$/_/>[=^[%]~_~$/:=(=#=&(~]/|&/__~=|~&~*./_/;~$=(~]~.(~]/:%_~==(~%_&~|%]=|=__%[/^/^~>:=..(~|&=|=_$~]/#%>%$%[~|/^~.^$%(~[/!/_|/&~~$/(/~]=_]/#/[/&/%&=_/~%=:=>$&~$=]/#%>%$%[=>~=#=&~__%>~]=~=^%[~~)~>]=>~&~~_%>_$~^~:=/_]~/(|&/_~/>~=,~[/&~>/+=:%=|~&~>%>+./(~(~%=&/(|&/_~]/$&~>_|=&$/_|=&$.+./_~~^~__/>%>%:%=..(|&=:/__=]/(.]~>:~]/%(~+/(//_$~~|&/|~&~&~_.~/>$&~]~>=_/:$=&]~]%_$&%).%:~=%>$/&>~*./&/(=_~|&=[/%$~&~=(~{!^;(~=||$;~~#!+/}
 ```

## Frequency
We started by checking the frequency of each character:

| Character | Frequency |
|-----------|-----------|
| ```~```   | 89        |
| ```/```   | 65        |
| ```=```   | 49        |
| ```_```   | 42        |
| ```&```   | 35        |
| ```%```   | 33        |
| ```>```   | 27        |
| ```$```   | 26        |
| ```]```   | 24        |
| ```(```   | 23        |
| ````\|````   | 22        |
| ```.```   | 19        |
| ```:```   | 16        |
| ```^```   | 12        |
| ```[```   | 11        |
| ```+```   | 6         |
| ```#```   | 6         |
| ```;```   | 3         |
| ```!```   | 3         |
| ```*```   | 2         |
| ```)```   | 2         |
| ```,```   | 1         |
| ```{```   | 1         |
| ```}```   | 1         |

Then we check the frequency of groups with 2 and 3 characters:

| 2 characters   | Frequency | 3 characters   | Frequency |
|-----------|----------|----------|----------|
| ```/_```  | 15       | ```~&~``` | 6        |
| ```&~```  | 15       | ```~]/``` | 5        |
| ```(~```  | 13       | ```/_~``` | 4        |
| ```~=```  | 11       | ```&/_``` | 4        |
| ```]/```  | 11       | ```$&~``` | 4        |
| ```~>```  | 10       | ```\|~&``` | 4        |
| ```~]```  | 10       | ```\|&/``` | 4        |
| ```~_```  | 9        | ```~:~``` | 3        |
| ```/(```  | 9        | ```:~=``` | 3        |
| ```_~```  | 8        | ```.(~``` | 3        |
| ```~&```  | 8        | ```=]/``` | 3        |
| ```&/```  | 8        | ```%[~``` | 3        |
| ```~~```  | 7        | ```/_\|``` | 3        |
| ```]~```  | 7        | ```/&~``` | 3        |
| ```\|&```  | 7        | ```/^~``` | 3        |
| ```%>```  | 7        | ```&~_``` | 3        |
| ```/>```  | 6        | ```(~]``` | 3        |
| ```$/```  | 6        | ```=(~``` | 3        |
| ```~$```  | 6        | ```~\|&``` | 3        |
| ```$~```  | 6        | ``` \| &=``` | 3      |
|...|...|...|...|

## Character Subtituion

First, we substituted the characters with the highest frequency with the most common characters in Portuguese: ```a```, ```e```, ```o```, ```s```, ```r```, ```i```, ```n```,(...) and we did the same with the groups of 2 and 3 characters.

That way, we started to find some words and parts of words. We continued substituing and then we find some words like: ```Negociação```, ```Proposta```, ```Empresa```, ```Contrato```, (...), that helped us understand the context of the text.

## Decrypted text and flag

We discourved the the text that was in the newspaper:
```
ENEGOCIACAOMEDIANTEUMASITUACAODENEMATANEMDESATAAOLIVACANSOUSEDEESPERARPELASRESOLUCOESDASOUTRASPARTESENVOLVIDASATECOMOFORMADEPRESSAOPARAQUESEHATOMADAUMADECISAOOMAISRAPIDOPOSSIVELELANCOUUMAPROPOSTADEFINITIVAPELAULTIMAVEZESPERAATEMEADOSDEFEVEREIROSEAIOCONTRATODEFINITIVONAOFORASSINADOAOLIVAABANDONARAASINSTALACOESDAEMPRESAENAOJAVERANEGOCIOPARANINGUEMAMAIOREMPRESADETRANSPORTESPORTUGUESAALASSENINICIOUUMPROCESSODEMUDANCADEIMAGEMEESTAAPREPARARASUAENTRADANOSECTORDADISTRIBUICAOINTERNAQUEREMOSAPROVEITARAOMA{ZLHMAOPPTHAAFZGE}
```

 We made some corrections, adding spaces, accents, and commas as well:
```
E negociação mediante uma situação de nem ata nem desata, a Oliva cansou-se de esperar pelas resoluções das outras partes envolvidas. Até como forma de pressão para que seja tomada uma decisão o mais rápido possível, lançou uma proposta definitiva pela última vez e espera até meados de fevereiro. Se aí o contrato definitivo não for assinado, a Oliva abandonará as instalações da empresa e não haverá negócio para ninguém. A maior empresa de transportes portuguesa, Alassen, iniciou um processo de mudança de imagem e está a preparar a sua entrada no setor da distribuição interna. Queremos aproveitar ao ma {zljmaopptjaafzge}.
```
We found the flag:

```{!^;(~=||$;~~#!+/}``` -> ```{zljmaopptjaafzge}```
## Key

We key to decypher was:

```~/=_&%>$](|.:^[+#;!*),``` -> ```AEOSRINTDMPUCLVGFHZQBJ```

(We used the following command to substitute:
```tr '~/=_&%>$](|.:^[+#;!*),' 'AEOSRINTDMPUCLVGFHZQBJ' < L05G06.cph > substituted.txt```)

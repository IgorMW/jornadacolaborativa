# PoC Jornada Colaborativa
  
## PoC para testar retorno de API do IBGE com algumas validações utilizando Newman, Github Actions e Github Pages.  
  

### O [endpoint](https://servicodados.ibge.gov.br/api/docs/nomes?versao=2) escolhido retorna os 20 nomes mais comuns no Brasil. Cuja resposta possui o seguinte padrão:
```
[
    {
        "localidade": "string",
        "sexo": "string",
        "res": [
            {
                "nome": "string",
                "frequencia": number,
                "ranking": number
            }
        ]
    }
]
```  
  
### São realizados 3 testes básicos na resposta recebida:
- Código de resposta igual a a 200
- Resposta menor que 10 segundos
- Ter no corpo da resposta o vigésimo nome  
  
### A criação do relatório é realizada utilizando a imagem [dannydainton/htmlextra](https://github.com/DannyDainton/newman-reporter-htmlextra). 
  
```console
          docker container run -t -v $(pwd):/etc/newman dannydainton/htmlextra \
          run 'jornadacolaborativa.postman_collection.json' \
          -k \
          -r cli,htmlextra \
          --reporter-htmlextra-export /etc/newman/docs/index.html \
          --reporter-htmlextra-browserTitle "Jornada Colaborativa" \
          --reporter-htmlextra-title "Jornada Colaborativa - Nomes Mais Comuns No Brasil"
```  
  
### Etapa de publicação no GitHub Pages. Utilizamos o [GitHub Pages Action](https://github.com/marketplace/actions/github-pages-action) para isso.
```console
      - name: Publish Report
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs
```

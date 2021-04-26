
## Command to start the Newman htmlextra container

```console
docker container run -t -v $(pwd):/etc/newman dannydainton/htmlextra \
    run 'jornadacolaborativa.postman_collection.json' \
    -k \
    -r cli,htmlextra \
    --reporter-htmlextra-export /etc/newman/index.html \
    --reporter-htmlextra-browserTitle "Jornada Colaborativa" \
    --reporter-htmlextra-title "Jornada Colaborativa - Nomes Mais Comuns No Brasil"
```


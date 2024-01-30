# Docker-container for "dummies" 

Så, du har laget en megakul app, men vil ikke bruke tusenvis av kroner, timer og tårer på å sette den opp på din lokale potetmasin i skapet på hybelen, samt at kompisne din, Roger, som du har slept deg med inn i en start-up hvor dere skal lage det neste Palworld-spillet, ikke har noe mer enn en chromebook fra 2015 å kjøre den eventuelle windows-appen dere skal lage. Da er docker løsningen for dere! I denne lille introen skal du få bygge din egen docker-container med noe kult inni, om du vil, for å så fyre den av opp mot skyen. 

## Så hva er Docker? 
Docker er en kontaineriserings-tjenste som gjør at man kan kjøre programmer og apper på dedikerte "servere" uavhengig av server-type, operativ-system eller annet trøbbel man måtte støte på hos sin lokale datamaskin. Dette gjør det også mulig å spare både plass, penger og svette, da man kan ha kjørende flere docker-tjenester samtidig lokalt, eller betale en slik og ingenting for å ha det kjørende i skyen. Mer info om selve Docker finner du på https://www.docker.com/ 

### Hva trenger du for å kjøre denne modulen? 
Det du trenger er:

1. en datamaskin med Visual Studio Code
2. Tilgang til et Azure-miljø
3. docker desktop (finnes her: https://www.docker.com/products/docker-desktop/)
4. Noe å bygge til en container

### Hallo, Docker! 
I denne modlulen har vi gitt en veldig enkel .NET app som gir en klassisk "Hello, World" Du kan selv bestemme om du vil bruke denne, eller ta ditt lokale prosjekt ut i en container! 

Det hele vil foregå i filen `Dockerfile` hvor man skal skrive en "oppskrift" som Docker skal kjøre etter. Den vil fra start av se omtrent slik ut: 

```
FROM  mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY bin/Debug/net7.0/BabysFirstDockerContainer.dll .
ENTRYPOINT [ "dotnet", "babysfirstdockercontainer.dll" ]
```

Dette gir instruksjoner til Docker Engine om hvordan docker-filen skal oppføre seg. Denne filen skal hente ut ASPNET versjon 7.0 fra Microsoft sine nettsider via `FROM`-kommandoen, så sette `WORKDIR` til /app, altså hvor den skal starte appen fra. `COPY` kopierer 